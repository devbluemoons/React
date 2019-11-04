## VS Code  
  
`VS Code`는 `MicroSoft`사에서 개발한 `오픈소스 에디터`이다  
  
#### VS Code `확장 프로그램` 설치  
  
`확장 프로그램`을 통하여 편리한 개발환경을 구축할 수 있다  
  
확장 프로그램은 `VS Code` 내부의 `마켓플레이스`에서 검색하여 설치할 수 있다  
  
- `ESLint` : 자바스크립트 문법 및 코드 스타일 검사
- `Reactjs Code Snippets` : 컴포넌트 및 라이프사이클 함수를 작성할 때 단축단어 사용 코드를 자동으로 생성
- `Prettier-Code formatter` : 코드 스타일 자동으로 정리
- `Reactjs Code Snippet` :    
  - 컴포넌트 코드를 간편하고 빠르게 생성할 수 있다 
  - 에디터에서 `rsc`를 입력하고 `Enter`키를 누르면 코드가 자동으로 생성된다  
- `vscode-styled-components` : 하이라이팅(문법에 따라 에디터 폰트 색상을 입히는 작업)이 정상적으로 입혀진다  
  
---  
  
## .prettierrc
  
`VS Code`에서 `F1`키를 누르고 입력창에 `format`이라고 입력한 다음 `Enter`키를 누르면 설정을 할 수 있다  
  
`Prettier`의 장점은 스타일을 쉽게 커스터마이징 할 수 있다는 것이다  
  
프로젝트의 루트 디렉터리(src, public 디렉터리들이 위치한 곳)에서  
  
`.prettierrc`라는 파일을 생성한 후 아래와 같은 내용을 입력한다  
  
```json  
{
  "singleQuote": true,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2
}
```  
  
`Prettier Options` 페이지에서 (https://prettier.io/docs/en/options.html) 다양한 옵션을 참조할 수 있다  
  
`VS Code` 설정은 상단메뉴의 하위 `settings` 창으로 들어가서 검색창에 `format on save`를 검색 후  
  
나타나는 체크 박스에 체크하여 저장할 때마다 코드가 자동으로 정리되도록 설정할 수 있다  
  
---  
  
## jsconfig.json  
  
파일이 열려있는 상태에서는 `자동 완성 기능`이 잘 작동하지만 닫혀 있는 상태에서도 정상동작 하려면 설정이 필요하다  
  
`VS Code`에서 파일 `자동 불러오기 기능`을 잘 활용하고 싶다면 최상위 디렉터리에 `jsconfig.json` 파일 생성  
  
생성된 `jsconfig.json` 파일에서 `ctrl + space` 키를 누르면 아래와 같은 코드가 자동완성 형태로 나타난다  
  
다시 한 번 `Enter`키를 누르면 코드가 자동 완성된다  
  
```json
{
  "compilerOptions": {
    "target": "es6"
  }
}
```
  
`ctrl + space` 키는 `VS Code` 에디터의 `자동완성 단축키`이다  
  
---  
  
### 크롬 리액트 개발자 도구
  
브라우저에  나타난 리액트 컴포넌트 심층 분석할 수 있도록 리액트 개발팀이 만들었다  
  
크롬 웹 스토어에서 `React Developer 'Tools`를 검색하여 설치  
  
### 크롬 개발자 도구를 통한 성능 모니터링
  
`Performance` 탭을 사용하여 측정  
  
### Redux DevTools의 설치 및 적용
  
리덕스 개발자 도구이며, 크롬 확장 프로그램으로 설치하여 사용할 수 있다
```
