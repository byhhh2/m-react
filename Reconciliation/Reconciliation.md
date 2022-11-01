# Reconciliation - 재조정

- prev V-DOM과 cur V-DOM를 비교하여 변경된 부분을 real DOM에 반영하는 과정
- 이때 react는 방금 만들어진 트리에 맞게 가장 효과적으로 UI를 갱신할 방법을 알아낼 필요가 있었다.
- 최첨단 알고리즘도 `o(n³)`의 복잡도를 가진다. -> 이는 너무 비싼 연산. 이를 해결하기 위해 react는 두 가지 **가정**을 기반해, `o(n)`복잡도의 휴리스틱(간편추론의 방법) 알고리즘을 구현
  1. 서로 다른 type의 두 element는 서로 다른 트리를 만든다.
  2. 개발자는 key를 통해 여러 렌더링 사이에 어떤 자식 element가 변경되지 않아야 할 지 표시해줄 수 있다.

<br>

## ✨ 트리 비교

- 두 개의 트리를 비교할 때 react는 **루트 element**부터 비교한다. 이때 루트 element의 type에 따라 동작이 달라진다.

### 🔥 루트 element 처리

> 루트 element의 type이 다른 경우 react는 이전 트리를 버리고 완전히 새로운 트리를 구축한다.  
> **설명** : HTML 태그마다 자기만의 규칙이 있어, 자식 태그가 한정적이다. 만약 `<ul>`이나 `<ol>`태그라면 바로 밑에는 `<li>`태그만 담기게 되고, 갑자기 `<img>`나 `<iframe>`이 담길 일은 없다. 만약 `<div>`가 `<span>`으로 바뀌어 자식이 그대로라고 해도, `display: block`이 무너지기 때문에 어차피 렌더링 결과물은 달라진다. 즉, 부모 태그의 타입이 바뀌는 순간 자식을 굳이 탐색할 필요없이 버리고 새로 렌더링 해버리는 편이 더 효율적이다.
>
> ex) `<a>` -> `<img>`

- 트리를 버릴 때 이전 DOM 노드들은 모두 파괴된다 (`componentWillUnmount()`가 실행)
- 새로운 트리가 만들어질 때, 새로운 DOM 노드들이 DOM에 삽입됨 (`UNSAFE_componentWillMount()`실행 -> `componentDidMount()` 실행)
- 이전 트리와 연관된 모든 state는 사라진다.

```jsx
<div ➡️ span>
  <Counter /> {/* Counter 컴포넌트는 사라지고 새로 mount된다. */}
</div ➡️ span>
```

<br>

> 루트 element의 type이 같은 경우 react는 동일한 내역은 유지하고 변경된 속성들만 갱신한다.  
> **설명** : 이게 가능한 이유는 react가 virtual DOM을 조작하기 때문이다. virtual DOM은 실제 DOM을 생성할 때 필요한 정보들을 담은 객체이기 때문에 업데이트할 내용이 생기면 virtual DOM 내부의 프로퍼티만 수정한 후, 모든 노드의 업데이트가 끝나면 실제 DOM을 렌더링하면 되기 때문이다.
>
> ex)
>
> ```jsx
>  <div className="before" title="stuff" />
>  <div className="after" title="stuff" />
> ```
>
> _className만 수정한다._  
> 만약 style 속성이 변경된다면 바뀐 스타일만 변경한다. (`color`가 바뀌었다면 바뀌지 않은 `fontWeight`는 갱신하지 않고 `color`만 갱신한다.)

- 컴포넌트의 인스턴스는 동일하게 유지되어 렌더링간 state가 유지된다. (`UNSAFE_componentWillReceiveProps()`, `UNSAFE_componentWillUpdate()`, `componentDidUpdate()`를 호출)

<br>

### 🔥 자식에 대한 재귀적 처리

- 동시에 두 리스트(이전, 현재)를 순회하고 차이점이 있으면 변경을 생성한다.

```jsx
<ul>
  <li>first</li> {/* 1 */}
  <li>second</li> {/* 2 */}
</ul>

<ul>
  <li>first</li> {/* 1 */}
  <li>second</li> {/* 2 */}
  <li>third</li> {/* 3 */}
</ul>
```

1. 일치 확인
2. 일치 확인
3. 변경 확인 -> 트리에 추가

- 그런데 이렇게 구현하면 **리스트 맨 앞에 element를 추가할 때 성능이 좋지 않다.**

```jsx
<ul>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

<ul>
  <li>Connecticut</li> {/* 얘를 앞으로 땡겨야 하니깐 모든 자식을 변경해야 한다. */}
  <li>Duke</li>
  <li>Villanova</li>
</ul>
```

- 이를 해결하기 위해 `key`!를 사용

### 🔥 `key`

- react는 key를 통해 기존 트리와 이후 트리의 자식들이 일치하는지 확인한다.

```jsx
<ul>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>

<ul>
  <li key="2014">Connecticut</li>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>

```

- _2014는 추가되었고, 2015와 2016은 그저 이동만 하면 된다._
- `key`는 오로지 형제 사이에서만 유일하면 된다.
- index를 key로 사용중이라면 배열이 재배열될 때 문제가 될 수 있다. (항목의 순서가 바뀔 때 key또한 바뀌므로)

<br>
<br>

## 참고

- [react 공식문서 - 재조정](https://ko.reactjs.org/docs/reconciliation.html)
- https://www.huskyhoochu.com/virtual-dom/
