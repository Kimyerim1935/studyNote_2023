# 학습 키워드

- TDD란
- Jest
- Describe - Context - It 패턴
- 단위테스트란

## ✔️ 키워드 정리

### TDD란

[TDD](https://web.archive.org/web/20070628064054/http://xper.org/wiki/xp/TestDrivenDevelopment)의 궁극적인 목표는 작동하는 깔끔한 코드를 작성하는 것이다. TDD의 개발 단계에는 리팩토링이 있는데, 리팩토링을 거치면서 중복된 코드들은 제거되고, 복잡한 코드들은 깔끔하게 정리된다.

테스트를 처음 작성할 때는 귀찮고 개발이 느려진다는 느낌을 받을 수 있지만, 장기적인 관점에서 봤을 때 개발 비용을 아껴준다는 장점이 있다.

TDD 개발 주기는 다음과 같다.

1. Red -> 실패하는 테스트 코드 작성. 인터페이스와 스펙에 집중한다.
2. Green -> 테스트를 통과하는 코드를 작성한다. 올바르지 않더라도 테스트만 통과할 수 있게끔
3. Refactor -> 리팩토링을 통해 코드를 올바르게 만든다. TDD에서 가장 중요한 부분!

TDD와 일반적인 개발 방식의 가장 큰 차이점은 테스트 코드를 작성한 뒤에 실제 코드를 작성한다는 것이다.
설계 단계에서 프로그래밍 목적을 반드시 미리 정의해야만 하고, 테스트 케이스도 작성을 해야만 한다.

테스트 코드를 작성하는 도중 발생하는 예외 사항도 테스트 케이스에 추가하고 설계를 개선한다.

이런 반복적인 단계를 진행하면서 자연스럽게 코드의 버그가 줄어들고, 간결해진다.

단위를 작게 만들어서 계속 반복하며 수정하는게 포인트이다. 테스트 케이스를 작성한다고 해서 다 TDD는 아니다.

### Jest

필요한건 다 갖고 있는 [Jest](https://jestjs.io/) 라이브러리는 페이스북에서 만들었다.

Jest를 사용하기 전에는 여러가지의 테스팅 라이브러리를 조합해서 사용했다고 한다.
Mocha나 Jasmin을 Test Runner로 사용하고, Chai나 Expect와 같은 Test Mathcher를 사용했다. 그리고 Sinon과 Testdouble과 같은 Test Mock라이브러리도 필요했었다.

여러 라이브러리를 사용하다보니 개발자들에게 혼란을 야기했다는 아쉬운점이 있었다.

하지만 Jest는 설치하기만 하면, Test Runner부터 Test Mock 프레임워크까지 제공해주기 때문에 현재 많이 사용되고 있다.

### Describe - Context - It 패턴

Jest를 사용해서 테스트 코드를 작성할 경우의 예시이다.

```Javascript
function add(...numbers: number[]): number{
   if (numbers.length === 0) {
    return 0;
   }

   return numbers.reduce((acc, number) => acc + number);
}

test('add test', () => {
    expect(add(1,2)).toBe(3);
})

describe('add', ()=> {
    context('with no argument', ()=> {
            it('return zero', () => {
                expect(add()).toBe(0);
            })
        })
    context('with only one argument', ()=> {
        it('returns the same number', () => {
            expect(add(2)).toBe(2);
        })
    })

    context('with two arguments', ()=> {
        it('returns sum of two numbers', ()=> {
            expect(add(1,2)).toBe(3);
        })
    })
})
```

먼저 테스트하고자 하는 함수를 상단에 작성해준 다음 테스트 코드를 작성한다.

- test, it: test()를 통해 테스트를 진행한다. 주로 개별적인 테스트를 작성할 때 사용한다. it은 text의 alias라고 한다.
- describe: 테스트의 단위를 묶는 큰 단위이다. 기재된 내용으로 단위를 분류한다. 테스트 할 대상을 명시한다.
- context: 테스트 대상이 놓인 상황/조건을 설명한다.
- expect: 테스트 할 코드를 넣어준다.
- toBe(), toEqual(): toBe()는 단순 비교, toEqual은 배열이나 객체 내부 깊은 비교를 수행한다. 공식문서에서 toEqual()은 객체 또는 배열의 모든 필드를 재귀적으로 검사한다고 한다.
- beforeEach(): test를 진행하기 전 최초 1회 실행되는 전처리기이다.
- afterEach(): test가 모두 진행된 후 마지막에 1회 실행되는 후처리기이다.

이런 패턴을 사용해서 테스트 코드를 계층 구조로 만들면 나중에 다시 봤을 때도 파악하기 쉽다는 장점이 있다.

### 단위테스트란

단위 테스트는 하나의 모듈을 기준으로 독립적으로 진행되는 가장 작은 단위의 테스트이다.
여기서의 모듈은 애플리케이션에서 작동하는 하나의 기능 또는 메서드로 이해할 수 있다.

즉, 단위 테스트는 애플리케이션을 구성하는 하나의 기능이 올바르게 동작하는지를 독립적으로 테스트 하는 것으로 "어떤 기능이 실행 됐을 경우, 어떤 결과가 나온다" 정도로 진행한다.

단위 테스트는 해당 부분만 독립적으로 테스트하기 때문에 어떤 코드를 리팩토링 해도 빠르게 문제 여부를 확인할 수 있다. 뿐만 아니라 새로운 기능을 추가했을 경우에도 빠르게 테스트를 수시로 진행할 수 있어서 테스팅에 대한 시간과 비용을 줄일 수 있다.

## 참고

<https://velog.io/@zzezze/TIL-Describe-Context-It><br/>
<https://velog.io/@kozel/Jest-Jest-%EA%B8%B0%EC%B4%88-Jest-Getting-Started><br/>
