# 학습 키워드

- Reset CSS
- `box-sizing` 속성
- `word-break` 속성
- Theme
- ThemeProvider

## ✔️ 키워드 정리

### Reset CSS

`npm i styled-reset` 명령어로 설치한 다음, `App.tsx` 파일이나 `main.tsx`파일에 컴포넌트로 사용하면 된다.

```Javascript
import { Reset } from 'styled-reset';

export default function App() {
  return (
    <div>
      <Reset />
    </div>
  )}
```

그 다음, `GlobalStyle.ts` 파일을 생성해서 이 내용을 추가해주면 된다.

```Javascript
// GlobalStyle.ts
import { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
  html {
    box-sizing: border-box;
  }

  *,
  *::before,
  *::after {
    box-sizing: inherit;
  }

  html {
    font-size: 62.5%;
  }

  body {
    font-size: 1.6rem;
  }

  :lang(ko) {
    h1, h2, h3 {
      word-break: keep-all;
    }
  }
`;

export default GlobalStyle;
```

### `box-sizing` 속성

이 속성은 box의 크기를 어떤 것을 기준으로 계산할 지 정하는 속성이다.

기본 값은 content-box 이며, 자주 사용하는 속성은 border-box이다.

box-sizing: content-box | border-box | initial | inherit

- content-box : 콘텐트 영역을 기준으로 크기를 정한다.
- border-box : 테두리를 기준으로 크기를 정한다.
- initial : 기본값으로 설정한다.
- inherit : 부모 요소의 속성값을 상속받는다.

### `word-break` 속성

텍스트가 컨텐츠 상자를 넘칠 경우에 줄 바꿈을 표시할지 여부를 설정한다.

- normal
기본 줄 바꿈 규칙을 사용합니다.

- break-all
오버플로를 방지하려면 두 문자 사이에 단어 분리를 삽입해야 합니다(중국어/일본어/한국어 텍스트 제외).

- keep-all
중국어/일본어/한국어(CJK) 텍스트에는 단어 나누기를 사용하면 안 됩니다. CJK가 아닌 텍스트 동작은 와 동일합니다 normal.

- break-word 더 이상 사용되지 않음
속성의 실제 가치에 관계없이 overflow-wrap: anywhere와 결합된 것과 동일한 효과가 있습니다.

### Theme

다크모드나 색상 관련해서 코드를 작성할 때 편리해진다.

기본 Theme부터 정의하고,

```Javascript
const defaultTheme = {
  colors: {
    background: 'linear-gradient(134deg, #F89E21 0.7%, #FF6400 65.66%)',
    text: '#FFF',
    primary: '#FF8400',
    primaryOp: '#FFF1DC',
    secondary: '#442728',
    menuBg: '#fff',
    gray: '#F4F4F4',
    activeBtn: '#D87000',
    activeCancelBtn: '#170A0C',
  },
};

export default defaultTheme;
```

darkMode도 사용할 예정이라서 darkTheme도 정의해줬다.

```Javascript
import Theme from './Theme';

const darkTheme : Theme = {
  colors: {
    background: '#1E1E1E',
    text: '#FFF',
    primary: '#FF8400',
    primaryOp: '#3A3A3A',
    secondary: '#442728',
    menuBg: '#3A3A3A',
    gray: '#1E1E1E',
    activeBtn: '#D87000',
    activeCancelBtn: '#170A0C',
  },
};

export default darkTheme;
```

타입 문제를 해결하기 위해 styled.d.ts 파일을 작성했다.

```Javascript
import 'styled-components';
import Theme from './Theme';

declare module 'styled-components' {
	export interface DefaultTheme extends Theme {}
}
```

마지막으로 `GlobalStyle.ts` 파일을 작성하면 끝이다.

```Javascript
import { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
  body {
    background: ${(props) => props.theme.colors.background};
    color: ${(props) => props.theme.colors.text};
  }

  a {
    color: ${(props) => props.theme.colors.text};
  }

  button,
  input,
  select,
  textarea {
   background: ${(props) => props.theme.colors.background};
   color: ${(props) => props.theme.colors.text};
  }
`;

export default GlobalStyle;
```

### ThemeProvider

생성한 theme을 기준으로 컴포넌트에 변화를 주고 싶다면 최상위 컴포넌트에서 ThemeProvider로 감싸줘야한다.

```Javascript
// App.tsx
import { ThemeProvider } from 'styled-components';
import defaultTheme from './styles/defaultTheme';

export default function App() {
  const { isDarkMode } = useDarkMode();
  const theme = isDarkMode ? darkTheme : defaultTheme;

  return (
     <ThemeProvider theme={theme}>
      <Reset />
      ...
     </ThemeProvider>
  )
}
```

이렇게 사용하면 된다.