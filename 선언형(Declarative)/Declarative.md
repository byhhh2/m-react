# Declarative

> React는 선언적 API를 제공하기 때문에 갱신이 될 때마다 매번 무엇이 바뀌었는지를 걱정할 필요가 없습니다.

> #### 선언형
>
> React는 상호작용이 많은 UI를 만들 때 생기는 어려움을 줄여줍니다. 애플리케이션의 각 상태에 대한 **간단한 뷰만 설계하세요.** 그럼 React는 데이터가 변경됨에 따라 적절한 컴포넌트만 효율적으로 갱신하고 렌더링합니다.
>
> **선언형 뷰는 코드를 예측 가능하고 디버그하기 쉽게 만들어 줍니다.**

```
즉, 우리가 리액트에게 원하는 UI의 상태를 알려주면(선언적), 그 상태를 기반으로 DOM은 자동적으로 업데이트가 되는 것입니다.
```

- [출처](https://programming119.tistory.com/240)

<br>
<br>

## ✨ 특징

- 어떤 로직으로 어떻게 코드를 짜야 페이지가 그려질지에 대해 고민하지 않고, 컴포넌트나 데이터 등의 배치를 통해 무엇이 렌더링 될지 생각한다. (= 선언형 UI의 핵심)

<br>

## ✨ 명령형 vs 선언형

| 명령형                                         | 선언형                                                                                            |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| 명령형 코드는 결과를 얻기 위한 **과정**에 집중 | 어떤 **과정**으로 구현되는지 알 필요가 없으며 (절차를 신경쓸 필요가 없다.), 사용하고 싶을 때 선언 |
| ex) for                                        | ex) filter, map..등                                                                               |

<br>

## ✨ react가 선언형인 이유

- JSX의 캡슐화를 통해 선언형 코드 작성이 가능

```jsx
function App() {
  return (
    <Title />
    <Content />
  )
}

// Title과 Content는 JSX로 작성된 코드를 캡슐화한 컴포넌트
// Title과 Content의 세부사항을 알 필요없이 그저 배치를 통해 무엇이 렌더링될 지 생각할 수 있다.
```

- 아래의 코드는 동일한 화면을 렌더링한다. - [참고](https://egas.tistory.com/2)

```html
<!-- React ❌ -->

<ul id="”list”"></ul>

<script>
  var arr = [1, 2, 3, 4, 5];
  var elem = document.querySelector('#list');

  for (var i = 0; i < arr.length; i++) {
    var child = document.createElement('li');

    child.innerHTML = arr[i];
    elem.appendChild(child);
  }
</script>
```

```jsx
// React ⭕️

const arr = [1, 2, 3, 4, 5];

return (
  <ul>
    {arr.map(elem => (
      <li>{elem}</li>
    ))}
  </ul>
);
```

<br>
<br>

## 참고

- [react](https://ko.reactjs.org/)
- [react 공식문서 - 재조정](https://ko.reactjs.org/docs/reconciliation.html#gatsby-focus-wrapper)
- https://velog.io/@nemo/%EC%84%A0%EC%96%B8%ED%98%95-%EB%AA%85%EB%A0%B9%ED%98%95
