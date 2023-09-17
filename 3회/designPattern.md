# 디자인 패턴

## Singleton 패턴

Singleton은 1회에 한하여 인스턴스화가 가능하며 전역에서 접근 가능한 클래스를 지칭한다. 만들어진 Singleton 인스턴스는 앱 전역에서 공유되기 때문에 앱의 전역 상태를 관리하기에 적합하다.

> 앱 전역에 공유되는 완전한 싱글턴 패턴은 아니지만, 리액트 라우터 관리를 singleton 패턴으로 관리했을 때 관리포인트가 하나로 줄어서 정말 유용했던 기억

## Proxy 패턴

Proxy 객체를 활용하면 특정 객체와의 인터렉션을 조금 더 컨트롤 할 수 있게 된다. Proxy 객체는 어떤 객체의 값을 설정하거나 값을 조회할때 등의 인터렉션을 직접 제어할 수 있다.

Proxy는 **유효성 검사**를 구현할 때 유용하다.

> proxy 객체, Reflect 객체를 알게해준 고마운 패턴.
> 객체에 직접 접근시키지 않고 안정성을 높여야 한다면 실제로도 사용해볼 법한 것 같다.
> useReducer가 약간 비슷한 느낌아닌가 싶다.

## Provider 패턴

종종 prop drilling이라 불리는 안티패턴을 사용하게 되는데. 아주 멀리있는 컴포넌트 트리까지 props를 내려주게 되면 prop에 의존되는 컴포넌트들을 나중에 리펙토링하기란 거의 불가능해지며. 어떤 데이터가 어디로부터 전해져 오는지조차 알기 어렵게 된다.

Provider 패턴은 이런 경우에 매우 유용하다. Provider 패턴을 이용하면 각 레이어에 직접 데이터를 주지 않고도 여러 컴포넌트들에게 데이터에 접근할 수 있게 구현할 수 있다.

> react의 context가 대표적인 예시

## Prototype 패턴

Prototype 패턴은 동일 타입의 여러 객체들이 프로퍼티를 공유할 때 유용하게 사용한다. Prototype은 JavaScript 객체의 기본 속성이므로 Prototype 체인을 활용할 수 있다.

> 모자딥으로 자바스크립트 프로토타입 머리깨지면서 공부하던 기억이...

## Container/Presentational 패턴

React에서 관심사의 분리(SoC) 를 강제하는 방법은 Container/Presentational Pattern을 이용하는 방법이 있다. 이 를 통해 비즈니스 로직에서 뷰를 분리해낼 수 있다.

1. Presentational Components: 데이터가 어떻게 사용자에게 보여질 지에 대해서만 다루는 컴포넌트. 
2. Container Components: 어떤 데이터가 보여질 지에 대해 다루는 컴포넌트.

> 실제 패턴인지는 잘모르지만, 현업에서 가장 많이 사용하는 패턴
> container 부분을 커스텀 훅으로 분리하는 방식을 더 많이 사용한다.
> 거의 장점이 대부분인 패턴이 아닌가?

## Hooks 패턴

React 16.8 버전에는 Hooks라는 기능이 추가되었다. Hooks는 React의 상태와 생명 주기 함수들을 ES2015의 클래스를 사용하지 않고 쓸 수 있게 해 준다.

Hooks가 디자인 패턴이 아닐순 있지만 Hooks는 앱에서 아주 중요한 역할을 한다. 여러 전통적인 디자인 패턴들은 모두 Hooks로 변경할 수 있다.

> 함수형 컴포넌트의 대시대를 열게한 장본인.
> 커스텀 훅 사랑해요

## Observer 패턴

Observer 패턴에서 특정 객체를 구독할 수 있는데. 구독하는 주체를 Observer라 하고. 구독 가능한 객체를 Observable이라 한다. 이벤트가 발생할 때 마다 Observable은 모든 Observer에게 이벤트를 전파한다.

> view-model간의 관계같은 느낌
> 많은 전역상태 라이브러리가 Observer 패턴과 유사하지 않나?

