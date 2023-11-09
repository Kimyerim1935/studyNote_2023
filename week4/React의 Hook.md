# 학습 키워드

- React Hook 이란
- Hooks

    - useState
    - useEffect
    - useContext
    - useRef
    - useLayoutEffect
- React StrictMode 란

## ✔️ 키워드 정리

### React Hook 이란

[Hook](https://ko.legacy.reactjs.org/docs/hooks-intro.html)은 React 버전 16.8부터 새로 추가됐다.
함수형 컴포넌트에서도 상태 관리를 할 수 있는 `useState` , 렌더링 이후에 실행할 작업을 관리할 수 있는 `useEffect`  그리고 리액트에서 Context를 좀 더 편하게 사용할 수 있는 `useContext` 가 대표적인 Hook이다.

Hook은 다음과 같은 특징을 갖고 있다.

- 선택적 사용: 기존의 코드를 다시 작성할 필요 없이 사용하고자 하는 컴포넌트들 안에서 Hook을 사용할 수 있다.
- 이전 버전과의 호환성: Hook은 호환성을 깨트리는 변화가 없다.

Hook은 계층의 변화 없이 상태 관련 로직을 재사용할 수 있도록 도와준다.
이러한 특징은 많은 컴포넌트에서 Hook을 공유하기 쉽게 만들어준다는 장점이 있다.
그리고 복잡한 요소들은 전부 Hook으로 격리시키거나 재사용할 수 있다.

### Hooks

React에서는 다양한 Hook들을 갖고 있다.
상황에 맞춰 알맞게 사용하면 훨씬 편리하게 React를 사용할 수 있다.

#### useState

컴포넌트에서 관리하는 동적인 값을 `state`라고 부른다.

```Javascript
const [value, setValue] = useState();
```

이 코드에서 `value`는 현재 상태, `setValue`는 Setter 함수이다.
제일 많이 쓰이는 Hook이라고 할 수 있다.

class 컴포넌트의 setState 메서드와 달리, useState의 Setter 함수는 상태가 갱신되는 객체를 자동으로 합치지는 않는다.

React는 Object.is() 비교 알고리즘을 사용하여 State Hook을 현재의 state와 동일한 값으로 갱신하는 경우 실행하지 않고 처리를 종료한다.

#### useEffect

[useEffect Hook](https://ko.legacy.reactjs.org/docs/hooks-effect.html)은 DOM 업데이트를 한 이후에 수행해야 할 작업에 대해 지정할 때 주로 사용한다.

useEffect는 화면이 렌더링 된 이후에 최초로 한 번 실행되고, 이후 상태가 변경될 때마다 계속 실행된다.

함수를 리턴할 수 있어서 종료처리도 가능한 Hook이다.
useEffect에서 반환한 함수는 리액트에서 해당 컴포넌트가 마운트 해제될 때 호출한다고 한다.

useEffect 사용 예시는 이렇다.

```Javascript
useEffect(()=> {
    ...
})
```

하지만 의존성 배열이 없으면 매번 렌더링할 때마다 실행이 되기 때문에 딱 한 번 실행하고 싶은 코드에는 의존성 배열을 추가해준다.

```Javascript
useEffect(()=> {
    ...
}, []) // []의존성 배열 추가
```

특정 변수의 상태가 변경될 때 useEffect를 실행하고 싶으면 의존성 배열 안에다가 변수를 넣어주면 된다.


#### useContext

```Javascript
const value = useContext(MyContext);
```

`context` 객체(React.createContext에서 반환된 값)을 받아 해당 `context`의 현재 값을 반환한다. `context`의 현재 값은 트리 안에서 이 Hook을 호출하는 컴포넌트에 <MyContext.Provider>의  `value` prop에 의해 결정된다.


<MyContext.Provider>가 갱신되면 이 Hook은 가장 최신의 context `value`를 사용하여 렌더러를 트리거 한다.
상위 컴포넌트에서 React.memo 또는  shouldComponentUpdate를 사용하더라도 `useContext`를 사용하고 있는 컴포넌트 자체에서부터 다시 렌더링 한다.

context값이 변경될 때마다 리렌더링 되기 때문에 메모이제이션을 사용하여 최적화 할 수 있다고 한다.

#### useRef

Ref를 사용해야할 때는 다음과 같다.

- 포커스, 텍스트 선택 영역, 미디어의 재생을 관리할 때
- 애니메이션을 직접적으로 실행시킬때
- 서드파티 DOM 라이브러리를 React와 같이 사용할 때

선언적으로 해결될 수 있는 문제에서는 Ref의 사용을 <b>지양</b>해야한다.

#### useLayoutEffect

[useLayoutEffect](https://react.dev/reference/react/useLayoutEffect)는 `useEffect` 브라우저가 화면을 다시 렌더링하기 전에 실행되는 버전이다.
사용법은 `useEffect`와 `useLayoutEffect`가 동일하다.

컴포넌트들이 렌더된 후 실행되며, 그 이후에 paint 되는데 useLayoutEffect는 paint가 되기 전에 실행되기 때문에 DOM을 조작하는 코드가 있더라도 사용자는 깜빡임을 경험하지 않는다.

하지만 공식 문서에서는 `useLayoutEffect`의 성능이 저하될 수 있어서 가능하면 `useEffect`를 사용하라고 권한다.
`useLayoutEffect`에 예약된 모든 상태 업데이트는 브라우저가 화면을 다시 그리는것을 차단하기 때문에 과도하게 사용하면 속도가 느려지기 때문이라고 한다.

### React StrictMode 란

자바스크립트에서는 코드 파일 최상단에 'use strict'를 써두면 자바스크립트를 실행했을 때 좀 더 엄격하게  코드를 검사한다.

React에서는 `StrictMode`가 있다.
`StrictMode`가 실행중일 때, console을 찍으면 2번씩 찍히는 걸 확인할 수 있다.

Strict Mode를 사용하지 않아도 동작하긴 하지만 사용하면 리액트가 자식 컴포넌트를 검사하고 잘못 사용된 부분을 알려준다.(단, 개발모드에서만 동작하니까 참고하기)

[StrictMode](https://ko.legacy.reactjs.org/docs/strict-mode.html)에서 검사하는 항목은 다음과 같다.

1. 잘못 사용한 생명주기 메서드
2. 레거시 문자열 ref 사용 여부
3. 권장되지 않는 findDOMNode 사용에 대한 경고
4. 예상치 못한 부작용 검사

## 참고

<https://funveloper.tistory.com/34><br/>
<https://overreacted.io/making-setinterval-declarative-with-react-hooks/><br/>
[useEffect 완벽 가이드](https://overreacted.io/a-complete-guide-to-useeffect/)<br/>
<https://react.dev/reference/react/StrictMode>