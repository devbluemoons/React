## `Timer`
```js
yarn add react-live-clock --save
yarn add react-moment --save
yarn add moment-timezone --save
```
  
```jsx
import Clock from "react-live-clock";

function Timer() {
    const currentDay = ["일", "월", "화", "수", "목", "금", "토"][new Date().getDay()];

    return (
	<div className="time-box">
	    <Clock format={`생산일 : YYYY년 MM월 DD일 (${currentDay}) HH:mm:ss`} ticking={true} />
	</div>
    );
}

export default Timer;
```
  
## `Select`
```jsx
import { useState, useEffect, useRef } from "react";
import { useRecoilState } from "recoil";
import { focusState } from "@/state/focusState";
import { openState } from "@/state/openState";

const list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const placeHolder = "선택해 주세요.";

function Select({ data }) {
	// state
	// const [isOpen, setIsOpen] = useState(false);
	const [isOn, setIsOn] = useState("on");
	const [isScroll, setIsScroll] = useState("scrolling");
	const [inputValue, setInputValue] = useState("");
	const [isMove, setIsMove] = useState(false);
	const [isFocus, setIsFocus] = useRecoilState(focusState);
	const [isOpen, setIsOpen] = useRecoilState(openState);

	// reference
	const selectBox = useRef();
	const scrollBox = useRef();
	const itemList = useRef();
	const componentRef = useRef();

	// local variables
	const isPress = useRef(false);
	const event = useRef(null);

	// event
	const onClick = () => setIsOpen(!isOpen);
	const onMouseLeave = () => setIsOpen(false);
	const onSelect = e => {
		setInputValue(e.target.innerText);
		setIsOpen(false);
	};
	const onMouseDown = e => {
		isPress.current = true;
		event.current = e;

		if (!itemList.current) {
			return false;
		}

		const { current } = itemList;
		const move = current.firstChild.offsetHeight;
		let scrollTop = scrollBox.current.scrollTop;

		switch (e.target.name) {
			case "up":
				scrollTop -= move;
				break;
			case "down":
				scrollTop += move;
				break;
			default:
		}

		scrollBox.current.scrollTop = scrollTop;
		setIsMove(scrollTop);
	};
	const onMouseUp = () => (isPress.current = false);

	// watch
	useEffect(() => {
		setIsOn(isOpen ? "on" : "");

		if (isOpen) {
			const selectBoxHeight = selectBox.current.offsetHeight;
			const itemListHeight = itemList.current.offsetHeight;

			const result = selectBoxHeight < itemListHeight;
			setIsScroll(result ? "scrolling" : "");
			setIsFocus(componentRef.current);
		}
	}, [isOpen]);

	useEffect(() => {
		setTimeout(() => {
			isPress.current && onMouseDown(event.current);
		}, 100);
	}, [isMove]);

	// view
	return (
		<div className="input-box" ref={componentRef}>
			<div className={`select-input ${isOn}`} onClick={onClick}>
				<input type="text" value={inputValue} placeholder={placeHolder} readOnly />
			</div>

			{isOpen && (
				<div className={`select-items ${isScroll}`} ref={selectBox}>
					<div className="scroll-box" ref={scrollBox}>
						<ul ref={itemList}>
							{list.map(i => (
								<li key={i.toString()} onClick={onSelect}>
									<a>{i}</a>
								</li>
							))}
						</ul>
					</div>
					<div className="scroll-btn">
						<a className="up-btn" name="up" onMouseDown={onMouseDown} onMouseUp={onMouseUp}></a>
						<a className="down-btn" name="down" onMouseDown={onMouseDown} onMouseUp={onMouseUp}></a>
					</div>
				</div>
			)}
		</div>
	);
}

export default Select;

```
