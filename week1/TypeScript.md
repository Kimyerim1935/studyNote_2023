## ✔️ 키워드 정리

### REPL
REPL(read-eval-print loop)은 단일 사용자의 입력을 취하고 이를 평가하고 결과를 사용자에게 반환하는 단순한 프로그래밍 환경이다.

주로 개발자들이 소스 코드 실행 결과를 빨리 확인해야하는 경우에 사용한다.

### TypeScript

#### Interface vs Type

공통점
- 객체, 함수의 타입을 정의할 수 있다.
- 변수 타입, 함수의 반환값을 지정하는 데 둘 다 사용할 수 있다.
- type과 interface 모두 확장하여 새 유형을 만들 수 있다.

차이점
- type은 기존 타입의 새 이름을 정의하는 방법이며, interface는 새로운 객체를 처음부터 정의한다. 
type은 Type Alias를 지정하는 데 사용할 수 있고, interface는 완전히 새로운 유형을 정의하는 데 사용할 수 있다.

- type은 선언된 타입을 재 선언시 오류가 지만, interface는 기존의 객체에 더하여 확장된다.

- type은 유니온 타입 및 인터섹션 타입을 만드는 데 사용할 수 있지만, interface는 오직 객체 유형을 만드는데만 사용할 수 있다.

#### 타입 추론
- 타입 추론이란 타입스크립트가 코드를 해석해나가는 동작을 의미한다.

```js
let x = 3;
```

이 코드에서 x의 타입을 따로 지정하지 않더라도 일단 x는 number로 간주된다. 변수를 선언 또는 초기화할 때 타입이 추론된다. 이 외에도 변수, 속성, 인자의 기본 값, 함수의 반환 값 등을 설정할 때 타입 추론이 일어난다.

#### Union Type vs Intersection Type

여러 항목들 중의 하나를 타입으로 지정하고 싶을 때 Union Type을 사용한다.

```js
type Fruits= "Apple" | "Orange" | "Banana";
type Desserts = "Pie" | "Cake";
```
| 이 기호로 구분하고 JavaScript의 or 연산자와 비슷한 역할을 한다. Union은 합집합이기 때문에 모든 요소들을 다 포함할 수 있다.

```js
type MyFavorites = Fruits | Deserts;
```
이렇게 MyFavorites 타입을 만들게 되면 Fruits 타입과 Desserts 타입을 모두 할당할 수 있다.


```js
type MyHobbies = "Swimming" | "Photography" | "Cooking";
type Exercises = "Swimming" | "Walking" | "Yoga";

type MyFavoriteHobbies = MyHobbies & Exercises;  // Swimming
```
&기호를 사용하면 양쪽 모두 할당할 수 있는 값만 남긴다. 
즉, 겹치는 값이 할당된다. 
반면에 아무것도 겹치지 않는다면 할당할 수 있는 값이 없으므로 `never`가 된다.

#### Optional Parameter
JavaScript에서는 함수가 매개변수를 지정하더라도 인수를 전달하지 않고 함수를 호출할 수 있다. 따라서 JavaScript는 기본적으로 선택적 매개변수를 지원한다.

TypeScript에서 컴파일러는 모든 함수 호출을 확인하고 다음과 같을 경우 오류를 발생시킨다.
1. 인수 개수가 함수에 지정된 매개 변수의 개수와 다를 경우
2. 인수 타입이 함수의 매개변수 타입과 일치하지 않을 경우

```js
function Add(a:number, b:number, c?: number) {
    return a + b + c;
}
```

타입을 지정하기 전에 ?를 붙여주면 해당 매개변수가 undefined여도 에러가 나타나지 않는다. 하지만 기본값을 지정해주는게 좋다고 해서 기본값을 지정해서 작성하는걸 습관화해야겠다.
