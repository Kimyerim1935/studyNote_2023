# 학습 키워드

- useRef
- Hook의 규칙

## ✔️ 키워드 정리

### useRef

[beta 버전 공식 문서](https://react.dev/reference/react/useRef)<br/>
[공식 문서](https://ko.legacy.reactjs.org/docs/hooks-reference.html#useref)

함수형 컴포넌트에서 ref를 사용할때는 [useRef](https://ko.legacy.reactjs.org/docs/refs-and-the-dom.html)라는 함수를 사용한다.

ref의 값을 가져올 땐 current를 사용해서 가져오면 된다.

```Javascript
 const intervalId = intervalRef.current;
```

반환된 useRef 객체는 컴포넌트의 전 생애주기를 통해 유지가 된다.
객체 자체가 값은 아니고, 값을 참조하기 위한 객체이다.(언제든지 변경할 수 있음)<br/>
=> 컴포넌트가 계속해서 렌더링이 되어도 컴포넌트가 언마운트 되기 전까지는 값을 그대로 유지한다.<br/>
=> current 숙성은 값을 변경해도 React 컴포넌트가 재렌더링 되지 않는다.

### Hook의 규칙

[Hook](https://ko.legacy.reactjs.org/docs/hooks-rules.html)을 작성할 때 주의사항이 있다.

반복문, 조건문 그리고 중첩된 함수 내에서 호출해서는 안된다.
컴포넌트가 렌더링될 때마다 항상 동일한 순서로 훅이 호출되어야하기 때문이다.

일반적인 javascript 함수에서 호출하면 안된다.
상태 관련 로직을 소스코드에서 명확하게 보이도록 해야하기 때문이다.

이런 규칙을 강제하도록 하는 ESLint 플러그인이 있다.
(CRA로 프로젝트를 설치하면 포함되어있다고 한다.)

이걸 설치하면 사용할 수 있다.

```Bash
npm install eslint-plugin-react-hooks --save-dev
```
