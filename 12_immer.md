## immer  
  
`전개 연산자`와 `배열의 내장 함수`를 사용하면 간단하게 배열 혹은 객체를 복사하고 새로운 값을 덮어 쓸 수 있다  
  
하지만 객체의 구조가 엄청나게 깊어지면 불변성을 유지하면서 이를 업데이트하는 것이 매우 힘들다  
  
이러한 상황에 `immer` 라이브러리를 사용하면, 구조가 복잡한 객체도 매우 쉽고 짧은 코드를 사용하여  
  
불변성을 유지하면서 업데이트해 줄 수 있다  
  
```
yarn add immer
```  
  
```jsx
import produce from 'immer';
const nextState = produce(originalState, draft => {
  // 바꾸고 싶은 값 바꾸기
  draft.somewhere.deep.inside = 5;
})
```
  
`produce`라는 함수는 두 가지 파라미터를 받는다  
  
첫 번째 파라미터는 `수정하고 싶은 상태`이고    
  
두 번째 파라미터는 `상태를 어떻게 업데이트할지 정의하는 함수`이다  
  
두 번째 파라미터로 전달되는 함수 내부에서 원하는 값을 변경하면  
  
`produce` 함수가 불변성 유지를 대신해 주면서 `새로운 상태를 생성`해 준다  
  
이 라이브러리의 핵심은 `불변성에 신경 쓰지 않는 것처럼 코드를 작성하되 불변성 관리는 제대로 해 주는 것`이다  
  
`immer`를 사용하여 컴포넌트 상태를 작성할 때는 `객체 안에 있는 값을 직접 수정`하거나  
  
배열에 직접적인 변화를 일으키는 `push`, `splice` 등의 함수를 사용해도 무방하다  
  
```jsx
import produce from 'immer';

const originalState = [
  {
    id: 1,
    todo: 'test001',
    checked: true,
  },
  {
    id: 2,
    todo: 'test002',
    checked: false,
  },
];

const nextState = produce(originalState, draft => {
  const todo = draft.find(t => t.id === 2);
  todo.checked = true;
  
  draft.push({
    id:3,
    todo: 'test003',
    checked: false,
  });
  
  draft.splice(draft.findIndex(t => t.id === 1), 1);
});
```  
