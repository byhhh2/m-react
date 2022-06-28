# JSX

- JavaScript를 확장한 문법으로 자바스크립트 코드 안에서 HTML 문법을 사용할 수 있다.
  - JS안에 마크업을 넣자!
- react element를 생성한다.
- react에서는 렌더링 로직이 UI로직과 연결된다.
- 컴포넌트
  - 느슨한 유닛 (마크업 + 로직)
  - 렌더링 로직과 UI 로직이 느슨하게 컴포넌트로 연결되어 있음 (분리하는 것이 인위적이기 때문에)

<br>

## ✨ JSX 특징

- JSX의 중괄호(`{}`) 안에는 유효한 모든 JavaScript 표현식을 넣을 수 있다.
- JSX의 속성에는 따옴표(`""`) 또는 중괄호(`{}`)가 들어갈 수 있다.
  - JSX는 HTML보다는 JS에 가깝기 때문에 속성이름에 camelCase를 사용
- babel은 JSX를 `React.createElement()`호출로 컴파일한다.

```jsx
const element = <h1 className="greeting">Hello, world!</h1>; // 1

const element = React.createElement(
  'h1',
  { className: 'greeting' },
  'Hello, world!'
); // 2

// 1 === 2

const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!',
  },
};
// React.createElement()가 생성한 객체
// 이 객체는 react element라고 한다.
// React는 이 객체를 읽어서, DOM을 구성하고 최신 상태로 유지하는 데 사용합니다.
```

### JSX와 표현식은 같을까요? && JSX와 React.createElement() 는 무슨 관계일까요?

```jsx
const element = <h1>Hello, world!</h1>; // JSX
const element = React.createElement('h1', 'Hello, world!'); // 표현식
```

- babel이 JSX를 `React.createElement()`호출로 컴파일한다. - [참고](https://ko.reactjs.org/docs/introducing-jsx.html#jsx-represents-objects)

### document.createElement()와 다른 점은 무엇일까요?

- document.createElement() : return DOM element
- React.createElement() : return object (= react element)
- [참고](https://ko.reactjs.org/docs/introducing-jsx.html#jsx-represents-objects)

<br>
<br>

## 참고

- [react 공식문서 - JSX](https://ko.reactjs.org/docs/introducing-jsx.html)
- [미션 키워드 정리물 - JSX](https://github.com/byhhh2/woowacourse-mission-keyword/blob/master/level2/calculator/JSX.md)
