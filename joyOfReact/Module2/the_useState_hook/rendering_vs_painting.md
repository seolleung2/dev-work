# React의 렌더링과 커밋 과정

React 애플리케이션에서 UI 업데이트는 세 단계로 이루어집니다: 트리거, 렌더, 커밋. 이 과정을 이해하면 React 코드의 실행 방식과 동작을 더 잘 이해할 수 있습니다.

## 1. 렌더링 트리거 (Trigger)

렌더링이 트리거되는 두 가지 경우가 있습니다:

1. 컴포넌트의 초기 렌더링
2. 컴포넌트(또는 그 조상 중 하나)의 상태가 업데이트된 경우

![React as a waiter](https://react.dev/images/docs/illustrations/i_render-and-commit1.png)

## 2. 렌더링 (Render)

렌더링이 트리거되면 React는 컴포넌트를 호출하여 화면에 표시할 내용을 파악합니다.

- 초기 렌더링에서는 루트 컴포넌트를 호출합니다.
- 이후 렌더링에서는 상태 업데이트로 인해 렌더링이 트리거된 함수 컴포넌트를 호출합니다.

이 과정은 재귀적으로 진행되며, 중첩된 컴포넌트가 없을 때까지 계속됩니다.

![React in the kitchen](https://react.dev/images/docs/illustrations/i_render-and-commit2.png)

### 주의사항

렌더링은 항상 순수한 계산이어야 합니다:

- 동일한 입력에 대해 항상 동일한 JSX를 반환해야 합니다.
- 렌더링 이전에 존재하던 객체나 변수를 변경해서는 안 됩니다.

## 3. DOM에 커밋 (Commit)

컴포넌트를 렌더링(호출)한 후, React는 DOM을 수정합니다.

- 초기 렌더링: React는 `appendChild()` DOM API를 사용하여 생성한 모든 DOM 노드를 화면에 표시합니다.
- 리렌더링: React는 렌더링 출력과 일치하도록 최소한의 필요한 작업을 수행합니다.

**중요**: React는 렌더 간에 차이가 있는 경우에만 DOM 노드를 변경합니다.

![React serving the UI](https://react.dev/images/docs/illustrations/i_render-and-commit3.png)

## 브라우저 페인팅

React가 DOM을 업데이트한 후, 브라우저는 화면을 다시 그립니다. 이 과정을 "브라우저 렌더링"이라고 하지만, 혼동을 피하기 위해 "페인팅"이라고 부릅니다.

## 렌더링 vs 페인팅

- **렌더링**: React가 컴포넌트를 호출하여 변경 사항을 파악하는 과정 (재조정 또는 "차이 찾기 게임"이라고도 함)
- **커밋**: React가 DOM을 편집하여 최신 스냅샷과 일치하도록 하는 과정
- **페인팅**: 브라우저가 DOM 노드가 편집될 때 관련 픽셀을 다시 그리는 과정

모든 리렌더링이 리페인팅을 필요로 하는 것은 아닙니다. 스냅샷 간에 변경된 것이 없다면 React는 DOM 노드를 편집하지 않으며, 따라서 아무것도 리페인팅되지 않습니다.

[출처: https://react.dev/learn/render-and-commit](https://react.dev/learn/render-and-commit)
