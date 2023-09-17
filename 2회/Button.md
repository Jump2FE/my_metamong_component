# 개념 훑고 가기

## 응집도/ 결합도란?

`응집도(cohension)` : 응집도는 한 모듈 내부의 처리 요소들이 서로 관련되어 있는 정도를 말한다. 즉, 모듈이 독립적인 기능을 수행하는지 또는 하나의 기능을 중심으로 책임이 잘 뭉쳐있는지를 나타낸다.

`결합도(coupling)` : 결합도는 서로 다른 모듈 간에 상호 의존하는 정도 또는 연관된 관계를 의미한다. 결합도는 보통 응집도와 대비된다. 낮은 결합도는 종종 높은 응집도와 관련이 있다.

모듈의 독립성을 판단하는 기준으로서 결합도를 낮추고 응집도를 높일 수록 모듈의 독립성이 높다고 할 수 있다.

## 관심사의 분리(separation of concerns, SoC)

`관심사` : 컴퓨터 과학에서 **관심사**(concern)는 컴퓨터 프로그램의 코드에 영향을 미치는 특정한 정보 집합이다.

`관심사 분리` : 컴퓨터 프로그램을 구별된 부분으로 분리시키는 디자인 원칙으로, 각 부문은 개개의 관심사를 해결한다.

관심사 분리를 적용하여 프로그래밍 한다면 모듈러 프로그램이 만들어지게 되고, **특정 부분을 알기 위해서 다른 부분도 알아야 할 필요가 없어지게 된다.**

ex)
- `객체 지향 프로그래밍` : 객체의 관심사를 기술하는 방식
- `함수형 프로그래밍`: 함수로서 관심사를 기술하는 방식

> **🤔관심사? 말이 너무 어렵다...**
> 컴퓨터 프로그램의 코드에 영향을 미치는 특정한 정보 집합
> => 코드를 바뀌게 할 수 있는 무언가
> 코드가 바뀌는 상황들을 적절히 분리하면 유지보수가 용이하겠구나!!

# 컴포넌트에서의~

## 응집도

- REP: 재사용/릴리스 등가 원칙 (Reuse/Release Equivalence Principle)  
- CCP: 공통 폐쇄 원칙 (Common Closure Principle)  
- CRP: 공통 재사용 원칙 (Common Reuse Principle)

### REP: 재사용/릴리스 등가 원칙 (Reuse/Release Equivalence Principle)

> 재사용 단위는 릴리즈 단위와 같다.  
> 컴포넌트가 릴리즈 절차를 통해 추적 관리 되지 않거나 릴리즈 번호가 부여 되지 않는다면, 해당 컴포넌트를 재사용 하고 싶어도 할 수 없고, 하지도 않을 것이다.

> **🧐 내 언어로 재해석하기**
> 컴포넌트를 업데이트가 된 건지 버려진건지 알아야 재사용을 하든가 말든가하지! 문서화로 컴포넌트를 관리해야해!

### CCP: 공통 폐쇄 원칙 (Common Closure Principle)

> 동일한 이유로 동일한 시점에 변경되는 클래스를 같은 컴포넌트로 묶어라.  
> 서로 다른 시점에 다른 이유로 변경되는 클래스는 다른 컴포넌트로 분리하라.
> 이는 컴포넌트 수준의 SRP원칙이라고 할 수 있다.

> **🧐 내 언어로 재해석하기**
> 컴포넌트를 묶는 기준을 동일한 이유로 변경되고 동일한 시점에 변경되는지로 판단할 수 있다.

### CRP: 공통 재사용 원칙 (Common Reuse Principle)

> 필요하지 않는것에 의존하게 강요하지 말라.

> **🧐 내 언어로 재해석하기**
> 딱 공통적으로 사용하는 것만 콤팩트하게 남기고 나머지는 버리라는 뜻인가보다.

## 결합도
- `ADP(Acyclic Dependencies Principle)` : 의존성 비순환 원칙
- `SDP(Stable Dependencies Principle)` : 안정된 의존성 원칙
- `SAP(Stable Abstract Principle)` : 안정된 추상화 원칙

### ADP: 의존성 비순환 원칙

> 컴포넌트 의존성 그래프에 순환이 있어서는 안된다.
> 순환이 발생하면 어떻게든 끊어야 한다.

### SDP: 안정된 의존성 원칙

> 안정성의 방향으로(더 안정된 쪽에) 의존하라.  
> 변경하기 어려운 모듈이 변경하기 쉽게 만들어진 모듈에 의존하지 않도록 만들어야 한다.

### SAP: 안정된 추상화 원칙

> 컴포넌트는 안정된 정도만큼만 추상화되어야 한다.

# 버튼 컴포넌트 만들기

> radix ui와 material design의 button 컴포넌트를 참고하여 진행했습니다!

## 타입으로 추상화하기

```ts
export type ButtonProps = {
  children: React.ReactNode;
  onClick?: () => void;
  size?: 'small' | 'medium' | 'large';
  variant?: 'filled' | 'outlined';
  color?: 'primary' | 'secondary';
  radius?: 'none' | 'small' | 'medium' | 'large';
  disabled?: boolean;
};
```

# 레퍼런스
[관심사의 분리(Separation of Concerns, SoC) Medium]
- https://medium.com/@smartbosslee/%EA%B4%80%EC%8B%AC%EC%82%AC%EC%9D%98-%EB%B6%84%EB%A6%AC-separation-of-concerns-soc-8a8d09df066d
[Clean Architecture 4-13 컴포넌트 응집도]
- https://wikidocs.net/167374
[Clean Architecture 4-13 컴포넌트 결합도]
- https://wikidocs.net/167375
[응집도있는 컴포넌트 설계란?]
- https://velog.io/@awesome-hong/응집도있는-컴포넌트-설계란
[radix-ui button 컴포넌트]
- https://www.radix-ui.com/themes/docs/components/button#radius
[material design button component]
- https://m3.material.io/components/buttons/guidelines
## 책

<a href="https://www.yes24.com/Product/Goods/77283734">
	<img width=200 height=300 src=https://image.yes24.com/goods/77283734/XL />
<a />
클린 아키텍처



