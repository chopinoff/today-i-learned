
# Hello World

가장 단순한 예시

```jsx
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<h1>Hello, world!</h1>);
```

# JSX 소개

## JSX란?

JavaScript를 확장한 문법, React element를 생성함

React에서는 렌더링 로직이 UI 로직과 연결됨 (이벤트 처리 방식, 시간에 따라  state가 변하는 방식, 화면에 표시하기 위해 데이터가 준비되는 방식)


## JSX에 표현식 포함하기

```jsx
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;
```

JSX의 중괄호 안에는 유효한 모든 JavaScript 표현식을 넣을 수 있음

## JSX 자체도 표현식이다

컴파일이 끝나면 정규 JavaScript 함수 호출이 되고 JSX 표현식이 JavaScript 객체로 인식됨

즉, JSX를 `if` 구문 및 `for` loop 안에 사용하고, 변수에 할당하고, 인자로서 받아들이고, 함수로부터 반환할 수 있음

```jsx
function getGreeting(user) {
	if (user) {
		return <h1>Hello, {formatName(user)}!</h1>;  
	}
		return <h1>Hello, Stranger.</h1>;
}
```


## JSX 속성 정의

어트리뷰트에 따옴표를 사용해 문자열 리터럴 정의
```jsx
const element = <a href="https://www.reactjs.org"> link </a>;
```

어트리뷰트에 중괄호를 사용해 JavaScript 표현식 삽입
```jsx
const element = <img src={user.avatarUrl}></img>;
```

### 주의
1. 따옴표, 중괄호 두 가지를 동시에 사용하면 안 됨
2. JSX는 JavaScript에 더 가깝기 때문에 camelCase 프로퍼티 명명 규칙을 따름
	- ex)  `class` > `className`, `tabindex` > `tabIndex`

## JSX로 자식 정의

태그가 비어있을 경우 `/>`를 사용해 바로 닫아주어야 함
```jsx
const element = <img src={user.avatarUrl} />;
```

JSX 태그는 자식을 포함할 수 있음
```jsx
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

## JSX는 주입 공격을 방지함

JSX는 XSS 공격을 막을 수 있음
