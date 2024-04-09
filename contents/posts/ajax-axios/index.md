---
title: '🦚 Ajax와 fetch, Axios는 어떻게 다를까?'
description: Ajax와 Fetch, Axios의 기본 개념과 사용법에 대해 알아보자.
date: 2024-03-13
update: 2024-03-13
tags:
  - ajax
  - fetch
  - axios
---

## Ajax (Asynchronous Javascript and XML)

Ajax는 웹 페이지 전체를 다시 로딩하지 않고도, 웹 페이지의 일부분만을 갱신할 수 있다. 즉 Ajax를 이용하면 백그라운드 영역에서 서버와 통신하여, 그 결과를 웹페이지의 일부분만 표시 할 수 있다.

### 동작 방식

Ajax는 `XMLHttpRequest` 객체를 사용하여 서버와 통신한다. 이 객체를 통해 데이터를 비동기적으로 교환할 수 있으며, 페이지 전체를 새로고침하지 않고도 일부분만을 업데이트할 수 있다.

### 사용법

```js
const xhr = new XMLHttpRequest(); // XMLHttpRequest 객체 생성

xhr.open('GET', 'url-to-the-server', true); // 요청 초기화 (HTTP 요청 메서드, 요청을 보낼 서버의 url, 비동기적으로 요청할 것인지 boolean)
// 응답 처리 이벤트 핸들러 (xhr.readyState === 4는 요청 완료되었음을 나타냄)
xhr.onreadystatechage = function () {
  if (xhr.readyState === 4 && xhr.status === 200) {
    console.log(xhr.responseText); // 서버로부터 받은 데이터 처리
  }
};

xhr.send(); // 요청 전송
```

### 한계

Ajax는 `XMLHttpRequest` 객체를 사용하여 비동기 통신을 구현한다. 하지만 사용법이 복잡하고, 콜백 지옥(callback hell)과 같은 문제가 발생할 수 있다. 또한 JSON 데이터를 처리하기 위한 추가적인 변환 작업이 필요하다.

### Fetch의 등장 배경

Fetch API는 `Promise`를 기반으로 하여 비동기 통신을 더욱 간결하고 직관적으로 만들 수 있게 해준다. Fetch는 `XMLHttpRequest`보다 더 유연하고 강력한 기능을 제공하며, 직접적으로 JSON을 지원하여 데이터 처리가 훨씬 간편해졌다.

## Fetch API

Fetch API는 브라우저의 `window` 객체에 내장되어 있으며, `Request`와 `Response` 객체를 사용하여 요청과 응답을 쉽게 처리할 수 있다.

### 사용법

```js
fetch(url, options)
  .then((response) => console.log('response: ', response.json())) // JSON 데이터로 변환
  .catch((error) => console.log('error: ', error));
```

fetch는 첫번째 인자로 `url`, 두번째 인자로 `옵션 객체`를 받고, `Promise` 타입의 객체를 반환한다. 반환된 객체는 API 호출이 성공했을 경우에는 응답(response) 객체를 `resolve`하고, 실패했을 경우에는 예외(error) 객체를 `reject`한다.

### 한계

Fetch API는 많은 개선점을 제공하지만, 여전히 몇 가지 한계가 있다.  
예를 들어, Fetch는 요청 시간 초과(timeouts)를 직접적으로 지원하지 않는다. 또한 브라우저 호환성 문제와 일부 기능(진행 상태 추적 등)에 대한 제한이 있을 수 있다.

### Axios의 등장 배경

Axios는 Fetch의 모든 장점을 가지면서도, Fetch의 한계를 극복하기 위해 등장했다. Axios는 요청 시간 초과 설정, 요청 취소, HTTP 상태 코드에 따른 자동 변환, 진행 상태 추적 등 추가적인 기능을 제공한다. 또한 브라우저뿐만 아니라 Node.js 환경에서도 사용할 수 있어서 서버 사이드와 클라이언트 사이드 모두 사용된다.

## Axios

Axios는 HTTP 요청을 보내기 위한 자바스크립트 라이브러리이다. Axios는 내부적으로 `XMLHttpRequest`를 사용하지만, `Promise` 기반의 API를 제공하여 보다 쉬운 비동기 처리를 가능하게 한다. 또한, 요청과 응답을 JSON 형태로 자동 변환해주거나 에러 처리 등과 추가적인 기능을 제공한다. 보통 아래와 같이 `async/await`와 함께 사용한다.

Fetch API와 비교했을 때 차이점을 좀 더 자세히 알아보자면, 아래와 같다.

- **자동 JSON 변환**

  Axios는 `response`를 자동으로 JSON 형태로 변환해준다. 반면, Fetch API는 `response`가 도착했을 때, `.json()`을 호출하여 수동으로 변환해야한다.

- **에러 처리**

  Fetch API는 네트워크 오류가 발생하지 않는 한 요청 실패를 액션이 실패로 간주하지 않는다. 즉, 404나 500 같은 서버 에러 상태에서도 `.then()`을 실행한다. 반면, Axios는 2xx 범위 외의 HTTP 상태 코드를 받으면 자동으로 에러를 발생시킨다.

- **브라우저 지원**

  Fetch API는 일부 구형 브라우저에서는 기본적으로 지원되지 않을 수 있다. 반면, Axios는 모든 브라우저에서 작동하도록 Promise API를 사용한다.

- **timeout 설정**

  Axios는 요청 타임아웃을 설정하는 옵션이 내장되어 있다. Fetch API에서는 이를 직접 구현해야한다.

### 사용법

```js
const fetchData = async () => {
  try {
    const response = await axios.get('url-to-the-server');
    console.log(response.data);
  } catch (error) {
    console.error('Error! : ', error);
  }
};
```

더 자세한 사용법을 알고싶다면, [**⚠️ 자바스크립트의 예외 처리**](https://leedawnn.github.io/error-handling/) 글을 참고!
