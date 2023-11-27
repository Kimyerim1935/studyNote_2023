# 학습 키워드

- 라우터란?
- React Router
  - Browser Router
  - Route
  - Memory Router

## ✔️ 키워드 정리

### 라우터란?

[라우터](https://ko.wikipedia.org/wiki/%EB%9D%BC%EC%9A%B0%ED%84%B0)는 패킷의 위치를 추출하여, 그 위치에 대한 최적의 경로를 지정하며, 이 경로를 따라 데이터 패킷을 다음 장치로 전향시키는 장치라고 한다.

라우터는 이름 그대로 네트워크와 네트워크 간의 경로를 설정하고 가장 빠른길로 트래픽을 이끌어주는 네트워크 장비이다.

라우터의 기본적인 기능은 같지만 네트워크에서 쓰이는 위치나 규모에 따라 라우터의 종류가 달라질 수 있다.
라우터의 기능에 있어서 차이점은 처리할 수 있는 패킷, 트래픽 숫자에 따라서 이렇게 구분이 된다.

- 코어 라우터: 인터넷 서비스 제공자(ISP)의 랜이나 여러 개의 ISP 네트워크를 서로 연결한다.
- 센터 라우터: WAN 회선을 거쳐 회사의 본점과 회사의 지점을 서로 연결한다. 또, 인터넷 서비스 제공자와 기업의 네트워크와 연결할 때에도 쓰인다.
- 엣지 라우터: 지점, 영업소의 네트워크를 WAN 회선에 연결하여 회사의 본점의 라우터에 접근한다.
- 원격 라우터: 랜과 WANG을 중계한다. WAN 라우터라고도 부른다.
- 브로드밴드 라우터: 가정이나 작은 규모의 기업에서 브로드밴드급의 인터넷에 접속할 때 쓰인다.
- 핫스팟 라우터 : 휴대용 핫스팟에서 인터넷에 접속할 때 쓰인다.
- ISP 라우터 : 인터넷을 제공하는 제공자에 의해 접속할 때 쓰이는 라우터이다.

### React Router

리액트에서 가장 많이 쓰이는 [React Router](https://reactrouter.com/en/main)를 사용하려고 한다.

```Bash
npm i react-router-dom
```

명령어로 라이브러리를 설치해준다.

리액트 라우터는 사용자가 입력한 주소를 감지하는 역할을 하며, 여러 환경에서 동작할 수 있도록 여러 종류의 라우터 컴포넌트들을 제공한다.

#### Browser Router

`Browser Router`는 브라우저 주소 표시줄에 현재 위치를 저장하고 브라우저에 내장된 기록 스택을 사용하여 탐색한다.

이렇게 작성하면 된다.

```Javascript
// main.tsx

import * as React from "react";
import { createRoot } from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import App from './App';

const root = createRoot(document.getElementById("root"));

root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

URL의 특정 기본 이름 아래에서 실행되도록 애플리케이션을 구성한다.

```Javascript
// App.tsx
import { Routes, Route } from 'react-router-dom';
import Footer from './components/Footer';
import Header from './components/Header';
import Home from './pages/Home';
import Order from './pages/Order';

export default function App() {
  return (
    <div>
      <Header />
      <main>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/order" element={<Order />} />
        </Routes>
      </main>
      <Footer />
    </div>
  );
}
```

#### Route

경로는 [React Router](https://reactrouter.com/en/main/route/route) 앱에서 가장 중요한 부분이다. 경로 중첩을 통해 복잡한 애플리케이션 레이아웃과 데이터 종속성이 단순해지고 선언적으로 된다.

```Javascript
const router = createBrowserRouter([
  {
    // it renders this element
    element: <Team />,

    // when the URL matches this segment
    path: "teams/:teamId",

    // with this data loaded before rendering
    loader: async ({ request, params }) => {
      return fetch(
        `/fake/api/teams/${params.teamId}.json`,
        { signal: request.signal }
      );
    },

    // performing this mutation when data is submitted to it
    action: async ({ request }) => {
      return updateFakeTeam(await request.formData());
    },

    // and renders this element in case something went wrong
    errorElement: <ErrorBoundary />,
  },
]);
```
이런식으로 JSX를 사용하여 경로를 선언할 수도 있다.

경로 세그먼트가 `:`로 시작하면 동적 세그먼트가 된다. 주로 상세페이지에서 사용된다.

새그먼트 끝에 `?`를 추가하면 세그먼트를 선택사항으로 만들 수 있다.
쿼리스트링에서 사용된다.


#### Memory Router

테스트 코드 작성할 때 `MemoryRouter`를 사용한다.
`initialEntries`에다가 path를 추가해줘야한다.

```Javascript
// App.test.tsx
import { render } from '@testing-library/react';
import { MemoryRouter } from 'react-router-dom';

import App from './App';

const context = describe;

describe('App', () => {
  context('when the current path is "/"', () => {
    it('renders the home page', () => {
      render(
        <MemoryRouter initialEntries={['/']}>
          <App />
        </MemoryRouter>,
      );

      screen.getByText(/welcome/);
    });
  });

  context('when the current path is "/order"', () => {
    it('renders the home page', () => {
      render(
        <MemoryRouter initialEntries={['/order']}>
          <App />
        </MemoryRouter>,
      );

      screen.getByText(/order/);
    });
  });
});
```

## 참고

<https://information.koreainfoguide.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%9A%A9%EC%96%B4-%EB%9D%BC%EC%9A%B0%ED%84%B0%EB%9E%80-Router><br/>
