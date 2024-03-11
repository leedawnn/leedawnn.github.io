---
title: "⚠️ 자바스크립트의 예외 처리"
description: try~catch문과 async/await가 필요한 이유에 대해 자세히 알아보자.
date: 2024-03-07
update: 2024-03-07
tags:
  - javascript
  - try~catch
  - async
  - await
series: "javascript"
---

자바스크립트에서 에러가 발생하면 스크립트는 죽고, 콘솔에 에러가 출력된다.  
그러나 `try...catch`문을 사용하면 스크립트가 죽는 걸 방지하고, 에러를 잡아서(catch) 예외 처리를 할 수 있게 된다.

## try...catch문

```js
try {
  // ...
} catch (error) {
  // 에러 핸들링
}
```

**try...catch문의 동작은 다음과 같다.**

1. 먼저, `try {...}` 안의 코드가 실행된다.
2. 에러가 없다면, `try` 안의 마지막 줄까지 실행되고, `catch` 블록은 건너뛴다.
3. 에러가 있다면, `try` 안 코드의 실행이 중단되고, `catch(error)` 블록으로 제어 흐름이 넘어간다. 변수 error는 무슨 일이 일어났는지에 대한 설명이 담긴 에러 객체를 포함한다.

`try {...}` 블록 안에서 에러가 발생해도 `catch`에서 에러를 처리하기 때문에 스크립트는 죽지 않는다.

### `try...catch`는 오직 런타임 에러에만 동작한다.

`try...catch`는 실행 가능한(runnable) 코드에만 동작한다. 실행 가능한 코드는 문법적으로 맞는 자바스크립트 코드를 의미한다.  
자바스크립트 엔진은 코드를 읽고 난 후 코드를 실행한다. 코드를 읽는 중에 발생하는 에러는 'parse-time 에러'라고 부르는데, 엔진은 이 코드를 이해할 수 없기 때문에 parse-time 에러는 코드 안에서 복구가 불가능하다.

`try...catch`는 유효한 코드에서 발생하는 에러만 처리할 수 있다. 이런 에러를 '런타임 에러(runtime error)' 혹은 '예외(exception)'라고 부른다.

### `try...catch`문은 동기적으로 동작한다.

`setTimeout`처럼 스케줄 된 코드에서 발생한 예외는 `try...catch`문에서 잡아낼 수 없다.

```js
try {
  setTimeout(function () {
    noSuchVariable // 스크립트는 여기서 죽는다.
  }, 1000)
} catch (e) {
  alert("작동 멈춤")
}
```

`setTimeout`에 넘겨진 익명 함수는 `try...catch`를 떠난 다음에서야 실행되기 때문이다.  
스케줄 된 함수 내부의 예외를 잡으려면, `try...catch`를 반드시 함수 내부에 구현해야한다.

```js
setTimeout(function () {
  try {
    noSuchVariable // 이제 try...catch에서 에러를 핸들링 할 수 있다!
  } catch {
    alert("에러를 잡았습니다!")
  }
}, 1000)
```

### 에러 객체

에러가 발생하면 자바스크립트는 에러 상세내용이 담긴 객체를 생성한다. 그 후, `catch` 블록에 이 객체를 인수로 전달한다.

```js
try {
  // ...
} catch (e) {
  // <-- 에러 객체
  // ...
}
```

내장 에러 전체와 에러 객체는 두 가지 주요 프로퍼티를 가진다.

- `name`
  에러 이름. 정의 되지 않은 변수 때문에 발생한 에러라면 `"ReferenceError"`가 이름이 된다.
- `message`
  에러 상세 내용을 담고 있는 문자 메시지.

예시:

```js
try {
  lalala // 에러, 변수가 정의되지 않음!
} catch (e) {
  alert(e.name) // ReferenceError
  alert(e.message) // lalala is not defined

  // 에러 전체를 보여줄 수도 있다.
  // 이때, 에러 객체는 "name: message" 형태의 문자열로 변환된다.
  alert(e) // ReferenceError: lalala is not defined
}
```

