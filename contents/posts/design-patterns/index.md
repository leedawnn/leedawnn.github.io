---
title: '✨ 프론트엔드에서 사용하는 디자인 패턴에는 뭐가 있을까?'
description: MVC, MVVM, Flux
date: 2024-03-21
update: 2024-03-21
tags:
  - design-pattern
  - architecture
---

## 디자인 패턴이란?

본론에 들어가기 앞서, 디자인 패턴의 정의와 사용하는 이유에 대해 알아보자.

**디자인 패턴**이란 개발 과정에서 공통으로 발생하는 문제를 해결하기 위해 사용되는 패턴이다. 저명한 소프트웨어 엔지니어 *마틴 파울러*는 디자인 패턴을 '절반만 완성된' 것이라고 표현한다. 디자인 패턴은 코드로 구현된 구현체가 아니라 문제 해결을 위한 패턴이기 때문에 자신의 개발 환경에 맞게 구현하는 것은 개발자의 몫이기 때문이다.

### 무조건 디자인 패턴을 활용하는 것이 좋은걸까?

우리는 간단한 TODO 앱을 만들 때 디자인 패턴이 필요하다고 말하지 않는다. 대부분의 디자인 패턴은 복잡하고 거대한 프로그램을 위해서 만들어졌다.

## 그래서, 디자인 패턴을 사용하는 이유가 뭘까?

- **증명된 솔루션이다.**

디자인 패턴은 최고의 개발자들이 만들어 낸 솔루션이다. 또한, 오랜 기간 사용되어 오면서 안정성 검증이 완료된 솔루션이다. 심지어 디자인 패턴은 문서화도 잘 되어있다. 거인의 어깨에 올라타서 안정적인 프로그램을 만들 수 있다.

- **재사용성과 유지보수성**

디자인 패턴은 검증된 해결 방법을 제공함으로써 개발 과정에서 비슷한 문제가 재발할 때마다 이를 재사용할 수 있게 한다. 이는 개발 시간을 단축시키고, 코드의 품질을 높일 수 있다. 또한 소프트웨어의 구조를 명확하게 하고, 코드의 가독성을 높여준다. 이로 인해 다른 개발자들이 코드를 이해하고 유지보수하기가 더 쉬워진다.

- **확장성**

디자인 패턴을 사용함으로써 시스템의 일부분을 변경하거나 확장하는 것이 더 용이해진다. 패턴은 일반적으로 유연성을 고려하여 설계되므로, 시스템을 쉽게 확장하거나 수정할 수 있다.

## 프론트엔드에서의 디자인 패턴 활용

프론트엔드에서는 다양한 디자인 패턴이 활용된다. 그 중에서도 특히 SPA(Single Page Application) 프레임워크나 라이브러리들이 `MVC`, `MVVM`과 같은 패턴을 채택하거나 변형하여 사용한다.

예를 들어,

- **React** : React 자체는 라이브러리이기 때문에 엄밀히 말해 디자인 패턴을 강제하지는 않는다. 그러나, `Flux 아키텍처`나 `Redux`와 같은 상태 관리 라이브러리와 함께 사용되어 일종의 `MVC` 변형 패턴으로 볼 수 있다.
- **Angular** : `MVVM`나 `MVC` 패턴의 변형을 사용한다. Angular는 데이터 바인딩, 의존성 주입 등의 기능을 통해 개발자가 이 패턴을 더 쉽게 구현할 수 있도록 돕는다.
- **Vue** : `MVVM` 패턴에 가깝다. Vue는 `ViewModel`의 역할을 하는 Vue 인스턴스를 통해 `View`와 `Model`을 연결한다.

이제 어떤 디자인 패턴들이 있는지 자세히 알아보자.

## MVC (Model-View-Controller)

