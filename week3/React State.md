# 학습 키워드

- React state란?
- DRY 원칙
- SSOT(Single Source of Truth)
- useState
- 1급 객체(first-class object)란?
- Lifting State Up

## ✔️ 키워드 정리

### React state란?

State는 컴포넌트에 대한 데이터 또는 정보를 포함하는 데 쓰이는 내장 객체라고 볼 수 있다.
컴포넌트의 상태는 변경될 수 있으며, 그 상태가 변경될 때마다 해당 컴포넌트가 다시 렌더링 된다.

State의 대한 변경은 컴포넌트의 동작, 렌더링 방법을 결정한다.

부모 컴포넌트가 props를 통해 전달된 것은 state가 아니다.
어떠한 값이 props 또는 state로부터 계산될 수 있다면, 그 값을 state에 두어서는 안된다.


### DRY 원칙

이 원칙은 모든 형태의 정보 중복을 지양하는 원리이다.
잘 짜여진 코드일수록 중복을 최소화하여 코드를 작성해둔 것을 볼 수 있다.

### SSOT(Single Source of Truth)

SSOT는 정보 시스템 설계 및 이론 중 하나로 정보와 스키마를 하나의 출처에서만 생성, 편집하도록 하는 방법론이다.


SSOT의 장점은 다음과 같다.
1. 정확성
: 데이터에 대한 일관성과 정확성을 유지하기 때문에 잘못된 데이터로 인한 잘못된 결정을 내리는 경우를 줄일 수 있다.

2. 일관성
: 모든 사용자가 동일한 정보를 사용하도록 보장하기 때문에 업무 프로세스와 의사결정에 일관성을 유지할 수 있다.

3. 효율성
: 모든 사용자가 동일한 정보를 사용하므로, 중복된 작업을 줄일 수 있어서 시간과 비용을 절약할 수 있다.

SSOT를 구현하기 위해서는 모든 데이터와 정보를 이해하고 표준화해야한다. 데이터의 표준화를 통해 일관성 있는 정보를 얻을 수 있고, 데이터의 정확성을 보장할 수 있다.

그러기 위해서는 데이터의 유형과 속성을 분석하고, 중복된 데이터를 제거해야하며 데이터 표준화 규칙을 작성해야한다.

SSOT는 데이터 일관성, 신뢰성, 효율성을 보장하는 중요한 개념이다.
데이터와 정보를 이해하고, 표준화하며, 출처를 지정하고 데이터 관리 규정을 작성해야한다.

### useState

리액트에서 함수형 컴포넌트를 작성할 때, 상태관리는 주로 Hook을 사용해서 하게 된다.
컴포넌트의 상태를 관리하고 업데이트할 때 useState를 사용해서 하게 되는데,

```Javascript
const [name, setName] = useState('');
```

컴포넌트의 현재 상태 값은 `name`이라는 변수에 들어있고, name을 변경하고 싶다면 setName 함수를 사용해서 변경할 수 있다.

setName을 이용해서 state를 변경하면 해당 컴포넌트는 다시 렌더링 된다.

모든 컴포넌트들은 자신의 이벤트 핸들러에서 setState()를 호출할 때까지 React는 리렌더링을 하지 않고 내부적으로 기다리고 있다. 이를 통해 불필요한 렌더링을 방지하면서 성능을 향상시킨다.

props와 state 사이에 일관성을 해칠 수 있으며, 디버깅하기 매우 힘든 이슈를 일으킬 수 있기 때문이고, 현재 작업중인 새로운 기능들을 구현하기 힘들게 할 수 있기 때문이다.

### 1급 객체(first-class object)란?

일급 객체란 변수에 할당할 수 있어야하고, 다른 함수를 인자로 전달 받아야한다.
또한 다른 함수의 결과로서 리턴될 수 있다.

함수가 일급 객체라면 고차함수를 만들 수 있고, 콜백을 사용할 수 있다.

일급 객체는 프로그래밍 언어론의 개념으로서, 자바스크립트 이외에도 다양한 언어들이 이 일급 객체 개념을 갖고 있다.


### Lifting State Up

리액트에서는 단방향 데이터 흐름을 원칙으로 한다.
따라서 하위 컴포넌트는 상위 컴포넌트로부터 전달 받은 데이터의 형태만 알 수 있다.

상위 컴포넌트에서 상태를 변경하는 함수를 하위 컴포넌트로 전달하고, 하위 컴포넌트가 전달받은 함수를 실행한다.
이것을 상태 끌어올리기라고 한다.

### 참고

https://onlyfor-me-blog.tistory.com/463<br/>
https://www.lesstif.com/software-engineering/ssot-single-source-of-truth-128122887.html<br/>
https://chancethecoder.tistory.com/45<br/>
https://legacy.reactjs.org/docs/hooks-state.html<br/>
https://inpa.tistory.com/entry/CS-%F0%9F%91%A8%E2%80%8D%F0%9F%92%BB-%EC%9D%BC%EA%B8%89-%EA%B0%9D%EC%B2%B4first-class-object<br/>
https://velog.io/@devjade/React-State-%EB%81%8C%EC%96%B4%EC%98%AC%EB%A6%AC%EA%B8%B0Lifting-State-Up<br/>