# Storybook

UI 컴포넌트를 외부 독립된 환경에서 개발하기 쉽게 도움을 주는 테스트 도구

## 특징

- 테스트 케이스라는 이름 대신 `스토리`라는 이름을 사용한다.
- 스토리 : 하나의 컴포넌트의 한 가지 상태를 표현
- 비즈니스 로직과 UI 컴포넌트를 독립적으로 분리하여 만들 수 있도록 도와준다.

## 설치

```
npx -p @storybook/cli sb init
```

## 예제

```js
import CheckBox from '.';

export default {
  title: 'Components/CheckBox', // 스토리북 사이드바에서 컴포넌트를 참조하는 방법
  component: CheckBox, // 해당 컴포넌트
};

const Template = args => <CheckBox {...args} />;

// export를 통해 storybook에게 문서화하고 있는 컴포넌트에 대해 알린다.
export const CheckBoxTemplate = Template.bind({});
/* Template.bind({}) : 함수의 복사본을 만드는 표준 js기법
 * 각각의 스토리가 고유한 속성을 갖지만, 동시에 동일한 구현을 사용하도록 할 수 있다.
 */

// 컴포넌트에 넘겨줄 props
CheckBoxTemplate.args = {
  checked: true,
  handleChange: () => {},
};
```

<br>
<br>

## ✨ [Addon](https://storybook.js.org/addons) - 유명한 것만!

![](https://storybook.js.org/a92861faee36b38eeb573b7ad50a4659/addon-locations.jpg)

```js
// main.js
  "addons": [
    "@storybook/addon-links", // 스토리 사이를 탐색하는 링크 생성
    "@storybook/addon-essentials", // 필수 addon 세트 (Controls, Actions ..)
    "@storybook/addon-interactions",
    "@storybook/preset-create-react-app"
  ],
```

<br>

### ⚡️ addon-essentials/[controls](https://storybook.js.org/docs/react/essentials/controls)

- [여러가지 controls](https://storybook.js.org/docs/react/essentials/controls#annotation)

디자이너와 개발자가 컴포넌트에 전달되는 값을 바꾸어보며 쉽게 컴포넌트의 행동을 살펴볼 수 있게 해준다.

- UI 문제점을 발견하는 일을 줄여준다. (글자를 아~주 많이 써본다던지 등)

```js
export default {
  title: 'Button',
  component: Button,
  argTypes: {
    variant: {
      // props 이름 - variant
      options: ['primary', 'secondary'],
      control: { type: 'radio' }, // control을 라디오 버튼으로 변경
    },
  },
};
```

![](https://storybook.js.org/608b8ade31cdaae67c23cf3ae8e0bd50/addon-controls-args-variant-optimized.png)

#### Matcher

```js
// preview.js or *.stories.jsx
export const parameters = {
  ...
  controls: {
    matchers: {
      color: /(background|color)$/i,
      date: /Date$/,
    },
  },
};
// 컨트롤이 정규식을 사용하여 자동으로 유추한다!
```

#### parameters

- control에 docs 표시

```js
// preview.js

export const parameters = {
  controls: { expanded: true },
};
```

- 특정 속성 컨트롤에서 제거해버리기

```js
// *.stories.jsx

// 테이블에서 없앰
export default {
  title: 'YourComponent',
  component: YourComponent,
  argTypes: {
    foo: {
      table: {
        disable: true,
      },
    },
  },
};

// 컨트롤 비활성화
export default {
  title: 'YourComponent',
  component: YourComponent,
  argTypes: {
    foo: {
      control: false,
    },
  },
};
```

<br>

### ⚡️ [addon-actions](https://storybook.js.org/docs/react/essentials/actions)

이벤트 핸들러가 수신한 데이터를 표시하는데 사용

```js
import CheckBox from '.';

export default {
  title: 'Components/CheckBox',
  component: CheckBox,
  argTypes: { handleChange: { action: 'change checkbox state' } },
};

const Template = args => {
  return <CheckBox {...args} />;
};

export const CheckBoxTemplate = Template.bind({});
CheckBoxTemplate.args = {
  checked: true,
};

// CheckBox.propTypes = {
//   checked: PropTypes.bool.isRequired,
//   handleChange: PropTypes.func.isRequired,
// };
```

```
change checkbox state: SyntheticBaseEvent {_reactName: "onChange", _targetInst: null, type: "change", nativeEvent: PointerEvent, target: HTMLInputElement…}
```

<br>

### ⚡️ [addon-links](https://storybook.js.org/addons/@storybook/addon-links/)

- 스토리에서 스토리로 이동

```js
import { linkTo } from '@storybook/addon-links';

linkTo('Toggle', 'off');
// 첫번째 매개변수 : 스토리 종류 이름
// 두번째 매개변수 : 스토리 이름
```

```js
import { linkTo } from '@storybook/addon-links';

export default {
  title: 'Button',
};

export const first = () => (
  <button onClick={linkTo('Button', 'second')}>Go to "Second"</button>
);
export const second = () => (
  <button onClick={linkTo('Button', 'first')}>Go to "First"</button>
);
```

<br>

### ⚡️ 액션 (Actions)

컴포넌트를 독립적으로 만들 때, 컴포넌트와의 상호작용을 확인하는데 도움, 함수와 state에 접근하지 못할 때 action() 사용

<br>
<br>
<br>

## ✨ `preview.js`

- css import
- parameters : 스토리북 기능과 애드온 동작을 제어하기 위해 사용
- 데코레이터(Decorators) : 스토리에 임의의 wrapper를 제공 (provider에서 스토리를 감싸줄 때)

```js
// import css
// import 'css/index.css'

import { BrowserRouter } from 'react-router-dom';
import { Provider } from 'react-redux';
import { ThemeProvider } from 'styled-components';

import { GlobalStyles, theme } from 'components';
import store from 'store/store';
import { doInitializeCart } from 'actions/actionCreator';
import { dummyProductList } from 'dummy_data';

// parameters
export const parameters = {
  actions: { argTypesRegex: '^on[A-Z].*' },
  controls: {
    matchers: {
      color: /(background|color)$/i,
      date: /Date$/,
    },
  },
};

// decorators
export const decorators = [
  (Story, context) => {
    store.dispatch(doInitializeCart({ products: dummyProductList }));

    return (
      <>
        <BrowserRouter>
          <GlobalStyles />
          <ThemeProvider theme={theme}>
            <Provider store={store}>
              <Story {...context} />
            </Provider>
          </ThemeProvider>
        </BrowserRouter>
      </>
    );
  },
];
```

<br>
<br>
<br>

### ✨ PropTypes

- 데이터 요구 사항 명시
- 자체적으로 문서화 가능

<br>
<br>
<br>

### ✨ 스토리에서 state 사용

```js
import { useState } from 'react';
import CheckBox from '.';

export default {
  title: 'Components/CheckBox',
  component: CheckBox,
  argTypes: {
    checked: { control: false },
  },
};

const Template = args => {
  const [checked, setChecked] = useState(true);

  return (
    <CheckBox
      {...args}
      checked={checked}
      handleChange={() => setChecked(prev => !prev)}
    />
  );
};

export const CheckBoxTemplate = Template.bind({});
CheckBoxTemplate.args = {};
```

<br>
<br>
<br>

## 참고

- [스토리북](https://storybook.js.org/docs/react/get-started/introduction)
