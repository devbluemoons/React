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

const list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

let placeHolder = "선택을 해주세요.";

function Select({ data }) {
    // state
    const [isOpen, setIsOpen] = useState(false);
    const [isOn, setIsOn] = useState("on");
    const [isScroll, setIsScroll] = useState("scrolling");
    const [inputValue, setInputValue] = useState("");
    const [isMove, setIsMove] = useState(0);

    // reference
    const selectBox = useRef();
    const scrollBox = useRef();
    const itemList = useRef();
    let isPress = useRef(false);
    let event = useRef(null);

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

        if (itemList.current) {
            const { current } = itemList;
            const move = current.firstChild.offsetHeight;

            switch (e.target.name) {
                case "up":
                    scrollBox.current.scrollTop -= move;
                    break;
                case "down":
                    scrollBox.current.scrollTop += move;
                    break;
            }

            setIsMove(scrollBox.current.scrollTop);
        }
    };
    const onMouseUp = () => (isPress.current = false);

    // watch
    useEffect(() => {
        setIsOn(isOpen ? "on" : "");

        if (isOpen) {
            const selecBoxHeight = selectBox.current.offsetHeight;
            const itemListHeight = itemList.current.offsetHeight;

            const result = selecBoxHeight < itemListHeight;
            setIsScroll(result ? "scrolling" : "");
        }
    }, [isOpen]);

    useEffect(() => {
        setTimeout(() => {
            isPress.current && onMouseDown(event.current);
        }, 100);
    }, [isMove]);

    // view
    return (
        <div className="input-box" onMouseLeave={onMouseLeave}>
            <div className={`select-input ${isOn}`} onClick={onClick}>
                <input type="text" value={inputValue} placeholder={placeHolder} readOnly />
            </div>

            {isOpen && (
                <div className={`select-items ${isScroll}`} ref={selectBox}>
                    <div className="scroll-box" ref={scrollBox}>
                        <ul ref={itemList}>
                            {list.map((item, index) => (
                                <li key={index} onClick={onSelect}>
                                    <a>{item}</a>
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