### `throw` 연산자

`throw`문의 주요 용도는 크게 두 가지가 있다.

1. 커스텀 에러 메시지
   throw문을 사용하면 특정 조건에서 커스텀 에러 메시지를 생성할 수 있다. 이는 코드를 디버깅하는데 도움이 된다.  
   또한, 특정 조건에서 발생하는 에러를 사용자에게 더 친절하게 전달할 수 있게 해준다.

```js
if (!isValid) {
  throw new Error("입력 값이 유효하지 않습니다.")
}
```

2. 예외를 강제로 발생시키기
   코드의 실행을 강제로 중단하고, 해당 에러를 `catch` 블록으로 전달할 수 있다. 이는 특정 조건에서 프로그램의 실행을 중단하고, 이를 적절하게 처리하고 싶을 때 유용하다.

### 에러 다시 던지기

```js
let json = '{ "age": 30 }' // 불완전한 데이터

try {
  user = JSON.parse(json) // user 앞에 let을 붙이는 걸 잊음

  // ...
} catch (e) {
  alert("JSON Error: " + e) // JSON Error: ReferenceError: user is not defined
  // 실제로는 JSON Error가 아님
}
```

위 코드에서 '불완전한 데이터'를 다루려는 목적으로 `try...catch`를 사용했다. 그런데 catch는 원래 try 블록에서 발생한 모든 에러를 잡으려는 목적으로 만들어졌다. 그런데 위 예시에서 catch는 예상치 못한 에러를 잡아주긴 했지만, 에러 종류와 상관없이 `"JSON Error"` 메시지를 보여준다. 이렇게 에러 종류와 관계없이 동일한 방식으로 에러를 처리하는 것은 디버깅을 어렵게 만들기 때문에 좋지 않다.

이런 문제를 피하고자 '**다시 던지기(rethrowing)**' 기술을 사용한다. 규칙은 간단하다.

**catch는 알고 있는 에러만 처리하고 나머지는 '다시 던져야'한다.**

1. catch가 모든 에러를 받는다.
2. catch(e) {...} 블록 안에서 에러 객체 e를 분석한다.
3. 에러 처리 방법을 알지 못하면 throw e를 한다.

보통 에러 타입을 `instanceof` 명령어로 체크한다.

```js
try {
  user = {
    /*...*/
  }
} catch (e) {
  if (e instanceof ReferenceError) {
    alert("ReferenceError") // 정의되지 않은 변수에 접근하여 'ReferenceError' 발생
  }
}
```

## async와 await

async와 await를 사용하면 Promise를 좀 더 편하게 사용할 수 있다.

### async 함수

```js
async function f() {
  return 1
}
```

`async`는 function 앞에 위치한다.

function 앞에 `async`를 붙이면 해당 함수는 항상 Promise를 반환한다. Promise가 아닌 값을 반환하더라도 이행(resolved) 상태의 Promise로 값을 감싸 이행된 Promise가 반환되도록 한다.

```js
async function f() {
  return 1
}

f().then(alert) // 1
```

`async`가 붙은 함수는 반드시 Promise를 반환하고, Promise가 아닌 것은 Promise로 감싸 반환한다. 또다른 키워드 `await`는 `async` 함수 안에서만 동작한다.

### await

```js
// await는 async 함수 안에서만 동작한다.
let value = await promise
```

자바스크립트는 `await` 키워드를 만나면 Promise가 처리될 때까지 기다린다. 결과는 그 이후 반환된다.

1초 후 이행되는 Promise를 예시로 `await`가 어떻게 동작하는지 살펴보자.

```js
async function f() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("완료!"), 1000)
  })

  let result = await promise // Promise가 이행될 때까지 기다림

  alert(result) // 완료!
}
```

함수를 호출하고, 함수 본문이 실행되는 도중에 `await` 키워드를 만나면 실행이 잠시 중단되었다가 Promise가 처리되면 실행이 재개된다. 이때 Promise 객체의 result 값이 변수 result에 할당된다. 따라서 위 예시를 실행하면 1초 뒤에 `"완료!"`가 출력된다.

