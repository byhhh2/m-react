# Life Cycle

## ✨ 생명주기 메서드

- 컴포넌트의 각각의 단계에서 실행되는 커스텀 기능
- 컴포넌트는 여러 종류의 생명주기 메서드를 가지고, 이 메서드를 오버라이딩하여 특정 시점에 실행되도록 설정할 수 있다.
- 컴포넌트가 만들어지고 DOM에 삽입될 때 (mounting), 컴포넌트가 업데이트될 때, DOM에서 마운트 해제(ummounted) • 제거될 때 사용할 수 있는 기능 제공

> **마운팅** : 컴포넌트가 처음 DOM에 렌더링 될 때  
> **언마운팅** : 컴포넌트에 의해 생성된 DOM이 삭제될 때

<br>
<br>

<img width="1023" alt="스크린샷 2022-06-28 오후 11 15 34" src="https://user-images.githubusercontent.com/52737532/176201455-77698a28-7ea3-461d-8847-5809b7cc8b8f.png">

## 1. Mount

- 아래 메서드들은 컴포넌트의 인스턴스가 생성되어 DOM상에 삽입될 때 순서대로 호출된다.

### 🔥 `constructor()`

- **마운트되기 전에 호출**
- 메서드를 바인딩하거나, state를 초기화하는 작업이 없다면 구현하지 않아도 된다.
- 구현하기 전에 `super(props)`를 호출해야 한다.
  - 그렇지 않으면 `this.props`가 생성자내에서 정의되지 않는다.
- `setState()`를 호출하면 안된다.
- `this.state`를 직접 할당할 수 있는 유일한 곳
- 부수효과를 발생시키거나 구독 작업을 수행하면 안된다.
- state에 props를 복사하면 안된다. (props값이 변하더라도 state에 반영되지 않으므로) props의 갱신을 의도적으로 무시해야할 때만 이와 같은 패턴을 사용하자.

### 🔥 `getDerivedStateFromProps()`

> getDerived : 파생되다.

- render() 메서드를 호출하기 직전에 호출
- 시간의 흐름에 따라 변하는 props가 state에 의존하는 드문예를 위해 존재한다.
- state를 갱신하기 위한 객체를 반환하거나 null을 반환하여 아무것도 갱신하지 않을 수 있다.

### 🔥 `render()`

- 클래스 컴포넌트에서 반드시 구현돼야 하는 유일한 메서드
- render가 반환해야하는 것
  - react element (보통 JSX를 사용하여 생성된다.)
  - 배열(여러개의 element)과 fragment(여러개의 자식 element를 그룹화)
  - portal (별도의 DOM 하위 트리에서 자식 element를 렌더링)
  - 문자열과 숫자 (DOM상의 텍스트 노드로서)
  - boolean 또는 null (아무것도 렌더링 하지 않는다. ex) `return true && <Child />` 패턴을 지원하는데에 사용됨)
- 순수하게 유지할 것 (브라우저와 상호작용 하지마라)
  - state를 변겅하지 않아야한다.
  - 호출될 때 마다 동일한 결과를 반환해야한다.
  - 브라우저와 직접적으로 상호작용 하지 않는다.

### 🔥 `componentDidMount()`

- **컴포넌트가 마운트된 직후, 즉 트리에 삽입된 직후 호출된다.**
- DOM 노드가 있어야 할 수 있는 초기화 작업은 이 메서드에서 하면 된다.
- 외부에서 데이터를 불러와야 한다면 네트워크 요청을 보내기 좋은 위치
- 데이터 구독을 설정하기 좋은 위치 (구독했다면 `componentWillUnmount()`에서 해제 작업을 해야한다.)

## 2. Update

- props 또는 state가 변경되면 갱신이 발생한다.
- 이 메서드들은 컴포넌트가 다시 렌더링될 때 순서대로 호출된다.

### 🔥 ~~getDerivedStateFromProps()~~

### 🔥 `shouldComponentUpdate()`

- 현재 state 또는 props의 변화가 컴포넌트의 출력결과에 영향을 미치는지 여부를 react가 알 수 있다.
- props 또는 state가 새로운 값으로 갱신되어서 렌더링이 발생하기 직전에 호출된다.
- 기본값은 true를 반환한다. (기본 동작으로 매 state 변화마다 다시 렌더링을 수행)
- 성능 최적화만을 위한 메서드
- 직접 작성대신 PureComponent를 사용하는 것이 좋다.
  - PureComponent : PureComponent는 props와 state에 대하여 얕은 비교를 수행하고, 해야 할 갱신 작업을 건너뛸 확률을 낮춥니다.

### 🔥 ~~render()~~

### 🔥 `getSnapshotBeforeUpdate()`

- 렌더링된 결과가 DOM 등에 반영되기 전에 호출된다.
- 이 메서드를 사용하면 DOM으로부터 스크롤 위치 등과 같은 정보를 DOM에 렌더링 결과가 반영되기 전에 얻을 수 있다. (채팅 화면처럼 스크롤 위치를 따로 처리하는 작업이 필요한 UI 등)
- 여기서 반환되는 값은 `componentDidUpdate()`에 인자로 전달
- 스냅샷 값을 반환하거나 null을 반환한다.

### 🔥 `componentDidUpdate()`

- 갱신이 일어난 직후에 호출된다.
- 최초 렌더링 시에는 호출되지 않는다.
- 컴포넌트가 갱신되었을 때 DOM을 조작하기 위해 활용하면 좋다. 이전과 현재 props를 비교하여 네트워크 요청을 보내는 작업도 여기서하면 된다.
- `setState()`를 호출할 수는 있지만 조건문이 있지 않다면 무한 반복이 발생할 수 있다.

```jsx
componentDidUpdate(prevProps) {
  // 전형적인 사용 사례 (props 비교를 잊지 마세요)
  if (this.props.userID !== prevProps.userID) {
    this.fetchData(this.props.userID);
  }
}
```

## 3. Unmount

### 🔥 `componentWillUnmount()`

- 컴포넌트가 마운트 해제되어 제거되기 직전에 호출된다.
- 구독 해제 등 필요한 모든 정리 작업을 수행하자.
- 컴포넌트는 다시 렌더링될 일이 없으므로 setState()를 호출하면 안된다.

## 참고

- [react 공식문서 - 생명주기 메서드](https://ko.reactjs.org/docs/glossary.html#lifecycle-methods)
- [react 공식문서 - React.Component](https://ko.reactjs.org/docs/react-component.html)
