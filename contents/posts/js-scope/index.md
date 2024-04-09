---
title: '🔭 자바스크립트의 스코프(Scope)'
description: lexcial scoping이 뭘까요?
date: 2024-03-27
update: 2024-03-27
tags:
  - javascript
  - scope
  - lexical-scoping
series: 'javascript'
---

## 스코프(Scope)란?

![](https://blog.hubspot.com/hs-fs/hubfs/JavaScript_Scope-1.webp?width=650&height=450&name=JavaScript_Scope-1.webp)

자바스크립트에서 스코프(Scope)는 변수와 함수 등의 식별자가 유효한 범위를 의미한다. 스코프는 크게 **전역 스코프(Global Scope)**, **지역 스코프(Local Scope)**로 나뉜다.

- **전역 스코프(Global scope)**

  ```js
  var pet = 'dog';

  function printPet() {
    console.log(pet); // 'dog'
  }
  ```

  전역 스코프는 말 그대로 전역에 선언되어 있어 어느 곳에서든지 해당 변수에 접근할 수 있다는 의미다.

- **지역 스코프(Local scope or Function-level scope)**

  ```js
  {
    var pet = 'cat';
  }

  console.log(pet); // undefined
  ```

  지역 스코프는 해당 지역에서만 접근할 수 있다.

  자바스크립트에서 함수를 선언하면 함수를 선언할 때마다 새로운 스코프를 생성하게 된다. 그러므로 함수 몸체에 선언한 변수는 해당 함수 안에서만 접근할 수 있는데, 이걸 **함수 스코프(Function scope)**라고 한다. 함수 스코프가 바로 지역 스코프의 예라고 할 수 있겠다.

모든 변수는 스코프를 갖는다. 변수의 관점에서 스코프를 구분하면 다음과 같이 2가지로 나눌 수 있다.

- **전역 변수(Global variable)**

  전역에서 선언된 변수이며 어디에든 참조할 수 있다.

- **지역 변수(Local variable)**

  지역(함수) 내에서 선언된 변수이며 그 지역과 그 지역의 하부 지역에서만 참조할 수 있다.

**변수는 선언 위치(전역 또는 지역)에 의해 스코프를 가지게 된다. 즉, 전역에서 선언된 변수는 전역 스코프를 갖는 전역 변수이고, 지역(자바스크립트의 경우 함수 내부)에서 선언된 변수는 지역 스코프를 갖는 지역 변수가 된다.**

**전역 스코프를 갖는 전역 변수는 전역에서 참조할 수 있다. 지역(함수 내부)에서 선언된 지역 변수는 그 지역과 그 지역의 하부 지역에서만 참조할 수 있다.**

## 자바스크립트 스코프의 특징

자바스크립트의 스코프는 타 언어와는 다른 특징을 가지고 있다.

대부분의 C-family language는 **블록 레벨 스코프(Block-level scope)**를 따른다. 블록 레벨 스코프란 코드 블록`({...})`내에서 유효한 스코프를 의미한다.

하지만 자바스크립트는 **함수 레벨 스코프(Function-level scope)**를 따른다. 함수 레벨 스코프란 함수 코드 블록 내에서 선언된 변수는 함수 코드 블록 내에서만 유효하고 함수 외부에서는 유효하지 않다(참조할 수 없다)는 것이다.

단, ES6에서 도입된 `let`과 `const`을 사용하면 블록 레벨 스코프를 사용할 수 있다.

```js
var x = 0;
{
  var x = 1;
  console.log(x); // 1
}
console.log(x); // 1

let y = 0;
{
  let y = 1;
  console.log(y); // 1
}
console.log(y); // 0
```

## 비 블록 레벨 스코프(Non Block-level scope)

```js
if (true) {
  var x = 5;
}

console.log(x);
```

변수 x는 코드 블록 내에서 선언되었다. 하지만 자바스크립트는 블록 레벨 스코프를 사용하지 않으므로 **함수 밖에서 선언된 변수는 코드 블록 내에서 선언되었다할 지라도 모두 전역 스코프**를 갖게된다. 따라서 변수 x는 전역 변수이다.

## 함수 레벨 스코프(Function-level scope)

```js
var a = 10; // 전역 변수

(function () {
  var b = 20; // 지역 변수
})();

console.log(a); // 10
console.log(b); // "b" is not defined
```

자바스크립트는 함수 레벨 스코프를 사용한다. 즉, 함수 내에서 선언된 매개변수와 변수는 함수 외부에서는 유효하지 않다. 따라서 변수 b는 지역 변수이다.

```js
var x = 'global';

function foo() {
  var x = 'local';
  console.log(x);
}

foo(); // local
console.log(x); // global
```

전역 변수 `x`와 지역 변수 `x`가 중복 선언되었다. 전역 영역에서는 전역 변수만이 참조 가능하고, 함수 내 지역 영역에서는 전역과 지역 변수 모두 참조 가능하나 위 예제와 같이 변수명이 중복된 경우, 지역 변수를 우선하여 참조한다.

다음은 함수 내에 존재하는 내부 함수의 경우를 살펴보자.

```js
var x = 'global';

function foo() {
  var x = 'local';
  console.log(x); // 1) local

  // 내부 함수
  function bar() {
    console.log(x); // 2) local
  }

  bar();
}

foo();
console.log(x); // global
```

내부 함수는 자신을 포함하고 있는 외부 함수의 변수에 접근할 수 있다. 클로저와 같이 내부 함수가 더 오래 생존하는 경우, 타 언어와는 다른 움직임을 보인다.

함수 `bar`에서 참조하는 변수 `x`는 함수 `foo`에서 선언된 지역 변수이다. 이는 실행 컨텍스트의 스코프 체인에 의해 참조 순위에서 전역변수 x가 뒤로 밀렸기 때문이다.

https://poiemaweb.com/js-scope 이어서,,
https://blog.hubspot.com/website/javascript-scope
https://www.zerocho.com/category/Javascript/post/5740531574288ebc5f2ba97e
