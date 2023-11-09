# 학습 키워드

- usehooks-ts
    - useBoolean
    - useEffectOnce
    - useFetch
    - useInterval
    - useEventListener
    - useLocalStorage
    - useDarkMode
- swr
- react-query

## ✔️ 키워드 정리

### usehooks-ts

자주 사용할법한 기능들을 커스텀 훅으로 작성해둔 라이브러리인데 타입스크립트 뿐만 아니라 자바스크립트에서도 사용 가능하다.

이 명령어를 사용해서 설치할 수 있다.

```Bash
npm i usehooks-ts
```

코드가 다 오픈되어있어서 커스텀 훅 작성할 때 참고하기 좋아보인다!
다른 라이브러리들은 git에 들어가서 한참 뒤져봐야 겨우 나오는데.. 너무 좋다ㅠㅠ

#### useBoolean

`boolean` 타입의 변수를 다룰 땐 `toggle`과 같이 의도가 명확한 함수를 쓰는게 좋다.

#### useEffectOnce

의존성 배열을 빈 배열로 넣어서 한 번만 실행하는 Effect를 잡아줄 때가 많은데, [useEffectOnce](https://usehooks-ts.com/react-hook/use-effect-once)를 쓰면 더 명확히 드러난다.

로직은 똑같지만, 이름을 명확히 하는 습관을 들이면 좋다.

```Javascript
// 적용 예시
import {useState} from 'react';
import {useEffectOnce} from 'usehooks-ts';

import Product from '../types/Product';

export default function useFetchProducts() {
    const [products, setProducts] = useState<Product[]>([]);

    useEffectOnce(()=> {
        const fetchProducts = async () => {
            const url = 'http://localhost:3000/products';
            const response = await fetch(url);
            const data = await response.json();
            setProducts(data.products);
        }

        fetchProducts();
    })
}
```

#### useFetch

fetch를 정말 간단하게 사용하기 좋다.
요청 헤더에 인증 토큰도 전달할 수 있도록 되어있어서 여러모로 요긴한 [useFetch](https://usehooks-ts.com/react-hook/use-fetch)이다.

#### useInterval

리액트에서 setInterval을 사용할 때 주의해야할 부분이 몇 가지 있다.  [useInterval](https://usehooks-ts.com/react-hook/use-interval)은 동적으로 작동해서 리액트에서 setInterval을 사용해야할 때는 `useInterval`을 사용하는게 좋다.

#### useEventListener

[useEventListener](https://usehooks-ts.com/react-hook/use-event-listener)는 모든 종류의 이벤트를 확인할 수 있다.
특히 dispatchEvent로 전달되는 커스텀 이벤트에 반응하기 좋아서 유용하게 쓸 수 있다!

#### useLocalStorage

[useLocalStorage](https://usehooks-ts.com/react-hook/use-local-storage)은 화면이 새로고침 되어도 상태가 유지되도록 로컬 저장소를 사용해서 상태를 유지한다.

첫번째 매개변수에 스토리지 key를 전달해야한다는 부분을 제외하면 useState와 사용법이 동일한 방식으로 사용된다.

#### useDarkMode

[useDarkMode](https://usehooks-ts.com/react-hook/use-dark-mode)는 다크모드인지 아닌지 확인해주는 훅인데, 웹사이트에 다크모드를 적용한다면 요긴하게 쓰일 것 같다.

### swr

[swr](https://swr.vercel.app/ko)은 백그라운드에서 캐시를 재검증하는 동안에 기존에 캐시 데이터를 사용하여 화면을 그려준다. 만약 에러를 반환하더라도 캐시된 데이터를 활용할 수 있게 함으로써 불필요한 데이터 호출과 렌더링에 영향 없이 효율적으로 동작한다.

기본구성은 이렇다.

```Javascript
const { data, error, isValidating, mutate } = useSWR(key, fetcher, options)
```
한 번도 써보지는 않았는데, 리액트 쿼리와 비슷한 것 같다. Next.js 만든 팀에서 만들었다고 하니 Next.js에서 한 번 써봐야겠다.

### react-query

 [React Query](https://tanstack.com/)는 React Application에서 서버 상태를 불러오고, 캐싱하며, 지속적으로 동기화하고 업데이트하는 작업을 도와준다.

React query는 데이터를 캐싱한다는 장점이 있다. 캐싱을 통해 동일한 데이터에 대한 반복적인 비동기 데이터 호출을 방지하고, 서버에 대한 부하를 줄이는 좋은 결과를 가져온다.

React query는 최신의 데이터를 fresh한 데이터, 기존에 있던 데이터를 stale한 데이터라고 말한다.

query key로 query를 관리하여 효율적으로 사용이 가능하다.

## 참고

<https://usehooks-ts.com/><br/>
<https://velog.io/@soryeongk/SWRBasic><br/>
