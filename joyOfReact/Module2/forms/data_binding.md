# 데이터 바인딩

## 개요

- 데이터 바인딩은 상태(state)를 특정 폼 입력과 동기화하는 과정입니다.
- React에서는 주로 `useState` 훅과 `value` 및 `onChange` 속성을 사용하여 구현합니다.

## 제어 컴포넌트 vs 비제어 컴포넌트

- 제어 컴포넌트: React가 입력값을 관리 (`value` 속성 사용)
- 비제어 컴포넌트: React가 입력값을 관리하지 않음
- 주의: 한 입력 요소를 제어/비제어 상태 사이에서 전환하지 않아야 함

  - 주의사항은 개별 입력 요소의 상태를 일관되게 유지하라는 것이며, 여러 입력 요소를 다룰 때 각각 다른 방식으로 관리하는 것은 문제가 되지 않음
    ```jsx
    function Form() {
      const [value, setValue] = React.useState("");
      return (
        <input
          value={value} // 첫 렌더링에서는 제어 컴포넌트
          onChange={(e) => {
            if (e.target.value === "uncontrol") {
              // 이렇게 하면 ❎
              // 특정 조건에서 value prop을 제거하여 비제어 컴포넌트로 만듦
              e.target.removeAttribute("value");
            } else {
              setValue(e.target.value);
            }
          }}
        />
      );
    }
    ```

## 일반적인 실수와 해결책

- 문제: `useState`의 초기값을 설정하지 않으면 `undefined`가 되어 비제어에서 제어로 전환될 수 있음
- 해결: 항상 정의된 값(예: 빈 문자열)으로 초기화
  ```javascript
  const [username, setUsername] = React.useState("");
  ```

## 대안적 접근: FormData

- `FormData`를 사용하여 제출 시 데이터 수집 가능
- 장점: 간단하고 직관적
- 단점: 실시간 UI 업데이트나 복잡한 폼 로직에는 적합하지 않을 수 있음

## 결론

- 대부분의 경우 제어 컴포넌트 방식이 가장 유연하고 안정적
- 상황에 따라 `FormData` 사용도 고려해볼 수 있음
