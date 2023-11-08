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

Hook을 작성할 때 주의사항이 있다.

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



#### useState

컴포넌트에서 관리하는 동적인 값을 `state`라고 부른다.

```Javascript
const [value, setValue] = useState();
```

이 코드에서 `value`는 현재 상태, `setValue`는 Setter 함수이다.
제일 많이 쓰이는 Hook이라고 할 수 있다.

#### useEffect

#### useContext

#### useRef

#### useLayoutEffect

### React StrictMode 란

## 참고

<https://funveloper.tistory.com/34><br/>
