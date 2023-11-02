# 학습 키워드

- React에서 JSX를 사용하는 목적
- Syntactic sugar
- React.createElement
- React Element
- React StrictMode
- VDOM(Virtual DOM)이란?
    - DOM이란?
    - DOM과 Virtual DOM의 차이
- Reconciliation(재조정) 과정은 무엇인가?

## ✔️ 키워드 정리

### React에서 JSX를 사용하는 목적

JSX란?
Javascript XML의 약자로 자바스크립트에 XML을 추가한 확장 문법이다.
React에서는 본질적으로 렌더링 로직이 UI로직과 연결된다.

컴포넌트 단위로 쪼개서 처리하는 React의 특성을 고려해보면 JSX를 사용하는것이 가독성 측면에서 훨씬 유리해서 사용을 지향하는 것 같다.

### Syntactic sugar

Syntactic sugar는 사람이 이해하기 쉽게 디자인된 프로그래밍 언어 문법이다. 사용하고자하는 프로그래밍 언어를 더욱 더 간결하고 명확하게 표현할 수 있도록 도와주는 역할을 한다.

React에서 JSX는 Syntactic sugar 역할을 한다!

### React.createElement

리액트는 `React.createElement(type, [props], [...children])`리는 API를 통해 컴포넌트를 생성한다.

```Javascript
<button type="submit" onClick={handleClick}>등록</button>
```

이 코드가 이렇게 변환된다.

```Javascript
React.createElement("button",
 {
    type: "submit",
    onClick: "handleClick"
 }, "등록");
```

### React Element

Element는 리액트 앱의 가장 작은 단위이다. 엘리먼트는 화면에 표시할 내용을 기술한다.

### React StrictMode

기존에 자바스크립트에서 strict mode는 코드에 주로 `'use strict'`를 선언하여 사용한다.

반면 리액트에서는

```Javascript
<React.StrictMode>
    ...
</React.StrictMode>
```

이렇게 사용할 수 있다.

React.StrictMode는 이러한 부분에서 도움이 된다.

- 안전하지 않은 생명주기를 가진 컴포넌트
- 레거시 문자열 사용에 대한 경고
- 권장되지 않는 findDOMNode 사용에 대한 경고
- 예상하지 못한 부작용 검사
- 레거시 context API 검사

### VDOM(Virtual DOM)이란?

수정사항이 여러가지가 있더라도, 실제 DOM과 비교해서 가상 DOM은 한 번만 렌더링을 일으킨다.


#### DOM이란?

작성된 HTML element들을 tree 형태로 표현한 것이다.

HTML과 자바스크립트를 이어주는 공간으로, 내가 작성한 HTML 소스를 자바스크립트가 이해할 수 있도록 객체로 변환해주는 것이다.

#### DOM과 Virtual DOM의 차이

DOM은 element의 노드가 추가되면 전체 문서가 갱신되지만, Virtual DOM은 변경점만 DOM에 적용하기 때문에 전체 문서가 갱신되지 않는다.

어떠한 element를 찾을 때, DOM은 querySelector 등의 메소드를 사용하여 찾는 반면에 Virtual DOM은 ref로 element를 찾는다.

### Reconciliation(재조정) 과정은 무엇인가?

state나 props가 갱신되면 render() 함수는 새로운 React 엘리먼트 트리를 반환한다.

React는 두 가지의 가정을 기반하여 O(n) 복잡도의 휴리스틱 알고리즘을 구현했다.
1. 서로 다른 타입의 두 엘리먼트는 서로 다른 트리를 만들어낸다.
2. 개발자가 key prop을 통해, 여러 렌더링 사이에서 어떤 자식의 엘리먼트가 변경되지 않아야할 지 표시해줄 수 있다.

엘리먼트의 타입이 다른 경우에 두 루트 엘리먼트의 타입이 다르면, React는 이전의 트리를 버리고 완전히 새로운 트리를 구축한다.
트리를 버릴 때 이전 DOM 노드들은 모두 파괴된다.

엘리먼트의 타입이 같은 경우에는 두 엘리먼트의 속성을 확인하여 동일한 내역은 유지 하고 변경된 부분들의 속성들만 갱신한다.

### 참고

- <https://seokzin.tistory.com/entry/React-%EC%97%98%EB%A6%AC%EB%A8%BC%ED%8A%B8%EC%99%80-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-Element-Component-JSX><br/>
- <https://gimdam.tistory.com/entry/%EB%A6%AC%EC%95%A1%ED%8A%B8-%EC%8B%9C%EC%9E%91-03-Hello-World><br/>
- https://programming119.tistory.com/240