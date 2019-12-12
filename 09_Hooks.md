## Hook이란 
  
`Hook`은 `함수형 컴포넌트`에서 `상태관리` 및 기능을 외부로 꺼내어 공유하기 위해 사용하는 기능   
  
###### Hooks 사용법  
  
```jsx
import React, { useState, useEffect, useReducer, useMemo, useCallBack, useRef, useContext } from 'react';
```
  
---
  
## useState()  
  
함수형 컴포넌트에서도 가변적인 상태를 지닐 수 있게 해준다  
```jsx
const [value, setValue] = useState(3);
```
  
## useEffect()  
  
컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정할 수 있다  
  
기본적으로 렌더링되고 난 직후마다 실행  

두 번째 배열에 무엇을 넣는지에 따라 실행되는 조건이 달라진다  
              
컴포넌트가 화면에 맨 처음 렌더링될 때만 실행하고,  
  
업데이트될 때는 실행하지 않으려면 함수의 두번째 파라미터로 `비어있는 배열`을 넣는다  
```jsx
useEffect(() => {
  console.log('마운트될 때만 실행');
},[])  <-- 바로 여기 (비어있는 배열)
```
  
###### 특정 값이 업데이트될 때만 실행하고 싶을 때  
  
두 번째 파라미터로 전달되는 배열 안에 검사하고 싶은 값을 넣어주면 된다  
```jsx
useEffect(() => {
  console.log(value);
},[value])
```    
  
컴포넌트가 언마운트되기 전이나 업데이트되기 직전에 어떠한 작업을 수행하고 싶다면 `뒷정리 함수`를 반환  
  
업데이트되기 직전의 값을 보여준다  

```jsx
useEffect(() => {
  console.log(value);
  return () => {
    console.log("return 구문이 뒷정리 함수")
  }
})
```
  
언마운트 될 때만 뒷정리 함수를 호출할 경우, 두번째 파라미터에 `비어있는 배열`을 넣는다  
  
```jsx
useEffect(() => {
  console.log(value);
  return () => {
    console.log("return 구문이 뒷정리 함수")
  }
},[])  <-- 바로 여기 (비어있는 배열)
```     
               
## useReducer()  
  
현재 상태, 업데이트를 위해 필요한 정보를 담은 액션값을 전달받아 `새로운 상태`를 반환하는 함수  
  
리듀서 함수에서 `새로운 상태`를 만들 때는 반드시 `불변성`을 지켜 주어야 한다  
  
```jsx
function reducer(state, action){
  return {
    ...state,
    [action.name]: action.value <-- 객체 내부에서 필드를 []로 감싸주면 값 자체가 필드명이 된다 
  };
}

const [state, dispatch] = useReducer(reducer, {
  name: '',
  nickname: ''
});

const { name, nickname } = state;
const onChange = e => {
  dispatch(e.target);
};
```                 
                 
## useMemo()  
  
함수형 컴포넌트 내부에서 발생하는 연산을 `최적화`할 수 있다  
  
렌더링하는 과정에서 특정 값이 바뀌었을 때만 연산을 실행하고  
    
값이 바뀌지 않았다면 이전에 연산했던 결과를 다시 사용하는 방식  
  
```jsx
useMemo(() => getAverage(list), [list]);
```
  
이 예제에서 대상 함수`getAverage(list)`에 대상값`list`을 담아 `useMemo()` 함수의 첫번째 인자로 넣고  
  
두번째 함수로 대상값 `list`를 배열에 담아 넣어준다  
  
`useMemo()` 함수가 호출이 되고 값이 변경될 경우만 연산하여 반환하고,  
  
값이 변경되지 않을 경우 두번째 배열에 넣어준 값을 참조한다  
  
## useCallback()  
  
렌더링 성능을 최적화해야 하는 상황에서 사용  
  
이벤트 핸들러 함수를 필요할 때만 생성할 수 있다  
  
첫 번째 파라미터에는 생성하고 싶은 함수를 넣고 두 번째 파라미터에는 배열을 넣는다  
  
두 번째 파라미터에 `비어있는 배열`을 넣게 되면 컴포넌트가 렌더링될 때 단 한 번만 함수가 생성된다  
  
함수 내부에서 상태 값에 의존해야 할 경우, 그 값을 두 번째 파라미터 안에 반드시 포함시켜 주어야 한다  
  
```jsx
onChange = useCallback(e => {
  setNumber(e.target.value);
},[]);  <-- (비어있는 배열)

onInsert = useCallback(() => {
  const nextList = list.concat(parseInt(number));
  setList(nextList);
  setNumber('');

}, [number, list]);  <-- (number 혹은 list가 바뀌엇을 때만 함수 생성)
```
  
  
숫자, 문자열, 객체처럼 일반 값을 재사용하려면 `useMemo`를 사용  
  
함수를 재사용하려면 `useCallback`을 사용  
  
```jsx                  
useCallback(() => {
  console.log('hello world');
}, [])

useMemo(() => {
  const fn = () => {
    console.log('hello world');
  };
  return fn;
}, [])
```        
             
## useRef()  
  
함수형 컴포넌트에서 ref를 쉽게 사용할 수 있도록 해준다  
  
렌더링이랑 상관없이 바뀔 수 있는 값에도 사용  

```jsx
const inputEl = useRef(null);
<input value={number} onChange={onChange} ref={inputEl} />

const id = useRef(1);
const setId = (n) => {
  id.current = n;
}
```                           
`ref`안의 값이 바뀌어도 컴포넌트가 렌더링되지 않는다는 점에는 주의해야 한다  
  
렌더링과 관련되지 않는 값을 관리할 때만 이러한 방식으로 코드를 작성한다  
  
## useContext()
  
함수형 컴포넌트에서 `Context`를 아주 편하게 사용할 수 있다  
  
```jsx
const { state } = useContext(ColorContext);

<div
  style={{
    width: '64px';
    height: '64px';
    background: state.color
  }}
/>
```
  
## 커스텀 Hooks  
  
여러 컴포넌트에서 비슷한 기능을 공유할 경우 만들어 사용한다  
  
마치 `service 로직`을 따로 분리하여 `재사용`하는 것고 비슷한 용도로 사용  
  
 ```jsx
 function reducer(state, action){
   return{
     ...state,
     [action.name]: action.value
   };
 }
  
export default function useInputs(initialForm){
  const [state, dispatch] = useReducer(reducer, initialForm);
  const onChange = e => {
    dispatch(e.target);
  };
  return [state, onChange];
}
 ```
###### 정의한 커스텀 Hook을 다른 파일에서 사용  
  
```jsx
const [state, onChange] = useInputs({
  name: '',
  nickname: ''
});

const { name, nickname} = state;
```
                    
                
                 
