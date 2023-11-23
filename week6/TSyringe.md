# 학습 키워드

- TSyringe
- 의존성 주입(Dependency Injection)
- reflect-metadata
- singleton (싱글톤)

## ✔️ 키워드 정리

### TSyringe

JavaScript와 TypeScript를 위한 경량 종속성 주입 컨테이너라고 한다.
타입스크립트에서 주로 사용한다.

TSyringe는 TypeScript용 DI도구이며 External Store를 관리하는 데 활용할 수 있다.

이 명령어로 설치하고,

```Bash
npm i tsyringe reflect-metadata
```

싱글톤으로 관리할 CounterStore 클래스를 준비하면 에러가 발생하는 것을 확인할 수 있다.

```Javascript
// Store.ts

import {singleton} from 'tsyringe';

@singleton()
export default class Store{
  count = 0;
}
```

‼️ 꼭 추가해줘야한다.

```Javascript
// main.tsx(제일 최상위 컴포넌트 파일) & setupTests.ts
import 'reflect-metadata';
```

`@singleton`에서 `@`는 [데코레이터](https://typescript-kr.github.io/pages/decorators.html)이다.

데코레이터를 사용할 때 `tsconfig.json`파일에서 요 부분의 주석을 풀어주면 된다.

```JSON
  // "experimentalDecorators": true,
  // "emitDecoratorMetadata": true,
```

📋 Store 사용 예시 코드

```Javascript
// CounterStore.ts

import {singleton} from 'tsyringe';

type Listener = () => void;

@singleton()
export default class CounterStore{
  count = 0;

  listeners: new Set<Listener>();

  increase() {
    this.count += 1;
    this.publish();
  }

  decrease() {
    this.count -= 1;
    this.publish();
  }

  publish() {
    this.listeners.forEach((listener) => {
      listener();
    });
  }

  addListener(listener: Listener) {
    this.listeners.add(listener);
  }

  removeListener(listener: Listener) {
    this.listeners.delete(listener);
  }
}

// useForceUpdate.ts
import {useState, useCallback} from 'react';

export default function useForceUpdate(){
  const [_, setState] = useState({});
  return useCallback(() => setState({}), [])
}

// useCounterStore
import {useEffect} from 'react';
import {container} from 'tsyringe';

import useForceUpdate from '../hooks/useForceUpdate';
import CounterStore from '../stores/CounterStore';

export default function useCounterStore() {
  const store = container.resolve(CounterStore);
  const forceUpdate = useForceUpdate();

  useEffect(() => {
    store.addListener(forceUpdate);

    return () => {
     store.removeListener(forceUpdate);
    }
  }, [store, forceUpdate])
}

// Counter.tsx
import useCounterStore from '../hooks/useCounterStore';

export default function Counter() {
  const store = useCounterStore();

  return (
    <div>
      <p>
      Count:
      {' '}
      {store.count}
      </p>
    </div>
  )
}

// CounterControl.tsx
import useCounterStore from '../hooks/useCounterStore';

export default function CountControl(){
  const store = useCounterStore();

  const handleClickIncrease = () => {
    store.increase();
  }

  const handleClickDecrease = () => {
    store.decrease();
  }

  return (
    <div>
      <p>{store.count}</p>
      <button type="button" onClick={handleClickIncrease}>
        Increase
      </button>
       <button type="button" onClick={handleClickDecrease}>
        Decrease
      </button>
    </div>
  )
}
```

테스트에서 TSyringe에서 관리하는 객체를 초기화할 수 있다.

```Javascript
import {render, screen} from '@testing-library/react';
import {container} from 'tsyringe';
import App from './App';

const context = describe;

test('App', () => {
  render(<App/>);
});

describe('App', () => {

  beforeEach(() => {  // 각 테스트 함수가 실행되기 전에 매번 호출됨 딱 한 번 호출하는건 BeforeAll
    container.clearInstances();
  })

  context('when press increase button once', ()=> {
    test('counter', () => {
      render(<APP/>);

      fireEvent.click(screen.getByText('Increase'));

      const elements = screen.getByText('Count: 1');
      expect(elements).toHaveLength(1);
    })
  })

  context('when press increase button twice', ()=> {
    test('counter', () => {
      render(<APP/>);

      fireEvent.click(screen.getByText('Increase'));

      const elements = screen.getByText('Count: 1');
      expect(elements).toHaveLength(1);
    })
  })
})

```

### 의존성 주입(Dependency Injection)

의존성 주입은 말 그대로 객체에 의존성을 주입하는 것이다.
한 객체의 코드에서 다른 객체를 생성하거나 다른 객체의 메서드를 호출할 때, 파라미터로 객체를 전달받아 사용할 때 의존성이 발생한다고 할 수 있다.

클래스 A가 다른 클래스나 인터페이스 B를 사용할 때 A는 B에 의존한다고 얘기할 수 있다.
이때, 모듈과 모듈 사이의 의존성의 정도를 결합도라고 한다.

하지만 의존성은 유닛 테스트가 어려운 코드를 만든다. 유닛 테스트는 특정 모듈이 의도된대로 작동하는지 테스트 하는 과정을 의미하는데 특정 모듈의 작동이 다른 모듈을 필요로 한다면 특정 모듈만 독립적으로 떼어내어 테스트하기 어렵다.
과도한 의존성은 모듈을 재사용하기 어렵게 만든다는 단점이 있다.

의존성 주입은 필요한 객체를 직접 생성하거나 찾지 않고, 외부에서 넣어주는 방식이다.
객체의 의존관계를 내부에서 결정하는 것이 아니라 객체 외부에서 런타임 시점에 결정하는 방식이다.

의존성 주입을 사용하는 이유는 모듈간 변경에 민감해지지 않아, SOLID 원칙 중 OCP를 만족하는 코드를 작성할 수 있고, 재사용성이 높아지고, 유닛 테스트를 쉽게 만들어주며 가독성이 증가하기 때문이다.

### reflect-metadata

메타 데이터는 데이터에 대한 데이터이다.

```Javascript
function sample() {
  console.log('sample function')
}

sample.name;  // sample
```

`sample`은 sample이라는 함수의 메타데이터라고 할 수 있다.
타입스크립트는 reflect-metadata 라는 패키지를 사용한다.

reflect-metadata 에서 제공하는 메서드나 데코레이터를 활용하여 쉽게 메타데이터를 추가할 수 있다.

### singleton (싱글톤)

싱글톤 패턴의 정의는 객체의 인스턴스가 오직 1개만 생성되는 것을 의미한다.

싱글톤 패턴을 사용하면 최초 한 번의 new 연산자를 통해서 고정된 메모리 영역을 사용하기 때문에 추후 해당 객체에 접근할 때 메모리 낭비를 방지할 수 있다는 장점이 있다.
뿐만 아니라 이미 생성된 인스턴스를 활용하니 속도 측면에서도 이점이 있다고 볼 수 있다.

또 다른 이점은 데이터 공유가 쉽다는 것이다.
싱글톤 인스턴스가 전역적으로 사용되는 인스턴스이기 때문에 다른 클래스의 인스턴스들이 접근하여 사용할 수 있다. 여러 클래스의 인스턴스에서 싱글톤 인스턴스의 데이터에 동시에 접근하게 되면 동시성 문제가 발생할 가능성이 있으니 유의하여 설계해야한다.

하지만 싱글톤 패턴을 구현하는 코드 자체가 많이 필요하다는 단점이 있다.

싱글톤 인스턴스는 자원을 공유하고 있기 때문에 테스트가 격리된 환경에서 수행되려면 매번 인스턴스의 상태를 초기화시켜줘야한다. 그렇지 않으면 테스트가 온전하게 이루어질 수 없다.

new 키워드를 직접 사용하여 클래스 안에서 객체를 생성하고 있기 때문에 SOLID 원칙 중 DIP를 위반하게 되고 OCP 원칙 또한 위반할 가능성이 높다.

이외에도 내부 상태를 변경하기 어렵다는 점, 자식 클래스를 생성할 수 없다는 등 여러가지 문제들이 있지만 장점을 잘 활용하면 유용한 패턴이라고 생각한다.

## 참고

<https://hudi.blog/dependency-injection/><br/>
<https://tecoble.techcourse.co.kr/post/2021-04-27-dependency-injection/><br/>
<https://velog.io/@kkajjeim/%EB%8D%B0%EC%BD%94%EB%A0%88%EC%9D%B4%ED%84%B0%EC%99%80-%EB%A9%94%ED%83%80%EB%8D%B0%EC%9D%B4%ED%84%B0>
