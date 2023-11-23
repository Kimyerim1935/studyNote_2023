# 학습 키워드

- usestore-ts
- useSyncExternalStore

## ✔️ 키워드 정리

### usestore-ts

```Javascript
// CounterStore.ts
import {singleton} from 'tsyringe';

import ObjectStore from './ObjectStore';

@singleton()
export default class CounterStore extends ObjectStore {
  count = 0;

  /**
   * 카운트를 증가시킨다
   */
  increase(step = 1) {
    this.count += step;
    this.publish();
  }

  /**
   * 카운트를 감소시킨다
   */
  decrease(step = 1) {
    this.count -= step;
    this.publish();
  }
}

// ObjectStore.ts
type Listener = () => void;

export default class ObjectStore{
  count = 0;

  private listeners: new Set<Listener>();

  protected publish() {
    this.listeners.forEach((listener) => listener());
  }

  addListener(listener: Listener) {
    this.listeners.add(listener);
  }

  removeListener(listener: Listener) {
    this.listeners.delete(listener);
  }
}

// Counter.tsx
import useCounterStore from '../hooks/useCounterStore';

export default function Counter(){
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

// useCounterStore
import {container} from 'tsyringe';

import CounterStore from '../stores/CounterStore';
import ObjectStore from '../stores/ObjectStore';

export default function useCounterStore() {
  const store = container.resolve(CounterStore);

  return useObjectStore(store);
}

// useObjectStore.ts
import {useEffect} from 'react';

import useForceUpdate from './useForceUpdate';

import ObjectStore from '../stores/ObjectStore';

export default function useObjectStore<T extends ObjectStore>(store: T):T{
  const forceUpdate = useForceUpdate();

  useEffect(() => {
    store.addListener(forceUpdate);

    return () => {
      store.forceUpdates.delete(forceUpdate);
    }
  }, [store, forceUpdate])
  return store
}

// CounterControl.tsx
import useCounterStore from '../hooks/useCounterStore';

export default function CountControl(){
  const store = useCounterStore();
  const {count} = store;

  return (
    <div>
      <p>{count}</p>
      <button type="button" onClick={()=> store.increase()}>
        Increase
      </button>
      <button type="button" onClick={()=> store.increase(10)}>
        Increase 10
      </button>
       <button type="button" onClick={() => store.decrease()}>
        Decrease
      </button>
      <button type="button" onClick={() => store.decrease(10)}>
        Decrease 10
      </button>
    </div>
  )
}
```

기존 코드에 usestore-ts를 적용하는 방법은 다음과 같다.

```Javascript
// CounterStore.ts
import {singleton} from 'tsyringe';
import {Action, Store} from 'usestore-ts';

@singleton()
@Store()  // 순서 주의! singleton이 먼저 와야한다.
export default class CounterStore {
  count = 0;

  // state = {
  //   x: 1;
  // }

  @Action()
  increase(step = 1) {
    this.count += step;
    // this.state = {...this.state, x: this.state.x + 1};
  }

  @Action()
  decrease(step = 1) {
    this.count -= step;
  }
}

// useCounterStore
import {container} from 'tsyringe';

import {useStore} from 'usestore-ts';

import CounterStore from '../stores/CounterStore';

export default function useCounterStore() {
  const store = container.resolve(CounterStore);

  return useStore(store);
}


// Counter.tsx
import useCounterStore from '../hooks/useCounterStore';

export default function Counter(){
  const [{count}] = useCounterStore();
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
  const [{count}, store] = useCounterStore();

  return (
    <div>
      <p>{count}</p>
      <button type="button" onClick={()=> store.increase()}>
        Increase
      </button>
      <button type="button" onClick={()=> store.increase(10)}>
        Increase 10
      </button>
       <button type="button" onClick={() => store.decrease()}>
        Decrease
      </button>
      <button type="button" onClick={() => store.decrease(10)}>
        Decrease 10
      </button>
    </div>
  )
}
```

`usestore-ts`에서 비동기 함수에 `@Action`을 붙이면 중간에 promise 함수를 리턴하기 때문에
별도로 Action을 만들어서 사용하면 편하다.

### useSyncExternalStore

`useSyncExternalStore`은 외부 스토어를 구독할 수 있는 [React 내장 Hooks](https://react-ko.dev/reference/react/useSyncExternalStore)이다.

```Javascript
import { useSyncExternalStore } from 'react';
import { todosStore } from './todoStore.js';

function TodosApp() {
  const todos = useSyncExternalStore(todosStore.subscribe, todosStore.getSnapshot);
  // ...
}
```

이런식으로 사용한다.

`subscribe`는 스토어를 구독하고 구독을 취소하는 함수를 반환해야한다.
`getSnapshot`는 저장소에서 데이터의 스냅샷을 읽어야 한다.

`getServerSnapshot`은 옵셔널한 값이다. 서버 렌더링 및 클라이언트에서 서버 렌더링 컨텐츠를 하이드레이션하는 동안에만 사용된다. 서버 스냅샷은 클라이언트와 서버 간 동일해야하고 직렬화되어 서버에서 클라이언트로 전달된다.
이 인수를 생략하면 서버에서 구성 요소를 렌더링할 때 오류가 ㅅ발생된다.

`useSyncExternalStore` Hook을 사용한 예제이다.

```Javascript
// App.js
import { useSyncExternalStore } from 'react';
import { todosStore } from './todoStore.js';

export default function TodosApp() {
  const todos = useSyncExternalStore(todosStore.subscribe, todosStore.getSnapshot);
  return (
    <>
      <button onClick={() => todosStore.addTodo()}>Add todo</button>
      <hr />
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>{todo.text}</li>
        ))}
      </ul>
    </>
  );
}

// todoStore.js
let nextId = 0;
let todos = [{ id: nextId++, text: 'Todo #1' }];
let listeners = [];

export const todosStore = {
  addTodo() {
    todos = [...todos, { id: nextId++, text: 'Todo #' + nextId }]
    emitChange();
  },
  subscribe(listener) {
    listeners = [...listeners, listener];
    return () => {
      listeners = listeners.filter(l => l !== listener);
    };
  },
  getSnapshot() {
    return todos;
  }
};

function emitChange() {
  for (let listener of listeners) {
    listener();
  }
}

```