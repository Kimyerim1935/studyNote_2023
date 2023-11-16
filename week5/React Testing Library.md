# 학습 키워드

- React Testing Library
- given - when - then 패턴
- Mocking
- Test fixture

## ✔️ 키워드 정리

### React Testing Library

[React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)는 React 구성요소를 테스트하기 위한 매우 가벼운 솔루션이다.

React Testing Library가 Jest랑 혼돈되는 경우가 종종 있는데, 엄밀히 따지자면 React Testing Library가 Jest를 포함하는 구조이다. 전반적으로 Jest를 통해 기능 테스트를 진행할 수 있지만, React의 컴포넌트를 렌더링하고 테스트 하기 위해서는 몇 가지의 기능이 더 필요하기 때문이다.

### given - when - then 패턴

`given-when-then` 패턴은 테스트 코드를 `준비-실행-검증` 이렇게 세 단계로 나누는 패턴을 말한다.

이런식으로 사용한다.

```Javascript
// Textfield.test.tsx
import {render. screen} from '@testing-library/react';

test('TextField', () => {
    // given
    const setFilterText = () => {
        ...
    }

    // when
    render((
        <TextField
            placeholder=""
            text=""
            setFilterText={setFilterText}
    />
    ));

    // then
    screen.getByLabelText('Search');
})

```

`given`에서 테스트를 준비하고, `when`에서 검증하고자 하는 메서드를 호출하고, `then`에서 호출 결과를 검증한다.

이 패턴은 BDD의 일부로 많은 테스트 프레임워크에 대한 구조화 접근 방식으로 나타난다.

BDD는 행동을 기반으로 하여 TDD를 수행하자는 공통의 이해인데, 애플리케이션이 어떻게 행동해야 하는지에 대한 이해를 구성하는 방법이다.

### Mocking

mocking이란 테스트하고자 하는 코드가 의존하는 function이나 class에 대해 모조품을 만들어 일단 돌아가게 만드는 것이다.
단위 테스트를 작성할 때 해당 코드가 의존하는 부분을 가짜로 대체하는 기법을 말한다.

프론트엔드 개발을 하다보면 서버에서 제공되는 API를 이용해서 정보를 받아오거나 정보를 보내서 응답을 받은 후에 액션을 처리하는 작업을 하게 된다.

API 스펙이 나오면 API를 호출하는 코드를 작성할 수 있지만, API 구현이 되지 않았다면 실제 데이터를 불러올 수 없으니 작업을 더 진행할 수 없다.
그래서 대안으로 응답 타입이 맞추어 Mock 데이터 객체를 만들고 이를 API 응답값처럼 이용한다.

[MSW](https://mswjs.io/) 라이브러리를 Mocking 할 때 주로 사용한다. MSW는 API를 쉽고 깔끔하게 Mocking 할 수 있도록 도와주는 라이브러리이다.

### Test fixture

Test fixture는 소프트웨어 테스팅 뿐만 아니라 회로나 물리적인 디바이스를 테스트 할 때도 사용되는 용어다.

소프트웨어에서 Test fixture는 어떤 테스트가 실행하는 환경을 위해 필요한 설정을 먼저 완료해주는 것이다.

쉽게 말해, 중복 발생되는 무언가를 고정시켜 한곳에서 관리하도록 하겠다는 개념이다.

대표적으로 Ruby On Rails 웹 프레임워크에서는 데이터베이스를 이미 알고 있는 파라미터로 초기화하기 위해 YAML 설정 파일을 사용한다. 이를 통해서 테스트가 반복적으로 동일한 Code Under Test 밑에서 안정적으로 같은 결과를 낼 수 있게 된다.

Test fixture는 다음과 같은 방식으로 셋업할 수 있다.
1. In-line: 가장 간단한 Test fixture 셋업으로, 각 메소드에 직접 테스트에 사용되는 fixture을 생성하는 경우, 여러 테스트가 동일한 데이터를 사용해야하는 경우 중복해서 fixture을 생성한다는 단점이 있다.

2. Delegate: 테스트 fixture를 별도의 helper mothod에 위치시키는 방법

3. Implicit: test가 실행될 때 자동으로 실행되는 setup function에서 test fixture를 위치시키는 경우

## 참고

<https://martinfowler.com/bliki/GivenWhenThen.html><br/>
<https://braindisk.tistory.com/91><br/>
<https://tech.kakao.com/2021/09/29/mocking-fe/><br/>
<https://yozm.wishket.com/magazine/detail/1711/><br/>
<https://greenmon.dev/2022/10/14/about-test-fixture.html><br/>
<https://thalals.tistory.com/375>