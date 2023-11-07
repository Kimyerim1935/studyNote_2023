# 학습 키워드

- Fetch API 란
- Promise
- ReadableStream
- Unicode
- CORS 란

## ✔️ 키워드 정리

### Fetch API 란

[fetch API](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API)<br/>
[Fetch 사용하는 방법](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Using_Fetch)

원격 API를 간편하게 호출할 수 있도록 브라우저에서 제공하는 함수이다. fetch 함수 이외에도 Ajax나 Axios를 많이 사용한다.

fetch 함수는 이렇게 사용하면 된다.

```Javascript
fetch(url, options)
  .then((response) => console.log("response:", response))
  .catch((error) => console.log("error:", error));

// example
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

fetch 함수는 응답 받은 데이터를 json으로 변경해줘야한다.

만약 다른 HTTP Method를 사용하고 싶다면, 이렇게 사용하면 된다.

```Javascript
const response = fetch(url, {
	method: 'POST',
});
```

### Promise

[promise 문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)
promise는 비동기 작업을 할 때 사용된다.

promise는 세 가지의 상태를 가진다.
1. pending(대기): 초기 상태
2. fulfilled(이행): 성공적으로 완료된 상태
3. rejected(거부): 실패한 상태

promise는 이렇게 사용하면 된다.

```Javasrcipt
const myPromise = new Promise((resolve, reject) => {
  ...
})
```

성공했을 경우엔 `.then()` 안에 성공 시 실행해야할 코드를 작성하고, 실패했을 경우엔 `.catch` 안에 실패 시 실행해야하는 코드를 작성해주면 된다.


```Javascript
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject(new Error());
  }, 1000);
});

myPromise
  .then(n => {         // 성공
    console.log(n);
  })
  .catch(error => {    // 실패
    console.log(error);
  });
```

### ReadableStream

```Javascript
const response = await fetch('http://localhost:3000/products');
const data = await response.json();
```

이 코드에서 `response.body`는 ReadableStream이다.

ReadableStream 인터페이스는 바이트 데이터를 읽을 수 있는 스트림을 제공한다.
Fetch API는 Response 객체의 body 속성을 통해서 구체적인 인스턴스를 제공한다.

이렇게 사용한다.

```Javascript
fetch('http://localhost:3000/products');
// → Promise

await fetch('http://localhost:3000/products');
// → Response

const response = await fetch('http://localhost:3000/products');
// → response.body는 ReadableStream

const reader = response.body.getReader();

const chunk = await reader.read();
// → chunk.value는 Uint8Array 타입.
// → 원래는 chunk.done이 true일 때까지 반복해야 한다.

const body = new TextDecoder().decode(chunk.value);

const data = JSON.parse(body);
```

[TextDecoder](https://ko.javascript.info/text-decoder)는 주어진 버퍼와 인코딩으로 실제 자바스크립트 문자열로 읽을 수 있게 해준다.

인코딩은 정해진 규칙에 따라 코드화, 암호화, 부호화 하는 것을 말한다.
정보의 형태 표준화, 보안, 저장 공간 절약 등을 위해 주로 한다.

```Javascript
let decoder = new TextDecoder([label], [options]);
```

- label: 기본적인 인코딩 방식은 `utf-8`이지만 다른 인코딩 방식도 지원한다.
- options: 선택적으로 사용 가능한 항목이다.

디코딩은 인코딩과 반대되는 개념을 갖고 있다. 복호화, 역코드화의 의미를 갖고 있으며 데이터를 읽어오기 위해 주로 한다.

객체 디코딩은 이렇게 한다.

```Javascript
let str = decoder.decode([input], [options]);
```

- input:디코딩할 `BufferSource`를 입력한다.
- options: 선택적으로 사용 가능한 항목이다.

반대로 인코딩하는 방식은 이렇다.

```Javascript
let encoder = new TextEncoder();

let encoder = new TextEncoder();

let uint8Array = encoder.encode("Hello");
alert(uint8Array); // 72,101,108,108,111
```

디코딩 할 경우와 달리 인코딩 시에는 `utf-8` 형식만 지원한다.

### Unicode

유니코드 표준은 컴퓨터 처리를 위한 텍스트 표현에 사용되는 범용 문자 인코딩 표준이다.
유니코드는 `utf-8`, `utf-16`, `utf-32`의 인코딩 체계를 사용하여 인코딩 될 수 있다.

기본 인코딩 양식은 16비트이다.

유니코드는 내부 처리 및 저장을 위한 기본 체계가 되었다. 많은 텍스트가 여전히 전통적인 인코딩으로 저장되지만 유니코드는 거의 독점적으로 새로운 정보 처리 시스템을 구축하는 데 사용된다.

인코딩, 디코딩이 잘 사용되는 예시 중에 하나라고 볼 수 있다.

### CORS 란

웹 브라우저는 [동일 출처 정책](https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy)에 따라 웹 페이지와 리소스를 요청한 곳이 서로 다른 출처일 때 서버에서 얻어온 결과를 사용하지 못하도록 막는다.
이미 요청과 응답된 데이터는 받아왔지만 사용 할 수 없는 상태!

REST API 서버에서 Headers에 `Access-Control-Allow-Origin` 속성을 추가해주면 된다.

Express에서는 [CORS 미들웨어](https://expressjs.com/en/resources/middleware/cors.html)를 설치해서 사용하면 된다.

이렇게 작성해주면 된다

```Javascript
const app = express();
app.use(cors());

app.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});

```

## 참고

<https://www.daleseo.com/js-window-fetch/><br/>
<https://learnjs.vlpt.us/async/01-promise.html><br/>
<https://codingpractices.tistory.com/entry/%EC%9D%B8%EC%BD%94%EB%94%A9-vs-%EB%94%94%EC%BD%94%EB%94%A9-%EC%A0%95%ED%99%95%ED%95%98%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0><br/>
<https://academic-accelerator.com/encyclopedia/kr/unicode><br/>
<https://aws.amazon.com/ko/what-is/cross-origin-resource-sharing/><br/>