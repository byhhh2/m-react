# Component

- react의 가장 기본적인 단위
- 더욱 큰 것의 일부
- 우리가 정의하는 어떤 형태로도 구현할 수 있다.
  - 역할의 분리 없이 단 하나의 컴포넌트로 디자인하는 것도 가능하다. 하지만 이렇게 하지 않는 이유는 컴포넌트가 가진 장점을 활용할 수 없기 때문이다. 이런 이유로 여러개의 컴포넌트로 나눠서 구성하고, 재사용할 수 있게 고민한다.
- 컴포넌트는 같은 공간에 존재하고 독립적으로 인터렉션한다.
- 캡슐화되어 있고, 재사용 • 재구성 할 수 있다.
- App을 개발한다는 것은 **레고**를 조립하는 것과 비슷하다. 레고와의 차이점은 부품이 부족할 일이 없고, 반드시 한 번은 재사용할 컴포넌트를 만들어야한다는 것
- 상호작용하는 여러 컴포넌트들을 **조합**해서 새로운 형태의 **합성** 컴포넌트를 만들 수 있다. 또, react의 가장 큰 장점 중 하나인데, 컴포넌트를 만든 후 **재사용**을 통해 app의 다른 부분에서도 사용할 수 있다.
  - 재사용 가능한 특징은 app의 중요한 요소이다.
  - 복제된 여러 컴포넌트들이 독립적으로 실행될 수 있을 때 side effect를 줄이고, 개발의 효율성을 극대화할 수 있다.

<br>

## ✨ web component

> 웹 컴포넌트는 그 기능을 나머지 코드로부터 캡슐화하여 재사용 가능한 커스텀 엘리먼트를 생성하고 웹 앱에서 활용할 수 있도록 해주는 다양한 기술들의 모음입니다. - [MDN](https://developer.mozilla.org/ko/docs/Web/Web_Components)

- 가능한 코드를 재사용하는 것이 좋은 생각이라는 것을 알고 있다.
  - 하지만 전통적 커스텀 마크업 구조에선 쉽지 않다.
  - HTML을 여러번 사용할 때 조심하지 않으면 페이지가 엉망이 될 수 있다.
- 웹 컴포넌트는 다음 문제들을 해결하는 것을 목표로 한다.
  - 세가지 주요 기술들로 구성
    - `custom element` : custom element와 그 동작을 정의할 수 있도록 해주는 JS API의 집합, UI에서 원하는대로 사용될 수 있다.
    - `shadow DOM` : 메인 document DOM으로 부터 독립적으로 렌더링 (shadow DOM tree), 이와 연관된 기능을 제어하기 위한 JS API의 집합, shadow DOM을 통해 element기능을 private하게 유지할 수 있어 document의 다른 부분과의 충돌 걱정없이 스크립트와 스타일을 작성할 수 있다.
    - `HTML template` : `<template>`, `<slot>` element / 렌더링된 페이지에 나타나지 않는 마크업 템플릿을 작성할 수 있게 해준다. custom element 구조 기반으로 여러번 재사용할 수 있다.
  - 재사용을 원하는 어느곳이든 코드 충돌에 대한 걱정이 없는 캡슐화된 기능을 갖춘 다용도의 custom element를 생성하기 위해 함께 사용될 수 있다.

<br>

## ✨ react에서의 컴포넌트

- 개념적으로 컴포넌트는 JS 함수와 유사하다. props라는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 `react element`를 반환한다.
- 작고 재사용 가능한 코드 조각
- 가장 간단한 React 컴포넌트는 React 엘리먼트를 반환하는 일반 JavaScript 함수
- 컴포넌트는 기능별로 나눌 수 있으며, 다른 컴포넌트 안에서 사용할 수 있다.
- 컴포넌트는 다른 컴포넌트, 배열, 문자열, 숫자를 반환할 수 있다.
- 자주 사용되는 UI, 혹은 복잡한 UI는 재사용 가능한 컴포넌트가 될 수 있다.

### 함수 컴포넌트

- props 객체 인자를 받은 후 react element를 반환

### 클래스 컴포넌트 (ES6 class)

- react 관점에서는 함수 컴포넌트나 클래스 컴포넌트나 동일하다.
- class는 몇가지 추가 기능이 존재한다.
- class 컴포넌트를 정의하려면 `React.Component`를 상속받아야한다.
- `render()` 함수는 `React.Component`의 하위 class에서 반드시 정의해야하는 메서드, 나머지는 선택사항
- 생명주기 메서드를 가진다.

---

#### 렌더링 예시

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;

ReactDOM.render(element, document.getElementById('root'));
```

1. `element`로 `ReactDOM.render()`를 호출한다.
2. react는 `{name: 'Sara'}`를 props로 하여 `Welcome` 컴포넌트를 호출합니다.
3. `Welcome` 컴포넌트는 결과적으로 `<h1>Hello, Sara</h1>` 엘리먼트(react element)를 반환합니다.
4. React DOM은 `<h1>Hello, Sara</h1>` 엘리먼트와 일치하도록 DOM을 효율적으로 업데이트합니다.

---

### 사용할 때의 특징

- 컴포넌트의 이름은 항상 대문자로 시작한다. (react에서는 소문자로 시작하는 컴포넌트를 DOM 태그로 처리하기 때문에)

<br>

### 컴포넌트 합성

- 컴포넌트는 자신의 출력에 다른 컴포넌트를 참조할 수 있다.
  - 모든 세부 단계에서 동일한 추상 컴포넌트를 사용할 수 있다.

```jsx
function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

// Welcome 컴포넌트를 여러번 렌더링하는 App 컴포넌트 (Welcome 참조)
```

<br>
<br>

## 참고

- 우테코 LMS - Component
- [react 공식문서 - components와 props](https://ko.reactjs.org/docs/components-and-props.html)
- [react 공식문서 - React.Component](https://ko.reactjs.org/docs/react-component.html#gatsby-focus-wrapper)
- [react 공식문서 - component](https://ko.reactjs.org/docs/glossary.html#components)
