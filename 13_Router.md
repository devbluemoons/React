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
  
### Link 컴포넌트를 사용하여 다른 주소로 이동
  
`Link 컴포넌트`는 클릭하면 다른 주소로 이동시켜 주는 라이브러리이다  
  
리액트는 `a 태그`를 직접 사용하지 않고 `Link 컴포넌트`를 사용하여 다른 주소로 이동한다  
  
`a 태그`를 사용하지 않는 이유는 페이지를 새로 불러오면서 상태들을 모두 날려버리기 때문이다  
  
```jsx
import { Route, Link } from 'react-router-dom';

<div>
  <ul>
    <li>
      <Link to="/">Home</Link>
    </li>
    <li>
      <Link to="/about">About</Link>
    </li>
  </ul>
  <hr>
  <Route path="/" component={Home} exact={true} />
  <Route path="/about" component={About} />
  <Route path={['/one', '/two', '/three']} component={Multi} />
</div>
```
