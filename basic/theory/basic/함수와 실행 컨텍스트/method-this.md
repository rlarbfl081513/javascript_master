# ✅ this가 뭔데

### this는 "누가 나를 호출했는가"에 따라 결정됨
```js
const obj = {
  name: '규리',
  sayHi: function () {
    console.log(this.name); // 규리
  }
};
obj.sayHi();
```

### 비유로 이해하기
- **일반 함수**: "나는 독립적이야! 호출할 때 누가 날 불렀는지 보고 결정할게!"
- **화살표 함수**: "난 생각 안 해. 그냥 바깥 함수의 this 따라갈래."

### 정리
| 표현 | 의미 |
|------|------|
| 자신의 this | 일반 함수가 **자기 기준으로 this 결정** (window 등) |
| 외부 this | 화살표 함수가 **바깥 함수의 this를 그대로 상속** |

---

## 📌 3. 사용 시 주의사항

| 구분             | 일반 함수 | 화살표 함수 |
|------------------|-----------|--------------|
| `this` 바인딩     | 있음      | ❌ 없음 (외부 상속) |
| 생성자 함수 사용 | 가능      | ❌ 불가능       |
| 메서드 정의      | ✅ 추천    | ❌ 피해야 함     |
| 콜백 함수        | 사용 가능 | ✅ 더 간결함     |

---

## 📌 4. map/forEach에서의 예시

```js
const persons = [
  { name: 'aaa' },
  { name: 'kkk' }
];

const result1 = persons.map(function (person) {
  return person.name;
});

const result2 = persons.map((person) => {
  return person.name;
});

console.log(result1); // ['aaa', 'kkk']
console.log(result2); // ['aaa', 'kkk']
```

### 이렇게 보자
- 코드 길이는 비슷할 수 있지만,
- **화살표 함수는 일관된 `this` + 깔끔한 콜백 작성**에 강점

---

## 🔚 정리
- 화살표 함수는 짧은 문법과 `this` 유지에 유리하다
- 일반 함수는 메서드, 생성자, 복잡한 `this` 사용에 적합하다
- 목적에 따라 상황에 맞게 선택하는 것이 가장 중요하다



# ✅ `this`가 다르게 동작하는 이유
**함수를 선언한 방식**과 **호출한 방식**에 따라 `this`의 값이 달라지기 때문
---

### ✅ 1. 메서드로 호출할 때 vs 단순 호출할 때

```js
const person = {
  name: 'Alice',
  greeting: function () {
    return `Hello my name is ${this.name}`
  },
}
console.log(person.greeting()) // Hello my name is Alice
```

- 여기서 `this`는 `person`을 가리켜.
- **이유**: `person.greeting()`처럼 **객체의 메서드로 호출**하면 `this`는 그 객체를 가리켜.

---

```js
const myFunc = function () {
  return this
}
console.log(myFunc()) // window (브라우저 기준)
```

- 여기선 그냥 `myFunc()`로 호출.
- **단순 함수 호출**이기 때문에, `this`는 **전역 객체** (`window` or `global` in Node.js).
- strict mode에서는 `undefined`.

---

### ✅ 2. 객체의 메서드로 호출

```js
const myObj = {
  data: 1,
  myFunc: function () {
    return this
  }
}
console.log(myObj.myFunc()) // myObj
```

- 메서드 호출 → `this`는 `myObj`를 가리킴.
- `myObj.myFunc()` 방식이므로 객체 내부 함수에서의 `this`는 해당 객체를 참조함.

---

### ✅ 3. 중첩 함수 안에서의 this

#### 3.1 일반 함수 사용
```js
const myObj2 = {
  numbers: [1, 2, 3],
  myFunc: function () {
    this.numbers.forEach(function (number) {
      console.log(this) // window
    })
  }
}
```

- `forEach` 안의 **콜백 함수는 일반 함수**.
- 일반 함수에서의 `this`는 **전역 객체**(`window`).
- `this.numbers.forEach(...)`에서 `this`는 `myObj2`지만,
  그 안에 **function(number) { ... }**은 **별도의 함수로 간주**돼서,
  이 함수 안의 `this`는 `myObj2`가 아니라 `window`가 되는 거야.

#### 해결 방법: 3.2 화살표 함수 사용
```js
const myObj3 = {
  numbers: [1, 2, 3],
  myFunc: function () {
    this.numbers.forEach((number) => {
      console.log(this) // myObj3
    })
  }
}
```

- 화살표 함수는 **자신만의 `this`를 가지지 않아**.
- 바깥 스코프의 `this`를 그대로 사용해.
- 여기서 바깥 스코프는 `myFunc()`이고, 그 `this`는 `myObj3`.
- 그래서 `console.log(this)`는 `myObj3`가 출력돼.

---

### ✨ 요약표

| 상황                        | `this`가 가리키는 대상        |
|-----------------------------|-----------------------------|
| 단순 함수 호출 (`f()`)      | 전역 객체 (`window`)         |
| 메서드 호출 (`obj.f()`)     | 해당 객체 (`obj`)             |
| 중첩 일반 함수              | 전역 객체 (`window`)         |
| 중첩 화살표 함수            | 바깥 `this`를 그대로 사용     |

---
