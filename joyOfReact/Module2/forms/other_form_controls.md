# React에서의 폼 컨트롤

## 주요 포인트

- React는 다양한 폼 컨트롤을 일관된 방식으로 다룰 수 있게 해줍니다.
- 대부분의 폼 컨트롤은 `value`와 `onChange`를 사용하여 제어됩니다.
- 체크박스와 라디오 버튼은 `checked`와 `onChange`를 사용합니다.

## Select 태그

### 주요 사용법

```jsx
<select
  value={selectedOption}
  onChange={(event) => setSelectedOption(event.target.value)}
>
  <option value="option1">Option 1</option>
  <option value="option2">Option 2</option>
</select>
```

### 특징

- `value` 속성으로 현재 선택된 옵션을 제어
- `onChange` 이벤트로 선택 변경 감지
- `<option>` 태그로 선택 항목 정의
- `<optgroup>` 태그로 옵션 그룹화 가능

## Radio 버튼

### 기본 구조

```jsx
<div>
  <input
    type="radio"
    id="option1"
    name="radioGroup"
    value="option1"
    checked={selectedValue === "option1"}
    onChange={(e) => setSelectedValue(e.target.value)}
  />
  <label htmlFor="option1">Option 1</label>

  <input
    type="radio"
    id="option2"
    name="radioGroup"
    value="option2"
    checked={selectedValue === "option2"}
    onChange={(e) => setSelectedValue(e.target.value)}
  />
  <label htmlFor="option2">Option 2</label>
</div>
```

### 특징

- 여러 개의 독립적인 `<input>` 요소로 구성
- `name` 속성으로 같은 그룹임을 표시
- `checked` 속성으로 선택 상태 제어
- `value` 속성으로 각 옵션의 값 정의

### 주요 속성 설명

1. `id` 속성

   - 각 라디오 버튼의 고유 식별자
   - `label`의 `htmlFor` 속성과 연결되어 사용성 향상
   - 사용자가 라벨을 클릭해도 해당 라디오 버튼이 선택됨

2. `name` 속성

   - 같은 그룹의 라디오 버튼들은 동일한 `name` 값을 가져야 함
   - 브라우저가 이를 통해 같은 그룹임을 인식
   - 한 그룹 내에서 하나의 옵션만 선택 가능하게 함

3. `value` 속성

   - 각 라디오 버튼의 실제 값
   - 선택 시 이 값이 React 상태로 전달됨

4. `checked` 속성

   - 현재 선택된 상태인지를 나타냄
   - React 상태와 연동하여 제어

5. `onChange` 이벤트 핸들러
   - 선택 상태 변경 시 호출됨
   - 새로운 값을 React 상태에 반영

### label과의 연동

- `<label>` 태그는 `htmlFor` 속성을 통해 특정 라디오 버튼과 연결
- `htmlFor`의 값은 연결하려는 라디오 버튼의 `id`와 일치해야 함
- 이를 통해 라벨 클릭 시 해당 라디오 버튼이 선택되는 향상된 사용성 제공

### 접근성 고려사항

- 적절한 `label` 사용은 스크린 리더 사용자에게 중요한 컨텍스트 제공
- 그룹화된 라디오 버튼은 `<fieldset>`과 `<legend>`로 감싸 추가적인 컨텍스트 제공 가능

```jsx
<fieldset>
  <legend>선호하는 과일</legend>
  {/* 라디오 버튼들 */}
</fieldset>
```

### 주의사항

- 동일 그룹의 모든 라디오 버튼은 같은 `name`을 가져야 하지만, `id`는 각각 고유해야 함
- React에서는 `defaultChecked` 대신 `checked`를 사용하여 제어 컴포넌트로 만듦

### Radio vs Select 선택 기준

| 상황                                      | 권장 컨트롤 |
| ----------------------------------------- | ----------- |
| 많은 옵션 (예: 국가 목록)                 | Select      |
| 모든 옵션을 읽어야 할 때                  | Radio       |
| 기본 옵션이 대부분의 사용자에게 권장될 때 | Select      |
| 옵션이 2-3개일 때                         | Radio       |

## 기타 폼 컨트롤

- Textarea: `<textarea value={} onChange={} />`
- Checkbox: `<input type="checkbox" checked={} onChange={} />`
- Range: `<input type="range" value={} onChange={} />`
- Color Picker: `<input type="color" value={} onChange={} />`

모든 폼 컨트롤은 React에서 비슷한 패턴으로 다뤄집니다. 대부분 `value`(또는 `checked`)와 `onChange`를 사용하여 제어합니다.
