# 학습 키워드

- HTML DOM API
  - Location
  - pathname

## ✔️ 키워드 정리

### HTML DOM API

[참고](https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API#html_dom_api_interfaces)

흔히 우리가 HTML에서 제어하는 div, span, input 등의 요소들을 (DOM)Document Object Modal이라고 한다.

프로그램을 사용하기 위한 명령들의 집합을 (API)Application Programming Interface라고 한다.

즉, DOM API는 HTML의 요소들을 JS에서 제어하기 위한 명령들의 집합을 의미한다.

```Javascript
  const nameField = document.getElementById("userName");
  const sendButton = document.getElementById("sendButton");

  sendButton.disabled = true;
  nameField.focus();

  nameField.addEventListener("input", (event) => {
    const elem = event.target;
    const valid = elem.value.length !== 0;

    if (valid && sendButton.disabled) {
      sendButton.disabled = false;
    } else if (!valid && !sendButton.disabled) {
      sendButton.disabled = true;
    }
  });

```

이 코드는 Document 인터페이스의 `getElementById()`메서드를 사용하여, ID가 'userName'과 'sendButton'인 요소를 나타내는 DOM 객체를 가져온다.
이를 통해 이러한 요소에 대한 정보를 제공하고 제어 권한을 부여하는 속성과 메서드에 접근할 수 있다.

#### Location

[Location](https://developer.mozilla.org/ko/docs/Web/API/Location) 인터페이스는 객체가 연결된 장소(URL)을 표현한다. `Location` 인터페이스에 변경을 가하면 연결된 객체에도 반영이 되는데 `Document`와 `Window`인터페이스가 이런 `Location`을 갖고 있다.

이렇게 사용하면 된다.

```Javascript
export default function App(){
  const path = window.location.pathname;

  return (
    <p>
     {path === '/' && <Home />}
     {path === '/about' && <About />}
    </p>
  )
}
```

#### pathname

URL인터페이스의 `pathName` 속성은 URL의 경로와 그 앞에 /로 이루어진 usvString을 반환한다.
경로가 없는 경우에는 빈 문자열을 반환한다.

사용 예시는 이렇다.

```Javascript
import Footer from './components/Footer';
import Header from './components/Header';
import Home from './pages/Home';
import Order from './pages/Order';

const pages: Record<string, React.FC> = {
  '/': Home,
  '/order': Order,
};

export default function App() {
  const path = window.location.pathname;
  const Page = pages[path] || Home;
  // const Page = Reflect.get(pages, path) || Home; <= 이렇게 사용해도 됨

  return (
    <div>
      <Header />
      <main>
        <Page />
      </main>
      <Footer />
    </div>
  );
}

```

## 참고

<https://developer.mozilla.org/ko/docs/Web/API/URL/pathname><br/>
<https://developer.mozilla.org/en-US/docs/Web/API/Location/pathname>