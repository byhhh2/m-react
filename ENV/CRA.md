# CRA

## 설명

- Create React App의 약자
- 빌드 도구가 아닌 코드에 집중할 수 있다.
- 개발 환경을 설정하고, 최신 JS를 사용하게 해주며, 좋은 개발환경과 프로덕션 앱 최적화를 해준다.
- 리액트 프로젝트를 쉽게 만들 수 있게 필요한 설정을 도와주고 필요한 모듈을 가져와줌.
- 프론트앤드 빌드 파이프라인만 생성
- 내부적으로 webpack, babel, ESLint 등을 사용한다. (즉, 구성할 필요가 없다. 코드에 집중할 수 있도록 미리 구성해놓은 것)
- 필요할 경우 `eject`를 통해서 구성을 변경할 수 있다.

<br>

> Boilerplate란? - [참고1](https://charlezz.medium.com/%EB%B3%B4%EC%9D%BC%EB%9F%AC%ED%94%8C%EB%A0%88%EC%9D%B4%ED%8A%B8-%EC%BD%94%EB%93%9C%EB%9E%80-boilerplate-code-83009a8d3297), [참고2](https://coding-grandpa.tistory.com/2)
>
> - 최소한의 변경으로 여러곳에서 재사용되며, 반복적으로 비슷한 형태를 띄는 코드 (별 수정 없이 반복적으로 사용되는 코드)
> - 모든 코드를 작성하기 위해 항상 필요한 부분 - "묻지도 따지지도 않고 따라 적는 코드"
> - 매번 프로그래밍을 할 때마다 Boilerplate 코드를 작성하는 것은 비효율적
>
> CRA == BiolerPlate?
>
> - 페이스북에서 만든 react 프로젝트용 Boilerplate
> - app을 생성해주고 설정해주는 변하지 않는 코드들이 존재하고 여러 곳에서 사용된다.
> - **지속적으로 패키지들이 버전이 업되고, 리액트도 마찬가지로 버전이 업되므로 프로젝트만의 보일러플레이트를 갖고 있다고 해도 패지키들의 버전업에 맞추어 지속적으로 관리해주어야 한다. 하지만 CRA를 사용하면 리액트의 지속적인 업데이트를 페이스북이 해주고 이에 맞추어 CRA도 업데이트 시켜준다.**

<br>

## ✨ 사용

```
npx create-react-app <project-name>
```

<br>

## ✨ What’s Included?

- React, JSX, ES6, TypeScript and Flow 문법 지원
- ES6 이외의 추가 언어
- 대화형 단위 테스트 러너
- 라이브 개발 서버
- JS, CSS, image를 해시, 소스맵과 함께 번들로 제공하는 빌드 스크립트
- service worker, web app menifest

<br>

## ✨ build

- babel이나 webpack 같은 build 도구를 사용 • 설정하지 않고도 react app이 동작한다. (build configuration이 필요없다.)
- production을 배포할 준비가 되었을 때 `npm run build`를 실행하면 build폴더 안에 최적하된 앱의 build를 생성한다.

<br>

## ✨ dependency

- create react app은 하나의 빌드 종속성만 필요하다. 모든 요소가 버전 불일치 없이 원활하게 작동하는지 확인한다.

<br>

## 참고

- [create-react-app](https://create-react-app.dev/)
- [create-react-app/repository](https://github.com/facebook/create-react-app)
- [react 공식문서 - create react app](https://ko.reactjs.org/docs/create-a-new-react-app.html#create-react-app)
- https://fe-churi.tistory.com/33
