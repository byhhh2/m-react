# Virtual DOM

- 리액트에서는 사용자 인터페이스를 나타내는 객체
- Virtual DOM은 가상적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 실제 DOM과 동기화하는 프로그래밍 개념입니다. (=재조정)
  - 선언적 API를 가능하게 하는 접근 방식
- React에게 원하는 UI의 상태를 알려주면 DOM이 그 상태와 일치하도록 한다.
- DOM을 추상화한 가상의 객체 (사본)

> ### React Fiber
>
> 재조정 엔진  
> 증분 렌더링 활성화

<br>

## ✨ Real DOM

- 작성된 HTML 문서가 **브라우저에 의해 해석되어 실제 문서를 나타내는 노드 트리** - [참고](https://www.howdy-mj.me/dom/what-is-dom/)
- DOM은 JS를 통해 document에 노드를 추가•삭제•변경•이벤트처리 등을 가능하게 하는 API를 제공
- HTML은 단순한 문자열일뿐이며, 브라우저가 이해하기 위해서는 노드(객체)로 변환해야한다.
- DOM은 HTML과 JS를 이어주는 공간, 작성한 HTML을 JS가 이해할 수 있도록 객체로 변환하는 것
- 자바스크립트 = DOM API

<br>

## ✨ Real DOM에 직접 접근하는 것에 대한 문제

- 사소한 부분을 수정하더라도 다시 HTML, CSS를 파싱해서 DOM 트리를 만들어야 한다. -> 비효율을 해결하기 위해 등장한 것이 virtual DOM
  - DOM이 변경되면서 여러번 렌더링 되는 것이 문제
- SPA가 등장하면서 DOM 복잡도가 증가하고 유지보수가 어려워짐

<br>

## ✨ 특징

- 수정사항이 여러개이더라도, virtual DOM은 한번만 렌더링을 일으킨다.
- 수정사항을 바로 DOM에 적용하는 것이 아니라 중간단계로 virtual DOM을 수정하고 virtual DOM을 통해 DOM을 수정
- 추상화 : DOM을 직접적으로 제어하는 API를 호출하지 않고 react같은 프레임워크가 virtual DOM을 통해 DOM 관리를 할 수 있도록 함.

<br>

## ✨ 예시

1. real DOM 조작 : `<ul>`태그 안에 `<li>`가 10개 존재하고, 각 `<li>`에 변경사항이 존재한다면 DOM에 접근하여 `<li>`를 10번 변경한다. 즉 렌더링이 10번 발생
2. virtual DOM : virtual DOM에서 `<li>`태그를 10번 변경하고 real DOM과 virtual DOM을 비교하여 변경된 부분인 `<ul>` 태그만 통채로 1번 변경한다. 즉 렌더링이 1번 발생

<br>

## ✨ react에서 DOM을 업데이트 시키는 절차

1. 데이터에 변경이 있으면 전체 UI를 virtual DOM에 re-render
2. 이전 virtual DOM과 변경된 virtual DOM을 비교
3. 변경된 부분만 실제 DOM에 반영

<br>
<br>

## 참고

- [react 공식문서 virtual DOM](https://ko.reactjs.org/docs/faq-internals.html#what-is-the-virtual-dom)
- https://www.howdy-mj.me/dom/what-is-dom/
- https://jeong-pro.tistory.com/210
- https://dev-cini.tistory.com/11