![](https://www.freecodecamp.org/news/content/images/2021/04/MVC3.png)

- **Model** : 데이터와 비즈니스 로직을 관리한다. 데이터 조회나 저장과 같은 기능을 수행하며, 데이터의 상태 변화를 `View`와 `Controller`에 통지한다.
- **View** : 사용자 인터페이스(UI)를 담당한다. 사용자에게 정보를 표시하고, 사용자의 입력을 받는다.
- **Controller** : 사용자의 입력을 받아 `Model`을 업데이트하고, 그 결과를 `View`에 반영한다. `View`와 `Model` 사이의 중재자 역할을 한다. 비즈니스 로직을 처리하는 `Model`과 완전히 UI에 의존적인 `View`가 서로 직접 이야기할 수 없게 한다.

### `MVC`의 한계

`MVC`에서 `View`는 `Controller`에 연결되어 화면을 구성하는 단위요소이므로 다수의 `View`들을 가질 수 있다. 그리고 `Model`은 `Controller`를 통해 `View`와 연결되어지지만, `Controller`를 통해서 하나의 `View`에 연결될 수 있는 `Model`도 여러 개가 될 수 있다.

이렇게 되면 `View`와 `Model`이 서로 의존성을 띄게 된다.

화면에 복잡한 화면과 데이터의 구성이 필요하다면, `Controller`에 다수의 `Model`과 `View`가 복잡하게 연결되어 있는 상황이 생길 수 있다.

**따라서, View에서 데이터 업데이트를 할 때 연쇄적인 업데이트가 일어나게 되고 앱이 커지면 업데이트 흐름을 따라가기 힘들어진다.**

`MVC`가 너무 복잡하고 비대해져서 새 기능을 추가할 때마다 크고 작은 문제점을 가지는 형태를 `Massive ViewController(대규모 MVC 어플리케이션)`라고 부른다. `MVC`의 한계를 잘 나타내는 용어이다.

이후 이러한 문제점을 보완한 여러 다양한 패턴들이 파생되었다. `MVP`, `MVVM`, `Flux` 등...

## MVVM (Model-View-ViewModel)

![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*J7_36YMEO8pNAYGyR53hkA.png)

- **Model** : MVC 패턴의 Model과 동일하게 데이터와 비즈니스 로직을 관리한다.
- **View** : 사용자에게 보여지는 UI 부분을 담당한다. `View`는 `ViewModel`을 통해 사용자의 입력을 처리하고, 상태 변화를 표시한다.
- **ViewModel** : `View`를 표현하기 위한 데이터와 명령을 가지고 있다. `ViewModel`의 역할은 `View`가 사용할 메서드와 필드를 구현하고, `View`에게 상태 변화를 알리는 것이다. `View`와 `Model` 사이의 의존성을 줄인다.

`MVVM`을 구성하는 3가지 요소의 역할과 책임을 이해하기 위해서는 먼저 이들 사이의 관계를 알아야합니다. `View`는 `ViewModel`을 알지만, `ViewModel`은 `View`를 알지 못합니다. 또한, `ViewModel`은 `Model`을 알지만, `Model`은 `ViewModel`을 알지 못한다.

이런 구조를 통해서 `ViewModel`과 `Model`이 `View`로부터 독립적인 형태를 만들어서 위에서 말한 UI로부터 비즈니스 로직과 프레젠테이션 로직을 분리라는 목적을 이룰 수 있게 되었다.

### `MVVM`의 한계

하지만 `MVVM` 패턴은 거대하고 복잡한 애플리케이션을 위해서 고안된 디자인 패턴인 만큼, 작은 규모의 애플리케이션에서 사용하게 되면 오버헤드가 커진다. 또한 데이터 바인딩이 복잡해지면 성능 저하 또는 디버깅이 어렵다는 단점이 있다.

## Flux 아키텍처

![](https://fullstackopen.com/static/7bf90479b6757c7af3b9a9f0e7f19a64/5a190/flux2.png)

> **🤔 디자인 패턴과 아키텍처는 다른 거 아냐?**
>
> Flux와 같은 **아키텍처**는 시스템의 전반적인 설계와 구조를 다루는 반면, 디자인 패턴은 그보다 더 세부적인 수준에서 구체적인 문제 해결 방법을 제공한다. 두 개념은 서로 보완적으로 작용할 수 있으며, 강력하고 유지보수가 용이한 소프트웨어를 개발하는 데 함께 사용될 수 있다.

`Flux`는 Meta에서 개발한 애플리케이션 아키텍처로, 주로 React와 함께 사용된다. `Flux`의 핵심은 데이터의 "**단방향 흐름**"이다. 이는 애플리케이션의 예측 가능성을 높이고 디버깅을 용이하게 한다.

`Flux` 아키텍처는 크게 4가지 구성 요소로 이루어져 있다.

- **Action** : 사용자의 행동이나 시스템에서 발생하는 이벤트로부터 시작되는 데이터의 흐름이다. `Action`은 어떤 변화가 일어나야할 지를 설명한다.
- **Dispatcher** : 모든 데이터 흐름의 중앙 허브이다. `Action`이 발생하면 `Dispatcher`를 통해 `Store`에 전달된다.
- **Store** : 애플리케이션의 상태를 보유하고 있으며, `Dispatcher`로 부터 `Action`을 받아 상태를 업데이트한다.
- **View** : 사용자에게 정보를 표시하고, 사용자의 상호작용을 받는다. `View`는 `Store`의 상태 변화에 반응하여 UI를 업데이트한다.

`Flux` 아키텍처와 React의 조합은 다음과 같은 장점을 제공한다.

- **명확한 데이터 흐름**

`Flux`에서는 데이터가 단방향으로 흐르기 때문에 애플리케이션에서 데이터가 어떻게 이동하고 변하는지 추적하기가 훨씬 용이하다. 이러한 접근 방식은 디버깅을 간소화하고, 데이터 흐름 관련 버그를 줄여준다.

- **컴포넌트와의 일관성**
  Flux는 애플리케이션의 상태를 스토어에서 중앙 집중적으로 관리한다. 이로 인해 컴포넌트가 상태를 직접 관리하는 대신, `Store`를 통해 상태를 조회하고, `Action`을 통해 상태를 업데이트합니다. 이러한 접근은 컴포넌트를 상태로부터 분리시켜, 더욱 순수한 UI 컴포넌트를 만들 수 있게 해준다. 결과적으로, 컴포넌트의 재사용성과 테스트 용이성이 향상.

- **유지보수의 용이성**

Flux의 명확한 구조와 규칙은 큰 규모의 애플리케이션에서도 유지보수성을 향상시킨다. 코드의 구조가 명확하고, 각 부분의 역할이 분명하기 때문에 새로운 개발자가 프로젝트에 참여하거나 기존 코드를 수정하는 일이 훨씬 쉬워진다.

- **확장성**
  Flux 아키텍처는 애플리케이션의 확장을 용이하게 한다. 새로운 기능이나 데이터 흐름을 추가할 때 기존 시스템을 크게 변경하지 않고도, 애플리케이션의 구조 안에서 자연스럽게 확장할 수 있다.

### `Flux`의 한계

- **복잡성 증가**
  Flux는 단방향 데이터 흐름을 제공하지만, 크고 복잡한 애플리케이션에서는 관리해야 할 액션, 디스패처, 스토어가 많아져 관리가 복잡해질 수 있습니다. 이는 프로젝트의 크기가 커질수록 더욱 두드러집니다.
- **보일러플레이트 코드**
  Flux 구현 시, 액션 타입, 액션 크리에이터, 스토어, 디스패처 등을 정의해야 합니다. 이 과정에서 반복적이고 유사한 코드가 많이 생성될 수 있으며, 이는 코드베이스를 불필요하게 늘릴 수 있습니다.
- **유연성의 제한**
  Flux 아키텍처는 엄격한 구조를 가지고 있으며, 이는 때때로 특정 상황에 대한 유연한 대응을 어렵게 만들 수 있습니다.
