# 손민욱 202030418

### 2024년 6월 12일 강의: CSS

#### CSS란?

CSS는 **Cascading Style Sheets**의 약자로, 웹 페이지의 스타일을 정의하는 언어입니다. "Cascading"은 '계단식'이라는 의미로, 여러 스타일이 동일한 엘리먼트에 적용될 때 스타일 간의 충돌을 방지하기 위해 계단식으로 적용하는 규칙을 가지고 있습니다.

- **스타일링 언어:** CSS는 HTML 엘리먼트의 외형을 설정합니다.
- **계단식 적용:** 여러 스타일이 한 엘리먼트에 적용될 때 우선순위를 정해 충돌을 막습니다.
- **다중 적용:** 하나의 스타일이 여러 엘리먼트에 적용될 수 있고, 하나의 엘리먼트에 여러 스타일이 적용될 수 있습니다.

#### 선택자와 스타일

- **선택자(Selector):** CSS에서 스타일을 적용할 HTML 엘리먼트를 선택하는 방법입니다. 선택자는 HTML 엘리먼트를 직접 지정하거나, 엘리먼트의 조합 또는 클래스 형태로 작성할 수 있습니다.
- **스타일(Style):** 스타일은 속성(Property)과 키-값(Key-Value) 쌍으로 이루어지며, 콜론(:)으로 구분하고, 각 스타일은 세미콜론(;)으로 구분합니다.

예시:
/_ 선택자 _/
h1 {
color: blue; /_ 스타일: 속성과 값 _/
font-size: 20px; /_ 스타일: 속성과 값 _/
}

# ---------------------------------------------------

## 2024년 6월 11일 강의: 리액트 컨텍스트와 특수화

### 컨텍스트를 사용하기 전에 고려할 점

컨텍스트는 여러 컴포넌트가 특정 데이터를 필요로 할 때 사용합니다. 무조건 컨텍스트를 사용하는 것이 좋은 것은 아닙니다. 재사용성이 떨어질 수 있기 때문입니다. 데이터 전달은 props를 사용하는 것이 더 적합할 때가 많습니다.

### Specialization(특수화, 전문화)

특수화는 범용적인 개념을 구체화하는 것입니다. 리액트에서는 합성을 통해 특수화를 구현합니다. 예를 들어, Dialog 컴포넌트를 기본으로 하여 SignUpDialog처럼 특수한 목적의 컴포넌트를 만드는 방식입니다.

### Containment와 Specialization

- **Containment:** props.children을 사용합니다.
- **Specialization:** 직접 정의한 props를 사용합니다.

예제: Dialog 컴포넌트에 props.children을 추가하여 SignUpDialog에서 이를 활용합니다.

```jsx
function Dialog(props) {
  return <div>{props.children}</div>;
}

function SignUpDialog() {
  return (
    <Dialog>
      <h1>Sign Up</h1>
    </Dialog>
  );
}
```

# 상속에 대해 알아보기

- 상속은 자식 클래스가 부모 클래스의 속성을 모두 갖게 되는 개념입니다.
- 리액트에서는 상속보다는 합성을 통해 새로운 컴포넌트를 생성하는 것을 선호합니다.

# ---------------------------------------------------

## 2024년 6월 05일 강의: 리액트 합성과 컨텍스트 API

### Shared State

Shared State는 같은 부모 컴포넌트의 state를 자식 컴포넌트가 공유해서 사용하는 것입니다.

### 합성

여러 개의 컴포넌트를 합쳐서 새로운 컴포넌트를 만드는 것입니다.

- **Containment:** 특정 컴포넌트가 하위 컴포넌트를 포함하는 형태의 합성 방법입니다. `children` prop을 사용하여 자식 엘리먼트를 출력에 그대로 전달합니다.

### 컨텍스트 API

