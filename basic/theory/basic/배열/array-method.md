# JavaScript - every() vs some() 메서드 비교

자바스크립트 배열에서 **모든 요소가 조건을 만족하는지** 또는 **하나라도 만족하는지**를 판단할 때 사용하는 메서드입니다.

---

## ✅ every() 메서드

> 배열의 **모든 요소가 주어진 조건을 만족**하면 `true`, 아니면 `false`

### 문법
```js
arr.every(callback(element, index, array))
```

### 예제
```js
const array = [1, 2, 3, 4, 5];

const isAllEven = array.every((el) => el % 2 === 0);
console.log(isAllEven); // false
```

### 해설
- `1 % 2 === 0` → false → 조건을 만족하지 않음
- 하나라도 false면 전체 결과는 false

---

## ✅ some() 메서드

> 배열에 **하나라도 조건을 만족하는 요소가 있으면** `true`

### 문법
```js
arr.some(callback(element, index, array))
```

### 예제
```js
const array = [1, 2, 3, 4, 5];

const hasEven = array.some((el) => el % 2 === 0);
console.log(hasEven); // true
```

### 해설
- `2`, `4` 등 짝수가 존재하므로 → 하나라도 만족 → true

---

## ✅ every vs some 비교표

| 메서드 | 조건 모두 만족 | 조건 하나라도 만족 |
|--------|----------------|--------------------|
| every | ✅ true         | ❌ false           |
| some  | ❌ false        | ✅ true            |

---

## ✅ 어떤 카테고리에 정리하면 좋을까?

이 내용은 다음 중 한 카테고리에 넣는 것이 적절합니다:

### 추천 폴더명 예시
- `Array_Methods` (가장 일반적)
- `JS_배열_고차함수`
- `배열_탐색_조건검사`

> 💡 `forEach`, `map`, `filter`, `reduce` 같이 **배열을 순회하면서 동작하는 고차 함수들**과 함께 정리하면 아주 좋아요!

