# 리액트의 리렌더링 (Re-rendering)

## 리렌더링이란?

리렌더링은 리액트 컴포넌트가 자신의 UI를 다시 계산하고 업데이트하는 과정입니다. 이는 리액트의 핵심 기능 중 하나로, 애플리케이션의 상태 변화를 효율적으로 UI에 반영합니다.

## 리렌더링이 발생하는 경우

1. **상태(State) 변경**

   - `useState`, `useReducer` 등을 통해 관리되는 상태가 변경될 때

   ```jsx
   const [count, setCount] = useState(0);
   // setCount(1)을 호출하면 리렌더링 발생
   ```

2. **속성(Props) 변경**

   - 부모 컴포넌트로부터 전달받는 props가 변경될 때

   ```jsx
   function Child({ name }) {
     return <div>{name}</div>;
   }
   // Parent 컴포넌트에서 name prop이 변경되면 Child 컴포넌트 리렌더링
   ```

3. **부모 컴포넌트 리렌더링**

   - 부모 컴포넌트가 리렌더링되면, 기본적으로 모든 자식 컴포넌트도 리렌더링됨

4. **Context 변경**

   - React.Context를 통해 제공되는 값이 변경될 때

   ```jsx
   const ThemeContext = React.createContext();
   // ThemeContext.Provider의 value가 변경되면 Consumer 컴포넌트들 리렌더링
   ```

5. **forceUpdate() 호출**
   - 클래스 컴포넌트에서 `forceUpdate()` 메서드를 직접 호출할 때

## 리렌더링 과정

1. **렌더 단계 (Render Phase)**

   - 컴포넌트의 `render` 함수(또는 함수형 컴포넌트 자체)가 호출됨
   - 가상 DOM(Virtual DOM)이 생성됨
   - 이전 가상 DOM과 새로운 가상 DOM을 비교(Diffing)

2. **커밋 단계 (Commit Phase)**
   - 실제 DOM에 변경사항을 적용
   - 라이프사이클 메서드 또는 훅이 호출됨 (예: `useEffect`)

## 리렌더링 최적화

1. **React.memo**

   - 함수형 컴포넌트를 메모이제이션

   ```jsx
   const MemoizedComponent = React.memo(MyComponent);
   ```

2. **useCallback**

   - 함수를 메모이제이션하여 불필요한 리렌더링 방지

   ```jsx
   const memoizedCallback = useCallback(() => {
     doSomething(a, b);
   }, [a, b]);
   ```

3. **useMemo**

   - 계산 비용이 큰 값을 메모이제이션

   ```jsx
   const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
   ```

4. **shouldComponentUpdate (클래스 컴포넌트)**
   - 리렌더링 여부를 수동으로 제어
   ```jsx
   shouldComponentUpdate(nextProps, nextState) {
     return nextProps.id !== this.props.id;
   }
   ```

## 주의사항

1. 모든 상태 변경이 리렌더링을 유발하지는 않습니다. 리액트는 상태가 실제로 변경되었을 때만 리렌더링을 수행합니다.

2. 리렌더링이 항상 실제 DOM 업데이트로 이어지는 것은 아닙니다. 리액트는 가상 DOM 비교를 통해 실제 변경이 필요한 경우에만 DOM을 업데이트합니다.

3. 과도한 리렌더링은 성능 저하의 원인이 될 수 있으므로, 적절한 최적화 기법을 사용하는 것이 중요합니다.

리렌더링은 리액트의 선언적 UI 패러다임의 핵심이며, 효율적인 상태 관리와 UI 업데이트를 가능하게 합니다. 올바르게 이해하고 활용하면 반응적이고 성능이 좋은 애플리케이션을 구축할 수 있습니다.
