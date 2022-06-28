## 문제

- `Input`과 `Form` 핸들링
  - HTML element 중 자체적으로 data를 가지는 element
  - 모든 데이터를 한 곳에서 제어하자라는 리액트의 설계 원칙을 위배

<br>

## Controlled Component VS Uncontrolled Component

### Controlled Component

- react에 의해 값이 완전히 제어
- state를 value로 설정하고 value 핸들링을 `setState()`로 한다.
- input에 들어온 데이터를 state로 저장하고, state기반으로 element를 리렌더링
- state가 input의 change이벤트가 발생하는 동시에 갱신된다. (= 실시간 처리가 가능)

```js
// input의 값은 항상 React state의 값
<input value={value} onChange={handleChange} />
```

### Uncontrolled Component

- DOM 자체에서 데이터가 다루어진다.
- `ref`를 사용해서 DOM의 데이터를 가져온다. (`ref`를 사용해서 input의 value를 **참조**한다.)
- 컴포넌트에서 실시간으로 input data를 관리하는 것이 아니기 때문에 실시간 처리가 불가능하다. (submit되었을 때 `this.ref.current.value`를 가져오는 식)

```js
<input value={value} onChange={handleChange} ref={inputRef} />
```

<br>

## 참고

- 우아한테크코스 LMS - Controlled & Uncontrolled Components
- https://velog.io/@dolarge/React-Controlled-Componenet-vs-Unconterolled-Componenet
