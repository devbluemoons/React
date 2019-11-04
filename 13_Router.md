## Router  
  
다른 주소에 다른 화면을 보여 주는 것을 `라우팅`이라고 한다  
  
```
yarn add react-router-dom
```
  
### 프로젝트에 라우터 적용
  
프로젝트에 라우터를 적용할 때는 `src/index.js` 파일에서 `react-router-dom`에 내장되어 있는  
  
`BrowserRouter` 컴포넌트를 사용하여 감싸면 된다  
  
###### src/index.js
  
```jsx
import { BrowserRouter } from 'react-router-dom';
import App from './App';

<BrowserRouter>
  <App />
<BrowserRouter/
```
  
### Route 컴포넌트로 특정 주소에 컴포넌트 연결
  
```jsx
import { Route } from 'react-router-dom';

<div>
  <Route path="/" component={Home} exact={true} />
  <Route path="/about" component={About} />
</div>
```  
  
