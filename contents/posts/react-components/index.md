---
title: "🚀 React에서 컴포넌트를 분리하는 기준"
description: 컴포넌트를 어떻게 나눌까?
date: 2024-02-26
update: 2024-02-26
tags:
  - react
  - components
series: "react"
---

## 컴포넌트를 분리하는 방법에는 어떤 것이 있을까?

컴포넌트를 분리하는 방법론들에 따라, 컴포넌트를 분리하는 "기준"이 달라지게 된다.  
보통 컴포넌트를 분리하는 방법론은 아래와 같이 나뉜다.

1. **컴포넌트의 관심사 분리(Separation of Concerns, SoC)**
2. **headless 컴포넌트**
3. **SOLID, 단일 책임의 원칙**

이 방법론들은 각각 어떤 기준을 가지고 있는지 하나씩 알아보자.

## 컴포넌트의 관심사 분리(Separation of Concerns, SoC)

### 관심사의 분리란?

- 관심사의 분리란 복잡한 코드를 비슷한 기능을 하는 코드끼리 별도로 관리하는 것을 말한다.
- 프로그램을 구별된 '개개의 관심사를 해결하는 부분'으로 분리하는 디자인 원칙이다.
- 컴포넌트 별로 관심사를 분리하면 확장성과 재사용성을 높일 수 있다.

### 컴포넌트를 분리하는 이유

- 컴포넌트는 의도에 따라 **UI를 표현**하고자 하거나 **동작하는 로직**을 담을 수 있다.
- 이처럼 컴포넌트는 재사용할 수 있는 최소 UI 단위임에도 불구하고, 웹의 복잡도와 해당 컴포넌트에서 수행하려고 하는 역할에 따라 얼마든지 복잡해질 수 있다.
- 따라서 '관심사의 분리' 원칙에 따라 컴포넌트를 분리해서 관리하여야 한다.