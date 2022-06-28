# Props

- props는 `읽기 전용`이다.

## 컴포넌트에서 자체 props를 수정해서는 안된다.

```jsx
// 순수함수 ⭕️

function sum(a, b) {
  return a + b;
}
```

- 순수함수
- 입력값을 바꾸려하지 않고, 항상 동일한 입력값에 대해 동일한 결과 반환

```jsx
// 순수함수 ❌

function withdraw(account, amount) {
  account.total -= amount;
}
```

- 순수함수가 아니다.
- 위 함수는 자신의 입력값을 변경하기 때문에 순수함수가 아니다.
- 변경을 위한 값은 state를 사용할 것

> 모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 합니다.

<br>
<br>

## 참고

- [react 공식문서 - props는 읽기 전용입니다.](https://ko.reactjs.org/docs/components-and-props.html#props-are-read-only)
