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
  
### URL 파라미터와 쿼리
  
- 파라미터 예시 : `/profiles/velopert`
- 쿼리 예시 : `/about?details=true`
  
파라미터는 `특정 아이디` 혹은 `이름`을 사용하여 조회할 때 사용  
  
쿼리는 `키워드를 검색`하거나 페이지에 필요한 `옵션을 전달`할 때 사용  
  
### URL 파라미터
  
`URL 파라미터`를 사용할 때는 라우트로 사용되는 컴포넌트에서 받아 오는 `match라는 객체` 안의 `params` 값을 참조한다  
  
```jsx
const Profile = ({match}) => {
  const {paramValue} = match.params;
}
```
  
사용할 `path 규칙`은 `/urlAddress/:typeSomething` <-- 형태로 작성하면 된다  
  
```jsx
<Route path="/profile/:username" component={Profile} />
```
  
### URL 쿼리
  
쿼리는 `location 객체`에 들어 있는 `search` 값에서 조회할 수 있다  
  
`location 객체`는 라우트로 사용된 컴포넌트에게 `props`로 전달되며  
  
웹 애플리케이션의 현재 주소에 대한 정보를 지니고 있다  
  
`URL 쿼리`를 읽을 때는 객체가 지닌 값 중에서 `search` 값을 확인해야 한다  
  
이 값은 `문자열` 형태로 되어있다  
  
`search` 값에서 특정 값을 읽어 오기 위해서는 이 문자열을 객체 형태로 변화해 주어야 한다  
  
쿼리 문자열을 객체로 변환할 때는 `qs`라이브러리를 사용한다  
  
```
yarn add qs
```
  
쿼리를 사용할 때는 쿼리 문자열을 객체로 파싱하는 과정에서 결과 값은 언제나 문자열이라는 점에 주의한다
  
```
import qs from 'qs';

const About = ({ location}) => {
  const query = qs.parse(location.search, {
    ignoreQueryPrefix: true // 이 설정을 통해 문자열 맨 앞의 ?를 생략한다
  });
  
  const showDetail = query.detail === 'true'; // 쿼리의 파싱 결과 값은 문자열
};
```  
  
### 서브 라우트
  
서브 라우트는 내부에 또 라우트를 정의하는 것을 의미  
  
라우트로 사용되고 있는 컴포넌트의 내부에 그저 `Route 컴포넌트`를 또 사용하면 된다  
  
