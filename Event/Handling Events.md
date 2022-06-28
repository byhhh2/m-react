# Event

## ✨ 이벤트 사용하기

```jsx
// React ❌

const element = document.getElementById('el');

element.addEventListener('click', () => {});

// React ⭕️

<button onClick={() => alert('클릭이 되었습니다.'}>
  클릭!
</button>
```

- react element에 인라인으로 정의한다.
- JSX 내부에서 함수로 이벤트 핸들러를 전달할 수 있다.

<br>

## ✨ bind

- `this`가 특정 객체에 연결되는 것
- `call`, `apply`, `bind` 함수로 this가 가르키는 것을 변경할 수 있다.

### `bind()`

- 인자로 전달된 객체를 새로 생성되는 함수안에서의 this가 가르키도록 한다.
- 새로운 함수를 생성하는 방식

```js
function originalFunction(a, b) {
  console.log(this.objValue); // objValue
  // bind()를 통해 this가 obj를 가르키게 됨

  console.log(a, b); // 1, 2
}

const obj = {
  objValue: 'objValue',
};

const boundedFunction = originalFunction.bind(obj);
// bind()를 통해 boundedFunction안의 this가 obj를 가르키게 됨

boundedFunction(1, 2); // a와 b전달
```

<br>

## ✨ bind를 사용해야하는 이유는 무엇일까?

- JS에서 클래스의 메서드는 기본적으로 바인딩되어 있지 않다. (함수 안에서의 `this` == `undefined`)
- 이벤트 핸들러 함수안에서 this가 컴포넌트를 가르키게 하려면 바인딩 해주어야 한다.

> 일반적으로 onClick={this.handleClick}과 같이 뒤에 ()를 사용하지 않고 메서드를 참조할 경우, 해당 메서드를 바인딩 해야 합니다.

<br>

## ✨ bind를 생략하는 방법은 없을까?

> **화살표 함수의 this 바인딩**
>
> JavaScript에서는 어떤 식별자(변수)를 찾을 때 현재 환경에서 그 변수가 없으면 바로 상위 환경을 검색합니다. 그렇게 점점 상위 환경으로 타고 타고 올라가다가 변수를 찾거나 가장 상위 환경에 도달하면 그만두게 되는 것이죠. 화살표 함수에서의 this 바인딩 방식도 이와 유사합니다. 화살표 함수에는 this라는 변수 자체가 존재하지 않기 때문에 그 상위 환경에서의 this를 참조하게 됩니다. - [참고](https://velog.io/@padoling/JavaScript-%ED%99%94%EC%82%B4%ED%91%9C-%ED%95%A8%EC%88%98%EC%99%80-this-%EB%B0%94%EC%9D%B8%EB%94%A9)

### 1. public class field 문법

```jsx
class LoggingButton extends React.Component {
  // 이 문법은 `this`가 handleClick 내에서 바인딩되도록 합니다.
  // 주의: 이 문법은 *실험적인* 문법입니다.
  handleClick = () => {
    console.log('this is:', this);
  };

  render() {
    return <button onClick={this.handleClick}>Click me</button>;
  }
}
```

### 2. 콜백에 화살표 함수를 사용

```jsx
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // 이 문법은 `this`가 handleClick 내에서 바인딩되도록 합니다.
    return <button onClick={() => this.handleClick()}>Click me</button>;
  }
}
```

- 이 문법의 문제점 : `LoggingButton`이 렌더링될 때마다 다른 콜백이 생성된다. (성능문제)
  - 성능문제를 피하고자, 생성자 안에서 바인딩하거나 public class field 문법을 사용하자.