`await`는 말 그대로 Promise가 처리될 때까지 함수 실행을 기다리게 만든다. Promise가 처리되면 그 결과와 함께 실행이 재개된다. Promise가 처리되길 기다리는 동안엔 엔진이 다른 일(다른 스크립트를 실행, 이벤트 처리 등)을 할 수 있기 때문에, CPU 리소스가 낭비되지 않는다.

`await`는 `promise.then`보다 더 세련되게 Promise의 result값을 얻을 수 있도록 하는 문법이다.
`promise.then`보다 가독성이 좋고 사용하기도 쉽다.

### 에러 핸들링

Promise가 정상적으로 이행되면 `await promise`는 Promise 객체의 result에 저장된 값을 반환한다. 반면 Promise가 거부되면 마치 throw문을 작성한 것처럼 에러가 던져진다.

```js
async function f() {
  await Promise.reject(new Error("에러 발생!"))
}

// 위 코드는 아래 코드와 동일하다.
async function f() {
  throw new Error("에러 발생!")
}
```

실제 상황에선 Promise가 거부 되기 전에 약간의 시간이 지체되는 경우가 있다. 이런 경우엔 `await`가 에러를 던지기 전에 지연이 발생한다.

await가 던진 에러는 throw가 던진 에러를 잡을 때처럼 `try...catch`를 사용해 잡을 수 있다.

```js
async function f() {
  try {
    let response = await fetch("http://유효하지-않은-주소")
  } catch (e) {
    alert(e) // TypeError: failed to fetch
  }
}

f()
```

`try...catch`가 없으면 아래 예시의 async 함수 `f()`를 호출해 만든 Promise가 거부 상태가 된다. `f()`에 `.catch`를 추가하면 거부된 Promise를 처리할 수 있다.

```js
async function f() {
  let response = await fetch("http://유효하지-않은-주소")
}

// f()는 거부 상태의 프라미스가 된다.
f().catch(alert) // TypeError: failed to fetch
```

### async/await는 Promise.all과도 함께 쓸 수 있다.

여러 개의 Promise가 모두 처리되길 기다려야 하는 상황이라면 이 Promise들을 `Promise.all`로 감싸고 여기에 `await`를 붙여 사용할 수 있다.

```js
// Promise 처리 결과가 담긴 배열을 기다린다.
let results = await Promise.all([
  fetch(url1),
  fetch(url2),
  ...
])
```

실패한 Promise에서 발생한 에러는 보통 에러와 마찬가지로 `Promise.all`로 전파된다. 에러 때문에 생긴 예외는 `try...catch`로 감싸 잡을 수 있다.

## 그래서 실무에서는 어떻게 써야해?

보통 `axios`를 이용해서 API 요청을 보내고 받아온다. 아래는 GPT-4에게 try~catch문과 async/await를 적절하게 사용한 best practice 작성을 부탁한 코드다.

### 1. 타입 정의

```ts
interface ApiResponse {
  success: boolean
  data: any // 실제 응답 구조에 맞게 타입을 상세하게 정의
}
```

### 2. Axios 인스턴스 생성

```ts
import axios from "axios"

const client = axios.create({
  baseURL: "https://api.example.com", // 보통 서버리스 함수 등으로 API 숨김. 여기선 skip
  headers: {
    "Content-Type": "application/json",
  },
})
```

### 3. API 요청 함수 작성

```ts
async function fetchSomeData(): Promise<ApiResponse> {
  try {
    const response = await client.get<ApiResponse>("/data")
    return response.data
  } catch (error) {
    if (axios.isAxiosError(error)) {
      // Axios 에러 처리
      console.error("Axios error:", error.response)
    } else {
      // 기타 에러 처리
      console.error("Unexpected error:", error)
    }
    throw error
  }
}
```

### 4. 사용 예시

```ts
async function main() {
  try {
    const data = await fetchSomeData()
    console.log(data)
  } catch (error) {
    console.error("Error fetching data:", error)
  }
}

main()
```
