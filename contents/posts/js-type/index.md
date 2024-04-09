---
title: '🙌 값에 의한 전달(Pass by Value)와 참조에 의한 전달(Pass by Reference) '
description: 자바스크립트에서 값에 의한 전달과 참조에 의한 전달 방식을 알아보자.
date: 2024-03-21
update: 2024-03-21
tags:
  - javascript
  - pass by value
  - pass by reference
series: 'javascript'
---

알고리즘을 풀면서 아래와 같은 함수를 작성하여, 값을 변경하고 두 수의 위치를 바꾸려고 했다.

```js
function changeNum(n1, n2) {
  if (n1 < n2) {
    n1 = n2 + 1;
  } else {
    n2 = n1 + 1;
  }
}

const arr = [2, 3, 9];
let [a, b, c] = arr;

changeNum(a, b);

console.log(arr); // [2, 3, 9]
```

하지만 의도와는 다르게 `changeNum`은 위치를 바꾸지 못하고 `arr`는 원본 그대로를 출력한다.

왜 함수 n1, n2의 값을 변경하지 못하는 걸까? 🥲

자바스크립트에서 기본 타입(primitive types)은 `값에 의한 전달(Pass by Value) 방식`으로 함수에 전달되기 때문이다. 이는 **함수에 값을 전달할 때, 실제 값의 복사본이 전달되며, 함수 내에서 매개변수의 값을 변경해도 외부의 변수에는 영향을 미치지 않는다는 것을 의미**한다.

따라서 changeNum 함수 내에서 n1, n2의 값을 변경해도 a, b 원본에는 영향을 주지 않는다.

그럼 어떻게 바꿀 수 있을까?

## 참조에 의한 전달(Pass by Reference)

객체나 배열과 같은 참조 타입은 `참조에 의한 전달(Pass by Reference)` 방식으로 작동한다. 이 방식에서는 **변수가 실제 데이터가 아닌, 데이터가 저장된 메모리 주소를 참조**한다.

함수에 참조 타입의 값을 인자로 전달할 때, 전달 되는 것은 실제 데이터의 복사본이 아니라 데이터가 저장된 메모리 주소의 참조이다. **따라서 함수 내에서 참조를 통해 데이터를 변경하면 원본 데이터에도 반영이 된다.**

이러한 방식을 이용하여 n1과 n2 값을 변경하면 객체나 배열을 통해 값을 전달하고, 함수 내에서 객체의 속성이나 배열의 요소를 변경할 수 있다.

```js
function changeNum(arr) {
  if (arr[0] < arr[1]) {
    arr[0] = arr[1] + 1;
  } else {
    arr[1] = arr[0] + 1;
  }
}

const arr = [2, 3, 9];
changeNum(arr);

console.log(arr); // [4, 3, 9]
```

## 값에 의한 전달(Pass by Value)

아까 말했듯이 기본 타입(primitive type)인 숫자, 문자열, boolean, null, undefined, Symbol, BigInt은 `값에 의한 전달(Pass by Value)`방식으로 처리한다. 이는 **함수에 기본 타입의 값을 인자로 전달할 때, 실제 값이 아닌 그 값의 복사본이 함수 내부로 전달된다는 의미**이다.

**따라서, 함수 내에서 매개변수의 값을 변경해도 원본 변수의 값에는 영향을 미치지 않는다.**

아래는 값에 의한 전달에 대한 간단한 예시 코드다.

```js
function modifyValue(x) {
  x = 5;
  console.log('함수 내부: ', x); // 함수 내부: 5
}

let a = 3;

modifyValue(a);
console.log('함수 외부: ', a); // 함수 외부: 3
```

## 요약

- 자바스크립트에서 **기본 타입(primitive type)**은 `값에 의한 전달(Pass by Value)` 방식으로 처리된다. 즉, 함수 내에서 매개변수의 값을 변경해도 원본 변수의 값에는 영향을 미치지 않는다.
- 반면 객체나 배열 같은 **참조 타입(reference type)**은 `참조에 의한 전달(Pass by Reference)` 방식으로 처리된다.
