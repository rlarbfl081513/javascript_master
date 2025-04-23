# this, 화살표 함수 연습 문제 모음 (예상 → 실습 → 해설)

자바스크립트에서 `this`, `화살표 함수`, `일반 함수`의 차이를 직접 실습하며 이해할 수 있도록 구성한 연습용 자료입니다.

---

## ✅ 연습 1: 일반 함수 vs 화살표 함수의 this

### 코드
```js
const obj = {
  name: '규리',
  sayHi: function () {
    console.log(this.name);
  },
  sayHiArrow: () => {
    console.log(this.name);
  }
};

obj.sayHi();      // ?
obj.sayHiArrow(); // ?
```

### ❓ 예상
- 각각 어떤 결과가 나올까요?
- 왜 그런 결과가 나올까요?

### ✅ 해설
- `sayHi()`는 일반 함수 → `this === obj` → '규리'
- `sayHiArrow()`는 화살표 함수 → `this === window` → undefined (브라우저 기준)

---

## ✅ 연습 2: setTimeout 안의 함수

### 코드
```js
const obj = {
  name: '규리',
  greet: function () {
    setTimeout(function () {
      console.log(this.name);
    }, 500);
  }
};

obj.greet(); // ?
```

### ❓ 예상
- 출력되는 값은 무엇인가요?
- 왜 그런 결과가 나올까요?

### 💡 힌트
- `setTimeout` 안의 function 은 누구 소속일까?

---

## ✅ 연습 3: 위 코드를 화살표 함수로 바꿔보기

```js
const obj = {
  name: '규리',
  greet: function () {
    setTimeout(() => {
      console.log(this.name);
    }, 500);
  }
};

obj.greet(); // ?
```

### ❓ 예상
- 이제는 결과가 어떻게 바뀌나요?

### ✅ 해설
- 화살표 함수는 외부의 this(obj)를 그대로 상속 → 결과: '규리'

---

## ✅ 연습 4: forEach에서의 this

```js
const team = {
  name: 'SSAFY',
  members: ['규리', '민수'],
  introduce: function () {
    this.members.forEach(function (member) {
      console.log(`${member} is in ${this.name}`);
    });
  }
};

team.introduce(); // ?
```

### ❓ 예상
- 결과는 어떤가요?
- 왜 SSAFY가 아닌 undefined가 뜰까요?

---

## ✅ 연습 5: 위의 forEach를 화살표 함수로 고치기

```js
const team = {
  name: 'SSAFY',
  members: ['규리', '민수'],
  introduce: function () {
    this.members.forEach((member) => {
      console.log(`${member} is in ${this.name}`);
    });
  }
};

team.introduce(); // ?
```

### ✅ 해설
- 화살표 함수는 외부의 this(team)를 그대로 사용
- 결과: 규리 is in SSAFY, 민수 is in SSAFY

---

## ✅ 연습 6: map에서 화살표 함수 vs 일반 함수

```js
const persons = [
  { name: 'aaa' },
  { name: 'bbb' },
];

const result1 = persons.map(function (person) {
  return person.name;
});

const result2 = persons.map((person) => person.name);

console.log(result1); // ?
console.log(result2); // ?
```

### ❓ 예상
- 두 결과가 같을까요? 다를까요?
- 화살표 함수의 장점은 무엇일까요?

### ✅ 해설
- 둘 다 ['aaa', 'bbb'] 출력됨
- 화살표 함수는 짧고 간결해서 콜백에 자주 사용됨

---

## ✨ 마무리 팁
- `this`가 헷갈리면 "누가 이 함수를 불렀는가"를 생각해보자
- 화살표 함수는 자기 스스로 this를 만들지 않고 바깥 것을 그대로 씀
- 직접 손으로 예상하고 결과 확인하는 연습을 자주 해보는 게 가장 좋은 학습 방법!

필요 시 `bind`, `call`, `apply` 실습도 추가 가능!

