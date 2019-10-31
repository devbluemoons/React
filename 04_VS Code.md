## VS Code  
  
`VS Code`는 `MicroSoft`사에서 개발한 `오픈소스 에디터`이다  
  
###### VS CODE `확장 프로그램` 설치  
  
`확장 프로그램`을 통하여 편리한 개발환경을 구축할 수 있다  
  
확장 프로그램은 `VS Code` 내부의 `마켓플레이스`에서 검색하여 설치할 수 있다  
  
- `ESLint` : 자바스크립트 문법 및 코드 스타일 검사
- `Reactjs Code Snippets` : 컴포넌트 및 라이프사이클 함수를 작성할 때 단축단어 사용 코드를 자동으로 생성
- `Prettier-Code formatter` : 코드 스타일 자동으로 정리
  
---  
  
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
  
`Pretiier Options` 페이지에서 (https://prettier.io/docs/en/options.html) 다양한 옵션을 참조할 수 있다  
  
`VS Code` 설정은 상단메뉴의 하위 `settings` 창으로 들어가서 검색창에 `format on save`를 검색 후  
  
나타나는 체크 박스에 체크하여 저장할 때마다 코드가 자동으로 정리되도록 설정할 수 있다  
  
