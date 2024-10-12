# The onClick Parable

## 주요 포인트

1. 단순 입력 필드의 `onChange` 이벤트와 버튼에 바인딩한 `onClick` 이벤트만 사용하는 것은 문제가 있다.
   - 이유 : 만약 사용자가 입력 필드에 값을 입력 후 Enter 를 입력한다면 버튼에 바인딩한 `onClick` 이벤트가 호출되지 않는다.
   - 이를 위해 `onKeyDown` 이벤트를 추가하여 Enter 키를 감지할 수 있지만, 이 방법은 브라우저가 이미 알고 있는 기능을 다시 구현하는 것에 지나지 않는다.
2. `<form>` 태그와 `onSubmit` 이벤트를 활용하는 것이 더 좋은 방법이다.

## 잘못된 접근 방식

- 버튼에 `onClick` 이벤트만 사용
- 입력 필드에 `onKeyDown` 이벤트 추가

## 올바른 접근 방식

```jsx
<form
  onSubmit={(event) => {
    event.preventDefault();
    runSearch(searchTerm);
  }}
>
  <input
    type="text"
    value={searchTerm}
    onChange={(event) => setSearchTerm(event.target.value)}
  />
  <button>Search!</button>
</form>
```

## `<form>` 사용의 이점

1. 버튼 클릭과 Enter 키 입력 모두 처리
2. 브라우저 기본 기능 활용 (예: 클라이언트 측 유효성 검사)
3. 코드 간소화

## `event.preventDefault()` 필요성

- 기본적으로 폼 제출은 페이지를 새로고침함
- 현대 React 앱에서는 전체 페이지 리로드 대신 부분 업데이트가 필요
- `event.preventDefault()`로 기본 동작 방지

## 결론

폼 처리 시 `<form>` 태그와 `onSubmit` 이벤트를 사용하여 웹 플랫폼의 기본 기능을 최대한 활용하는 것이 좋다.
