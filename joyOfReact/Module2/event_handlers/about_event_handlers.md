# React의 이벤트 핸들러

## 1. 이벤트의 중요성

- 사용자 상호작용에 따라 수많은 이벤트가 발생
- 동적 웹 애플리케이션에서 이벤트는 상태 변경을 트리거하는 데 중요
- 사용자 경험(UX)을 향상시키는 핵심 요소

## 2. 이벤트 리스닝 방법

### 2.1 JavaScript의 기본 방법 (addEventListener)

```javascript
const button = document.querySelector("button");

button.addEventListener("click", () => {
  alert("Button clicked!");
});
```

### 2.2 HTML 방식

```html
<button onclick="alert('Button clicked!')">Click me</button>
```

### 2.3 React 방식 (권장)

```javascript
function Button() {
  function handleClick() {
    alert("Button clicked!");
  }

  return <button onClick={handleClick}>Click me</button>;
}
```

## 3. React에서 이벤트 핸들러 사용의 장점

- 자동 정리: 컴포넌트가 언마운트될 때 이벤트 리스너를 자동으로 제거하여 메모리 누수 방지
- 성능 향상: React의 이벤트 위임(event delegation) 시스템을 통한 최적화
- DOM 직접 조작 회피: React의 선언적 추상화 유지로 코드의 예측 가능성과 유지보수성 향상
- 크로스 브라우저 호환성: React가 브라우저 간 차이를 처리하여 일관된 동작 보장

## 4. React 추상화 내에서 작업하기

- DOM을 직접 조작하지 않고 React의 방식을 따르는 것이 중요
- 새로운 기술 학습 시 기존 방식에 맞추려 하지 말고, 그 기술의 방식을 따르는 것이 효과적

## 5. HTML과의 차이점

### 5.1 카멜 케이스 사용

- `onClick`, `onChange`, `onKeyDown` 등 사용

### 5.2 함수 참조 전달

```jsx
// ✅ 올바른 방법:
<button onClick={doSomething} />
// 🚫 잘못된 방법:
<button onClick={doSomething()} />
```

- 함수를 즉시 호출하지 않고, 참조를 전달해야 함
- React가 나중에 이벤트 발생 시 함수를 호출할 수 있도록 함

### 5.3 이벤트 객체 처리

```jsx
function handleClick(event) {
  event.preventDefault(); // 기본 동작 방지
  console.log(event.target); // 이벤트가 발생한 요소
}

return <button onClick={handleClick}>Click me</button>;
```

- React는 W3C 명세를 따르는 합성 이벤트(SyntheticEvent) 객체를 제공
- 크로스 브라우저 호환성을 보장하며, 네이티브 이벤트와 유사하게 사용 가능

## 6. 조건부 이벤트 핸들링

```jsx
function ConditionalButton({ isDisabled }) {
  return (
    <button
      onClick={isDisabled ? undefined : handleClick}
      disabled={isDisabled}
    >
      Click me
    </button>
  );
}
```

- 조건에 따라 이벤트 핸들러를 동적으로 할당하거나 제거할 수 있음
- UI의 상태에 따른 유연한 상호작용 구현 가능
