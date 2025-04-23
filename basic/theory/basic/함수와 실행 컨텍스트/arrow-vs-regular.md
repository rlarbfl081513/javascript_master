# JavaScript - 화살표 함수 vs 일반 함수

## 📌 1. 문법 비교

### 일반 함수 (Function Expression)
```js
const greet = function(name) {
  return `Hello, ${name}`;
};
```

### 화살표 함수 (Arrow Function)
```js
const greet = (name) => {
  return `Hello, ${name}`;
};
```

### 한 줄 반환은 더 간결하게
```js
const square = x => x * 2;
```

- 파라미터가 하나면 괄호 생략 가능
- 한 줄 반환이면 `{}`와 `return`도 생략 가능

---

## 📌 2. this 바인딩 차이 (핵심)

### 일반 함수는 자신의 this를 가짐
```js
const obj = {
  name: '규리',
  greet: function () {
    setTimeout(function () {
      console.log(this.name); // ❌ undefined
    }, 1000);
  }
};
```

- `setTimeout`의 콜백은 일반 함수이므로,
  `this`는 전역 객체(window)를 가리킴
- **일반 함수는 자신만의 `this`를 만들어냄**

### 화살표 함수는 외부 this를 상속함
```js
const obj = {
  name: '규리',
  greet: function () {
    setTimeout(() => {
      console.log(this.name); // ✅ '규리'
    }, 1000);
  }
};
```

- `setTimeout` 안의 화살표 함수는 `greet()`의 `this`를 그대로 사용
- **화살표 함수는 자기만의 this를 만들지 않고, 외부 this를 그대로 따름**

---

