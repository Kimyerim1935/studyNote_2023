# 학습 키워드

- ReactRouter - RouterProvider

## ✔️ 키워드 정리

### ReactRouter - RouterProvider

React Router 버전 6.4부터 지원하는 라우터 객체를 만들어서 쓰는 방법은 다음과 같다.

```Javascript
// main.tsx
import 'reflect-metadata';
import ReactDOM from 'react-dom/client';

import App from './App';

function main() {
  const container = document.getElementById('root');
  if (!container) {
    return;
  }

  const root = ReactDOM.createRoot(container);
  root.render((
    <App />
  ));
}

main();
```

`main.tsx`에서 BrowserRouter를 빼주고
`App.tsx`도 수정해준다.

```Javascript
// App.tsx
import { createBrowserRouter, RouterProvider } from 'react-router-dom';
import routes from './routes';

const router = createBrowserRouter(routes);

export default function App() {
  return (
    <RouterProvider router={router} />
  );
}


// routes.tsx
import Home from './pages/Home';
import Order from './pages/Order';
import Complete from './pages/Complete';
import Layout from './components/Layout';

const routes = [
  {
    element: <Layout />,
    children: [
      {
        path: '/',
        element: <Home />,
      },
      {
        path: '/order',
        element: <Order />,
      },
      {
        path: '/order/complete',
        element: <Complete />,
      },
    ],
  },

];

export default routes;
```

router에 대한 테스트코드는 이렇게 작성하면 된다.

```Javascript
// router.test.tsx

import { screen, render } from '@testing-library/react';
import { createMemoryRouter } from 'react-router-dom';

import { RouterProvider } from 'react-router';
import routes from './routes';

const context = describe;

describe('App', () => {
  function renderRouter(path:string) {
    const router = createMemoryRouter(routes, { initialEntries: [path] });
    render(
      <RouterProvider router={router} />,
    );
  }

  context('when the current path is "/"', () => {
    it('renders the home page', () => {
      renderRouter('/');

      screen.getByText(/welcome/);
    });
  });

  context('when the current path is "/order"', () => {
    it('renders the order page', () => {
      renderRouter('/order');

      screen.getByText(/order/);
    });
  });

  context('when the current path is "/order/complete"', () => {
    it('renders the order complete page', () => {
      renderRouter('/order/complete');

      screen.getByText(/주문이 완료되었습니다!/);
    });
  });
});
```