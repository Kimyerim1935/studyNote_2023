# 학습 키워드

- E2E(End to End) Test
- Headless Chrome
- Puppeteer
- Playwright
- CodeceptJS

## ✔️ 키워드 정리

### E2E(End to End) Test

E2E Test는 End To End 테스트의 약자로 애플리케이션의 흐름을 처음부터 끝까지 테스트하는 것을 의미한다.
유닛테스트나 통합 테스트는 모듈의 무결성을 증명할 수 있는 강력한 테스트이지만, 모듈의 무결성이 애플리케이션 동작의 무결성까지 모두 증명해줄 수 없다.
하지만, E2E 테스트 과정에서는 실제 사용자의 시나리오를 테스트 하기 때문에 애플리케이션의 전반적인 동작들을 테스트하고 테스트를 통과함으로써 애플리케이션의 무결성을 증명할 수 있다.

### Headless Chrome

Headless 모드는 보통 웹 브라우저가 GUI로 동작하게 되는데, GUI 없이 프로그램 상으로만 돌리는 것을 의미한다. 실제 브라우저와 같게 동작하므로 Javascript도 잘 동작하고 웹 사이트를 크롤링하거나 스크린샷을 찍을 때 유용하다.
브라우저 테스트를 할 때도 훨신 빠르게 돌릴 수 있다.

headless Chrome으로 웹사이트를 띄워놓고 원격으로 디버깅할 수 있다.
서버 등에서 headless Chrome으로 작업을 할 때 원격 디버깅 포트를 열면 데스크톱에 설치된 Chrome에서 접속해서 디버깅이 가능하다.

디버깅 할 사이트를 클릭하면 브라우저에서 디버깅할 때와 동일하게 개발자 도구에서 디버깅 할 수 있다.

### Puppeteer

puppeteer은 구글에서 만든 노드 라이브러리로 Headless Chrome 또는 Chrominum을 제어할 수 있다.

puppeteer를 사용하면 이런 것들을 할 수 있다.

- 화면을 스크린샷 하거나 PDF를 생성할 수 있다.
- SPA을 크롤링하여 사전에 컨텐츠를 렌더링 할 수 있다.
- 자동화된 UI 테스트를 실행할 수 있다.
- 최신 버전의 크롬에서 자동화된 테스트 환경을 만들 수 있다.
- timeline trace를 통해 퍼포먼스 이슈를 진단할 수 있다.
- 크롬 확장 프로그램을 테스트 할 수 있다.

puppeteer API는 계층적인 구조로 구성되어 있고, 실제 브라우저 구성요소처럼 되어있다.

- puppeteer는 크롬의 DevTools Protocol을 사용하여 브라우저를 컨트롤한다.
- Browser 인스턴스는 다수의 browser context를 가질 수 있다.
- Page는 최소 하나의 Frame을 가지고 있어야 한다.

### Playwright

하나의 API로 모든 최신 브라우저에서 빠르고 안정적인 자동화를 원하는 MS에서 만든 자동화 도구다.
레거시 Edge나 IE11은 지원하지 않지만 다양한 장점이 있다.

- 여러 페이지, 도메인, iframe에 걸친 시나리오
- 클릭과 같은 액션을 실행하기 전에 엘리먼트가 준비될 때까지 기다림
- 네트워크 요청을 모킹하기 위한 네트워크 활동 가로채기
- 마우스, 키보드의 기본 입력 이벤트

### CodeceptJS

CodeceptJs는 특수한 BDD 스타일 구문을 사용하는 최신 E2E 테스트 프레임워크이다.
단위 테스트만으로는 시스템이 올바르게 작동하는지 알 수 없고, 사용자가 유용하게 사용할 수 있는지 미리 정의하는것도 쉽지 않다. 결정적으로 사용자와 소통하기 위한 교차점이 마련되어 있지 않기 때문에 인수테스트가 필요하다.

인수 테스트는 여러 방식으로 작성할 수 있다.

codeceptjs를 설치한 뒤,

```Javascript
Feature('Google');

Scenario('Search “CodeceptJS”', ({ I }) => {
  I.amOnPage('https://www.google.com/ncr');
  I.fillField('[name="q"]', 'CodeceptJS');
  I.click('Google Search');
  I.see('codecept.io');
});
```

이런식으로 사용하면 된다.

## 참고

<https://fe-developers.kakaoent.com/2023/230209-e2e/><br/>
<https://blog.outsider.ne.kr/1291><br/>
<https://ui.toast.com/posts/ko_20210818><br/>
<https://github.com/ahastudio/til/blob/main/test/20201207-codeceptjs.md>