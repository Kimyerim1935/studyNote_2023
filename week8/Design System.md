# 학습 키워드

- 반응형 웹 디자인(Responsive web design)
- 디자인 시스템(Design System)
- Atomic Design

## ✔️ 키워드 정리

### 반응형 웹 디자인(Responsive web design)

[반응형 디자인](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Responsive_Design)은 웹 페이지가 모든 화면 크기와 해상도에서 잘 렌더링 되도록 하면서도 사용성을 보장하는 웹 디자인 접근 방식이다. 멀티 디바이스 웹을 위한 디자인 방식이라고도 한다.

요새 대부분의 웹 사이트들은 반응형 웹 디자인을 적용한 것을 볼 수 있다.

[미디어 쿼리](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_media_queries)를 사용하면 css를 선택적으로 적용하여 사용자의 요구에 맞게 페이지의 스타일을 지정할 수 있다.

제일 작은 화면부터 제일 큰 화면 순으로 디자인 하는 것을 모바일 우선 디자인이라고 한다.



### 디자인 시스템(Design System)

[디자인 시스템](https://www.nngroup.com/articles/design-systems-101/)은 여러 페이지와 채널에서 공유 언어와 시각적 일관성을 생성하는 동시에 중복성을 줄여 규모에 맞게 디자인을 관리하기 위한 표준 세트이다.

디자인 시스템 예시

- [Atlassian Design System](https://atlassian.design/)
- [Material Design (Google)](https://material.io/)
- [Base Web (Uber)](https://baseweb.design/)
- [Polaris (Shopify)](https://polaris.shopify.com/)
- [Lightning Design System (Salesforce)](https://www.lightningdesignsystem.com/)
- [Mailchimp Pattern Library](https://ux.mailchimp.com/patterns)
- [Ant Design](https://ant.design/)

디자인 시스템을 잘 구현하면 디자인 팀을 비롯하여 프로젝트에 참여하는 인원에게 많은 이점을 제공할 수 있다.

1. 디자인 및 개발 작업을 대규모로 신속하게 생성하고 복제할 수 있다.
: 디자인 시스템의 주요 이점은 미리 만들어진 UI 구성 요소와 요소를 활용하여 디자인을 빠르게
복제할 수 있다는 것이다.

2. 더 크고 복잡한 문제에 집중할 수 있도록 설계 리소스의 부담을 덜어준다.
: 더 간단한 UI 요소가 이미 생성되어 재사용 가능하므로 디자인 리소스는 시각적 모양을 조정하는것보다 더 복잡한 문제에 집중할 수 있다. 규모가 작은 프로젝트의 화면만 생성할 경우 이러한 보상이 작아보일 수 있지만, 규모가 큰 프로젝트의 경우 상당한 이점이 있다.

3. 다기능 팀 내 팀 간에 통일된 언어를 생성한다.
: 설계 책임이 바뀌거나 팀이 분산될 때 통합된 언어는 잘못된 의사소통으로 인해 낭비되는 설계 또는 개발 시간을 줄여준다.

4. 제품 및 부서 전반에 걸쳐 시각적 일관성을 만든다.
: 디자인 시스템은 구성 요소, 패턴 및 스타일의 단일 소스를 제공하고 분리된 경험을 통합하여 시각적으로 응집력이 있고 동일한 생태계의 일부인 것처럼 보인다.

반면에, 디자인 시스템을 사용하는 것을 방해할 수 있는 몇 가지의 제한 사항이 있다.

1. 디자인 시스템을 만들고 유지하는 것은 전담 팀이 필요한 시간 집약적인 활동이다.

2. 다른 사람들에게 디자인 시스템 사용법을 가르치는 데에는 시간이 걸린다.

3. 프로젝트는 일반적으로 재사용 가능한 구성 요소가 필요하지 않은 정적인 일회성 창작물이라는 인식이 있을 수 있다.

### Atomic Design

[Atomic Design](https://atomicdesign.bradfrost.com/table-of-contents/)은 디자인 시스템을 만드는 방법론이다.

이렇게 다섯 단계로 나뉜다.

1. [Atoms](https://bradfrost.com/blog/post/atomic-web-design/#atoms)
2. [Molecules](https://bradfrost.com/blog/post/atomic-web-design/#molecules)
3. [Organisms](https://bradfrost.com/blog/post/atomic-web-design/#organisms)
4. [Templates](https://bradfrost.com/blog/post/atomic-web-design/#templates)
5. [Pages](https://bradfrost.com/blog/post/atomic-web-design/#pages)

컴포넌트 간의 계층을 만들기 위한 방법이라고 생각하면 편할 것 같다.