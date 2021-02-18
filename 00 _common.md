## `Timer`
```js
yarn add react-live- click --save
```
  
```js
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
