# Ref

- react element 혹은 DOM 노드에 직접 접근하기 위한 방법
  - 일반적인 방법을 따르지 않고, 접근할 element를 참조하기 위해 달아두는 라벨같은 것
- 컴포넌트에서는 state를 조작해서 렌더링을 제어하는데, element 자체를 직접 수정하지는 않는다.
- 하지만 가끔 element에 직접 접근해서 수정해야하는 일이 생긴다. 그때 사용하는 것이 `Ref`
- 가능한 적게 사용하세요.

<br>

## ✨ Ref 사용하기

1. `React.createRef()`를 사용해 생성
2. 참조하려는 노드의 ref attr에 연결

```js
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }

  render() {
    return <div ref={this.myRef} />
  }

  ...

  const node = this.myRef.current; // 참조하기
```

<br>
<br>

## 참고

- 우테코 LMS - Ref