- **React.createContext:** 컨텍스트를 생성하기 위한 함수입니다.
- **Context.Provider:** 하위 컴포넌트들을 감싸주면 모든 하위 컴포넌트가 해당 컨텍스트의 데이터에 접근할 수 있게 합니다.
- **Context.Consumer:** 함수형 컴포넌트에서 컨텍스트를 구독할 수 있습니다.
- **Context.displayName:** 컨텍스트 객체는 displayName이라는 문자열 속성을 갖습니다. 리액트 개발자 도구에서 유용합니다.

### 컨텍스트를 사용해야 할 경우

여러 컴포넌트에서 자주 필요로 하는 데이터는 로그인 여부, 로그인 정보, UI 테마, 현재 선택된 언어 등이 있습니다. 이런 데이터들을 기존의 방식대로 props를 통해 넘겨주는 방식은 복잡해질 수 있습니다. 컨텍스트를 사용하면 일일이 props로 전달할 필요 없이 데이터를 곧바로 전달할 수 있습니다.

# ---------------------------------------------------

# 5월 29일 강의 내용

## textarea 태그

- HTML에서는 `<textarea>`의 children으로 텍스트가 들어갑니다.
- 리액트에서는 state를 통해 태그의 value라는 attribute를 변경하여 텍스트를 표시합니다.

## File input 태그

- File input 태그는 그 값이 읽기 전용이기 때문에 리액트에서는 비제어 컴포넌트가 됩니다. `<input type="file"/>`

## Input Null Value

- 제어 컴포넌트에 value prop을 정해진 값으로 넣으면 입력값을 바꿀 수 없습니다.
- 만약 value prop은 넣되 자유롭게 입력할 수 있게 만들고 싶다면 값이 `undefined` 또는 `null`을 넣어주면 됩니다.

# ---------------------------------------------------

# 5월 22일 강의 내용

## 리스트와 키란 무엇인가?

- 리스트는 자바스크립트의 배열과 같은 것입니다.
- 키는 각 객체나 아이템을 구분할 수 있는 고유한 값을 의미합니다.
- 리액트에서는 배열과 키를 사용해 반복되는 다수의 엘리먼트를 쉽게 렌더링할 수 있습니다.

## 여러 개의 컴포넌트 렌더링하기

- 배열에 있는 엘리먼트를 `map()` 함수를 이용하여 렌더링합니다.
- 예: `const doubled = numbers.map((number) => number * 2);`

## 리스트의 키에 대해 알아보기

- 키는 리스트에서 아이템을 구별하기 위한 고유한 문자열입니다.
- 리스트에서 어떤 아이템이 변경, 추가 또는 제거되었는지 구분하기 위해 사용합니다.
- 키는 같은 리스트에 있는 엘리먼트 사이에서만 고유한 값이면 됩니다.

## 제어 컴포넌트

- 제어 컴포넌트는 사용자가 입력한 값에 접근하고 제어할 수 있도록 해주는 컴포넌트입니다.

# ---------------------------------------------------------------------------------

# 5월 8일 강의 내용

## DOM Event

- HTML: `<button onClick="activate()">Activate</button>`
- React: `<button onClick={activate}> Activate </button>`

## Event Handler

- 사건이 발생하면 사건을 처리하는 역할을 합니다.
- EventListener로 불리기도 합니다.

## Conditional Rendering

- 조건부 렌더링: 조건에 따라서 렌더링이 달라집니다.
  ```jsx
  function Greeting(props) {
    const isLoggedIn = props.isLoggedIn;
    if (isLoggedIn) {
      return <UserGreeting />;
    }
    return <GuestGreeting />;
  }
  ```

````

