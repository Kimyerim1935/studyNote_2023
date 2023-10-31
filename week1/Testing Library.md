# 학습 키워드

- Jest
- Describe-Context-It 패턴
- React Testing Library

## ✔️ 키워드 정리

### Jest

Jest는 페이스북에서 만들어서 React와 더불어 많은 자바스크립트 개발자들이 사용하고 있는 테스팅 라이브러리이다.

하지만 기존의 다른 자바스크립트 테스팅 라이브러리들과의 차별점이 있어서 테스팅 프레임워크라고 불린다.

 Mocha와 Chai처럼 RSpec의 describe-it을 지원하고, expect로 단언(assertion)할 수 있다. Mocking도 다양한 레벨에서 쉽게 사용할 수 있다

Jest는 Test Runner, Test Matcher그리고 Test Mock까지 몽땅 해결이 되기 때문에 Jest하나로
모든 테스트를 다 할 수 있다.

### Describe-Context-It 패턴

```
describe('add func', () => {
    it('returns sum of two numbers' , () => {
        expect(add(1,2).toBe(3));
    })
})
```

### React Testing Library

UI 테스트에 특화된 라이브러리. 거의 E2E Test처럼 쓸 수 있다.

단, “F/E 테스트 = only React 컴포넌트 테스트”가 되는 상황은 최대한 피하는 게 좋다. 본질에 집중하지 못하고 너무 많은 테스트 코드를 작성할 위험이 있다. 유지보수를 돕기 위해 테스트 코드를 작성하는데, 테스트 코드를 잘못 작성하면 오히려 유지보수를 저해할 수 있다.

```
screen.getByText('Hello');
screen.getByText(/Hello/);

expect(screen.queryByText(/Hi/)).toBeInTheDocument();
expect(screen.queryByText(/Hi/)).not.toBeInTheDocument();
```
