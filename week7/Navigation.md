# 학습 키워드

- Web APIs - History
- React Router - NavLink, Link, Navigate, useNavigate

## ✔️ 키워드 정리

### Web APIs - History

[History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API)는 전역 객체를 통해 브라우저의 세션 기록에 대한 액세스를 제공한다.

사용자 기록으 앞뒤로 이동하는 것은 `back()`, `forward()` 그리고 `go()`메서드를 사용한다.

뒤로 이동하려면 `history.back()`;
앞으로 이동하려면 `history.forward()`

특정 지점으로 이동하려면 `history.go(-1 || 1)`


```Javascript
window.addEventListener("popstate", (event) => {
  alert(
    `location: ${document.location}, state: ${JSON.stringify(event.state)}`,
  );
});

history.pushState({ page: 1 }, "title 1", "?page=1");
history.pushState({ page: 2 }, "title 2", "?page=2");
history.replaceState({ page: 3 }, "title 3", "?page=3");
history.back(); // alerts "location: http://example.com/example.html?page=1, state: {"page":1}"
history.back(); // alerts "location: http://example.com/example.html, state: null"
history.go(2); // alerts "location: http://example.com/example.html?page=3, state: {"page":3}"

```

이런식으로 사용 가능하다.

### React Router - NavLink, Link, Navigate, useNavigate

`Link`는 사용자가 클릭하거나 탭하여 다른 페이지로 이동할 수 있는 요소이다.

`NavLink`는 `Link`요소와 비슷한데 활성화 상태일 때 active 클래스가 추가된다.
스타일링에 유용한 태그이다.

`Navigate`요소는 렌더링될 때 현재 위치를 변경한다. `useNavigate`를 둘러싼 component Wrapper이며 `props`와 동일한 모든 인수를 허용한다.

이렇게 사용한다.

```Javascript
import { Navigate } from 'react-router-dom';

function Func() {

    const onClickImg = () => {
    return <Navigate to="/login" />;
  }

  return (
  	<img src={...} alt={...} onClick={onClickImg} />
  );
}

export default Func;
```

`useNavigate`는 첫 번째 인자로는 주소를 받고 두 번째 인자로 {replace, state} 인수를 사용힌다.

`navigate("../success",  { replace: true});`

replace 값으로 `true`를 사용한다면, navigate에 적힌 주소로 넘어간 후 뒤로가기를 하더라도 바로 이전 페이지로 돌아가지 않고 메인 페이지('/')로 돌아간다. `false`는 뒤로가기가 가능하다.