```

## Truthy와 Falsy 값

### Truthy

- true로 여겨지는 값
  - 예시: `true`, `{}`, `[]`, `42`, `"0"`, `"false"`

### Falsy

- false로 여겨지는 값
  - 예시: `0`, `-0`, `0n`, `''`, `""`, ` `` `, `null`, `undefined`, `NaN`

## Element Variables

- 렌더링 된 element를 변수로 취급 가능합니다.

## Inline Conditions

- 조건문을 코드 안에 집어넣는 것

### InlineIf

- `true && expression` → `expression`
- `false && expression` → `false`

## 이벤트 핸들링

- 이벤트 이름이 `onclick`에서 `onClick`으로 변경 (Camel case)
- 전달하려는 함수는 문자열에서 함수 그대로 전달.
- 이벤트가 발생했을 때 해당 이벤트를 처리하는 함수를 "이벤트 핸들러" 또는 "이벤트 리스너"라고 부릅니다.

### 이벤트 핸들러 추가하는 방법

- 버튼을 클릭하면 이벤트 핸들러 함수인 `handleClick()` 함수를 호출하도록 합니다.
- `bind`를 사용하지 않으면 `this.handleClick`은 글로벌 스코프에서 호출되어 `undefined`가 됩니다.
- `bind`를 사용하지 않으려면 화살표 함수를 사용할 수 있습니다. (참고: 클래스 컴포넌트는 이제 거의 사용하지 않음)

## 7장: 훅의 규칙

### 첫 번째 규칙

- 최상위 레벨에서만 호출해야 합니다. 반복문, 조건문, 중첩된 함수 안에서 호출하면 안됩니다.

### 두 번째 규칙

- 함수형 컴포넌트에서만 호출해야 합니다. 일반 자바스크립트 함수에서 호출하면 안됩니다.

### 추가 내용

- 커스텀 훅을 만들어 사용할 수 있습니다.

# ---------------------------------------------------

# 4월 17일 강의 내용

# 주제: State와 생명 주기에 대한 이해

# State: React 컴포넌트의 상태를 관리하는 개념으로, 컴포넌트의 동적인 변화를 처리하는 데 사용됩니다. State는 컴포넌트의 내부에 저장되며, setState() 함수를 통해 업데이트됩니다.

# 생명 주기(Lifecycle): React 컴포넌트는 생성부터 소멸까지의 여러 단계를 가집니다. 이러한 단계를 생명 주기라고 하며, 컴포넌트의 상태 변화와 관련된 작업을 수행할 수 있습니다.

# 주제: 훅(Hook)에 대한 소개

# 훅(Hook): React v16.8에서 도입된 기능으로, 함수형 컴포넌트에서 상태 관리와 생명 주기 기능을 사용할 수 있게 해줍니다. useState, useEffect 등의 내장 훅을 사용하여 기능을 활용할 수 있습니다.

# ---------------------------------------------------

# 4월 3일 강의 내용

# 주제: 컴포넌트(Component)에 대한 이해

# Props의 개념, 특징, 사용법

# Props(Property): React 컴포넌트 간에 데이터를 전달하는 메커니즘입니다. 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달할 때 사용됩니다.

# 특징:

# Props는 읽기 전용(immutable)입니다. 자식 컴포넌트에서 Props를 변경할 수 없습니다.

# 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달할 때 사용됩니다.

# 사용법:

# jsx

# Copy code

# // 부모 컴포넌트에서 자식 컴포넌트에 props 전달

# <MyComponent name="John" age={30} />

# // 자식 컴포넌트에서 props 사용

# const MyComponent = (props) => {

# return <div>{props.name}, Age: {props.age}</div>;

# }

# 컴포넌트의 종류

# 함수 컴포넌트(Function Component): 함수 형태로 정의되는 컴포넌트로, props를 인자로 받아 JSX를 반환합니다.

# 클래스 컴포넌트(Class Component): 클래스 형태로 정의되는 컴포넌트로, React.Component 클래스를 상속받아 render() 메서드를 구현합니다.

# 컴포넌트 이름짓기

# 컴포넌트의 이름은 대문자로 시작해야 합니다.

# 컴포넌트의 이름은 해당 컴포넌트가 수행하는 기능을 잘 설명해야 합니다.

# 컴포넌트 렌더링

# React 애플리케이션에서 컴포넌트를 화면에 렌더링하는 과정입니다.

# ReactDOM.render() 함수를 사용하여 루트 컴포넌트를 지정하고, 해당 컴포넌트를 실제 DOM에 렌더링합니다.

# 컴포넌트 합성

# 여러 개의 작은 컴포넌트를 조합하여 복잡한 UI를 만드는 기술입니다.

# 각 컴포넌트는 재사용 가능하며, 복잡한 UI를 구성하는 데 유용합니다.

# 컴포넌트 추출

# 컴포넌트가 너무 복잡해지거나 재사용성을 높이기 위해 부분적으로 컴포넌트를 추출하는 기술입니다.

# 추출된 컴포넌트는 독립적으로 테스트하거나 재사용할 수 있습니다.

# ---------------------------------------------------

# 3월 27일 강의 내용

# 주제: JSX 소개

# JSX(JavaScript XML): React에서 UI를 구성하기 위한 JavaScript의 확장 문법입니다. XML과 유사한 문법을 사용하여 React 엘리먼트를 작성할 수 있습니다. JSX는 가독성이 뛰어나고, React의 컴파일러가 일반 JavaScript 코드로 변환하기 때문에 편리하게 사용할 수 있습니다.

# 역할: React 엘리먼트를 생성하는 데 사용됩니다.

# 장점: 가독성이 뛰어나며, 동적인 UI 작성이 가능합니다.

# 사용법: JavaScript 표현식을 중괄호 {}로 감싸서 JSX 내부에 삽입할 수 있습니다.

# 주제: 엘리먼트(Element) 소개

# 엘리먼트(Element): React 애플리케이션의 구성 요소로, UI를 표현하는 최소 단위입니다. React 엘리먼트는 가상 DOM에 해당하는 객체로서, 화면에 렌더링되기 위한 정보를 포함합니다.

# 정의: 엘리먼트는 React에서 UI를 구성하는 기본적인 요소입니다. React 엘리먼트는 가상 DOM에 렌더링되며, JavaScript 객체로 취급됩니다.

# 생김새: JavaScript 객체로서 {type, props, children}와 같은 구조를 가집니다.

# 특징: 불변성을 가지며, 가상 DOM에 렌더링되어 성능을 향상시킵니다.

# 엘리먼트 렌더링하는 법: ReactDOM.render() 함수를 사용하여 실제 DOM에 렌더링합니다.

# ---------------------------------------------------

# 3월 20일 강의 내용

# 주제: 리액트(React) 소개

# 리액트(React): 페이스북에서 개발된 UI 라이브러리로, 사용자 인터페이스를 구축하기 위한 JavaScript 라이브러리입니다. 가상 DOM을 활용하여 성능을 최적화하고, 컴포넌트 기반 아키텍처를 제공하여 개발 생산성을 높입니다.

# 장점: 가상 DOM을 사용하여 효율적인 렌더링을 지원하여 성능이 우수합니다. 코드 재사용성과 유지보수성이 뛰어나며, 업데이트 사항을 빠르게 반영할 수 있습니다.

# 단점: 초기 학습 곡선이 높을 수 있고, 라이브러리의 생태계가 다양하고 빠르게 변하기 때문에 최신 트렌드를 따라가는 것이 어려울 수 있습니다.

# ---------------------------------------------------

# 3월 13일 강의 내용

# 주제: GitHub 사용법 소개

# GitHub 사용법: 협업과 버전 관리를 위한 분산 버전 관리 시스템으로, 소스 코드를 저장하고 공유하는 데 사용됩니다. GitHub을 통해 프로젝트를 관리하고 다른 사용자와 협업할 수 있습니다.

# VSCode와 GitHub 연동: VSCode의 Git 기능을 사용하여 GitHub과 연동할 수 있습니다.
```
````
