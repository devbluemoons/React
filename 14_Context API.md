## Context API  
  
`전역적`으로 사용할 데이터가 있을 때 유용한 기능이다  
  
새 `Context`를 만들 때는 `createContext` 함수를 사용한다  
  
### 새 Context 만들기
  
```jsx
import { createContext } from 'react';

const ColorContext = createContext({ color: 'black' });

export default ColorContext; 
```
  
### Consumer 사용하기
  
`props`를 받아 오는 것이 아니라 `ColorContext` 안에 들어 있는 `Consumer`라는 컴포넌트 내부 값을 사용  
  
`Consumer` 사이에 중괄호를 열어서 그 안에 `함수`를 넣어준다  
  
이러한 패턴을 `Function as a child` 혹은 `Render Props`라고 한다  
  
컴포넌트의 `children`이 있어야 할 자리에 `함수`를 전달한다  
  
```jsx
<ColorContext.Consumer>
  {value => (
    <div 
      style={{
        width: '64px',
        height: '64px',
        background: value.color
      }}
    />
  )}
</ColorContext.Consumer>
```
  
### Provider
  
`Provider`를 사용하면 `Context`의 `value`를 변경할 수 있다  
```jsx
import ColorContext from './contexts/color'; // value를 지정한 컴포넌트

<ColorContext.Provider value={{ color: 'red' }}>
  (...)
</ColorContext.Provider>
```
  
만약 `Provider`를 사용했는데 `value`를 명시하지 않았다면 오류가 발생한다  
  
`Provider`를 사용할 경우 `value` 값을 꼭 명시해줘야 제대로 작동한다  
  
