# React에서 이벤트 핸들러에 인자 전달하기

## 문제 상황

React에서 이벤트 핸들러 함수에 인자를 전달해야 할 때가 있습니다. 예를 들어:

```jsx
// 잘못된 방법:
<button onClick={setTheme}>Toggle theme</button>
<button onClick={setTheme('dark')}>Toggle theme</button>
```

## 해결책: 래퍼 함수 사용

```jsx
// 올바른 방법:
<button onClick={() => setTheme("dark")}>Toggle theme</button>
```

이 방법은 새로운 익명 화살표 함수를 생성하여 React에 전달합니다. 버튼 클릭 시 이 함수가 실행되어 `setTheme('dark')`를 호출합니다.

## 성능에 대한 오해

- 익명 함수 생성이 성능에 큰 영향을 미치지 않습니다.
- 함수 생성 비용은 매우 낮습니다.
- React는 최적화된 이벤트 위임 시스템을 사용합니다.
- 성능 최적화가 필요한 경우 React의 `useCallback` 훅을 사용할 수 있습니다 (Module 3에서 다룰 예정).

## 대안: bind 메서드

```jsx
<button onClick={setTheme.bind(null, "dark")}>Toggle theme</button>
```

이 방법도 유효하지만, React 커뮤니티에서는 덜 일반적입니다. 익명 래퍼 함수 사용을 권장합니다.

## React에서의 bind 메서드 사용

React 커뮤니티에서 `bind` 메서드는 이벤트 핸들러에 인자를 전달하는 데 자주 사용되지 않습니다. 그 이유는 다음과 같습니다:

1. **가독성**: 화살표 함수에 비해 `bind` 메서드는 덜 직관적이고 읽기 어려울 수 있습니다.

2. **일관성**: React 컴포넌트에서 화살표 함수를 사용하는 것이 더 일반적이며, 코드베이스 전체의 일관성을 유지하는 데 도움이 됩니다.

3. **학습 곡선**: 많은 React 개발자들이 화살표 함수에 더 익숙합니다.

4. **this 컨텍스트**: 클래스 컴포넌트에서 `bind`를 사용할 때 `this` 컨텍스트 관리가 복잡해질 수 있습니다.

## bind 메서드의 첫 번째 인자로 null 사용하기

`setTheme.bind(null, 'dark')`에서 첫 번째 인자로 `null`을 사용한 이유는 다음과 같습니다:

1. **this 컨텍스트가 필요 없는 경우**:

   - `setTheme` 함수가 특정 객체의 메서드가 아니라 독립적인 함수일 경우, `this` 컨텍스트가 중요하지 않습니다.
   - 함수형 컴포넌트나 훅을 사용하는 현대적인 React에서는 대부분의 경우 `this` 바인딩이 필요 없습니다.

2. **인자 전달에 초점**:

   - 여기서의 주요 목적은 'dark'라는 인자를 `setTheme` 함수에 전달하는 것입니다.
   - `this` 바인딩은 필요하지 않지만, `bind`의 부분 적용 기능을 활용하고 있습니다.

3. **관례적 사용**:
   - `this` 바인딩이 필요 없을 때 `null`이나 `undefined`를 사용하는 것은 JavaScript에서 흔한 관행입니다.

### 예시 비교

```jsx
// bind 메서드 사용 (덜 선호됨)
<button onClick={setTheme.bind(null, 'dark')}>Toggle theme</button>

// 화살표 함수 사용 (더 선호됨)
<button onClick={() => setTheme('dark')}>Toggle theme</button>
```