[옵저버 패턴으로 바닐라JS 상태관리하기](https://velog.io/@proshy/옵저버-패턴으로-바닐라JS-상태관리하기)

자매품으로 Pub/Sub 패턴도 있다.

## Mixin 패턴

Mixin은 상속 없이 어떤 객체나 클래스에 재사용 가능한 기능을 추가할 수 있는 객체이다. Mixin은 단독으로 사용할 순 없고 상속 없이 객체나 클래스에 기능을 추가하는 목적으로 사용된다.

```js
class Dog {
  constructor(name) {
    this.name = name
  }
}

const dogFunctionality = {
  bark: () => console.log('Woof!'),
  wagTail: () => console.log('Wagging my tail!'),
  play: () => console.log('Playing!'),
}

Object.assign(Dog.prototype, dogFunctionality)
```

> 이미 만들어진 객체에 기능을 주입하기에는 좋아보이나 코드의 복잡도가 높아져서 유지보수가 어려워 질 것 같다.

## Mediator/Middleware 패턴

컴포넌트들이 서로 직접 통신하는 대신 중재자 역할을 하는 객체를 통하도록 한다. 중재가 객체가 요청을 받아 이를 필요로 하는 객체들에게 전달하는 것이다. 중재자는 보통 객체나 함수로 구현된다.

이 미들웨어 패턴은 여러 객체 간 다대 다의 통신을 하나의 관리 포인트를 통하도록 만들어 관계를 단순하게 만들어준다.

> 정말 정말 많이 사용하는 패턴.
> 모든 흐름이 미들웨어를 타기 때문에 주의가 필요하다.
> [redux middleware](https://redux.js.org/understanding/history-and-design/middleware), [axios interceptors](https://axios-http.com/docs/interceptors), [next middleware](https://nextjs.org/docs/app/building-your-application/routing/middleware)

## HOC 패턴

종종 여러 컴포넌트에서 같은 로직을 사용해야 하는 경우가 있다. 이런 로직은 컴포넌트의 스타일시트를 설정하는 것일 수 있고. 권한을 요청하거나. 전역 상태를 추가하는 것일 수 있다.

같은 로직을 여러 컴포넌트에서 재사용하는 방법 중 하나로 고차 컴포넌트 패턴을 활용하는 방법이 있다. 이 패턴은 앱 전반적으로 재사용 가능한 로직을 여러 컴포넌트들이 쓸 수 있게 해 준다.

고차 컴포넌트란 다른 컴포넌트를 받는 컴포넌트를 뜻한다. HOC는 인자로 넘긴 컴포넌트에게 추가되길 원하는 로직을 가지고 있다. HOC는 로직이 적용된 엘리먼트를 반환하게 된다.

```js
function withStyles(Component) {
  return props => {
    const style = { padding: '0.2rem', margin: '1rem' }
    return <Component style={style} {...props} />
  }
}

const Button = () = <button>Click me!</button>
const Text = () => <p>Hello World!</p>

const StyledButton = withStyles(Button)
const StyledText = withStyles(Text)
```

### HOC의 사용 사례

- 앱 전반적으로 동일하며 커스터마이징 불가한 동작이 여러 컴포넌트에 필요한 경우
- 컴포넌트가 커스텀 로직 추가 없이 단독으로 동작할 수 있어야 하는 경우

> 사용하면 좋을 상황이 있기는 있지만 실제로는 잘 사용하지 않는 패턴
> 컴포넌트의 재사용성을 높이고 로직도 분리하면서 관심사 분리도 지킬 수 있지만, props나 데이터 트래킹이 어려워져서 컴포넌트를 잘 설계한다면 굳이 굳이 사용할 일이 없는 것 같다.

## Render Props 패턴

컴포넌트를 재사용 가능하게 할 수 있는 또 다른 방법으로, render prop 패턴을 사용하는 방법이 있다.

`children` prop을 활용하는 것으로 해당 컴포넌트를 재사용할 수 있게 된다.

## Factory 패턴

팩토리 패턴을 사용하면 함수를 호출하는 것으로 객체를 만들어낼 수 있다. `new` 키워드를 사용하는 대신 함수 호출의 결과로 객체를 만들 수 있는 것이다.

**factory 패턴**
```js
const createUser = ({ firstName, lastName, email }) => ({
  firstName,
  lastName,
  email,
  fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
});

const user1 = createUser({
  firstName: "John",
  lastName: "Doe",
  email: "john@doe.com"
});

const user2 = createUser({
  firstName: "Jane",
  lastName: "Doe",
  email: "jane@doe.com"
});
```

**class**
```js
class User {
  constructor(firstName, lastName, email) {
    this.firstName = firstName
    this.lastName = lastName
    this.email = email
  }

  fullName() {
    return `${this.firstName} ${this.lastName}`
  }
}

const user1 = new User({
  firstName: 'John',
  lastName: 'Doe',
  email: 'john@doe.com',
})

const user2 = new User({
  firstName: 'Jane',
  lastName: 'Doe',
  email: 'jane@doe.com',
})
```

> class를 사용할 수 없는 상황에서 객체를 찍어내야한다면 사용할 만한 패턴일 것 같다.
> 그냥 class 쓸 것 같다.
## Compound 패턴
하나의 작업을 위해 여러 컴포넌트를 만들어 역할을 분담하게 한다

```js
// export
export const Dialog = Object.assign(DialogMain, {
  Dimmed: DialogDimmed,
  Title: DialogTitle,
  Subtitle: DialogSubtitle,
  Description: DialogDescription,
  Comment: DialogComment,
  CheckButton: DialogCheckButton,
  CheckBox: DialogCheckBox,
  TextButton: DialogTextButton,
  Button: DialogButton,
  LabelButton: DialogLabelButton,
  Divider: DialogDivider,
});

// Usage
<Dialog>
    <Dialog.Title>제목</Dialog.Title>
</Dialog>
```

## 레퍼런스
https://patterns-dev-kr.github.io/
https://vallista.kr/TypeScript-디자인-패턴-옵저버-패턴/
https://vallista.kr/TypeScript-디자인-패턴-팩토리-패턴/
https://fe-developers.kakaoent.com/2022/220731-composition-component/