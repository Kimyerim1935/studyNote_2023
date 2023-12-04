# 학습 키워드

- className
- 의미있는 마크업

## ✔️ 키워드 정리

### className

className은 특정 엘리먼트의 클래스 속성의 값을 가져오거나 설정할 수 있다.
리액트에서는 class를 사용하지 않고 JSX문법으로 className을 사용한다.

* css는 컴포넌트를 전제로 하고 있지 않는다. 공통된 부분이 많을 때 재사용하기 쉽다.

```Javascript
const darkMode = false;

function primaryColor (){
  return darkMode ? '#F00' : '#00F';
}

export default function Greeting(){
  return (
    <p style={{color: primaryColor()}}>
      hello~
    </p>
  )
}

// 또는 이렇게도 사용 가능
export default function Greeting(){
  const style = {
    color: 'blue'
  }

  return (
    <p style={style}>
      hello~
    </p>
  )
}

```

이런식으로 인라인 style을 작성해서 사용할 수도 있다.

### 의미있는 마크업

[참고](https://developer.mozilla.org/ko/docs/Web/HTML/Reference)

의미론적 [마크업](https://developer.mozilla.org/ko/docs/Glossary/Markup)은 W3C의 권고사항이며, 이에 따라 HTML5에서는 의미론적 마크업을 위한 다양한 태그들이 새롭게 생겨났다.

이런 부분들을 잘 맞춰서 코드를 작성해야한다.

- 헤더/푸터에 `<header>`와 `<footer>` 사용
- 메인 컨텐츠에 `<main>`과 `<section>`사용
- 독립적인 컨텐츠에 `<article>` 사용
- 최상위 제목으로 `<h1>` 사용
- 순서가 없는 목록으로 `<ul>`과 `<li>` 사용
- 내비게이션에 `<nav>`사용

마크업을 잘 작성하면 검색 엔진이 시맨틱 태그를 중요한 키워드로 간주하기 때문에 검색엔진 최적화(SEO)에 유리하다.
웹 접근성 측면에서, 시각장애가 있는 사용자로 하여금 그 의미를 훨씬 잘 파악할 수 있다.
코드를 볼 때 가독성이 좋다.