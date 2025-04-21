# 자바스크립트 예습 정리 - 핵심 개념 및 코드 모음

## 1. classList 조작

```js
const tag = document.querySelector('h1');
tag.classList.add('title');
tag.classList.remove('title');
tag.classList.toggle('highlight');
```

## 2. DOM 요소 선택

```js
document.querySelector('.class');
document.querySelector('#id');
document.querySelectorAll('tag');
```

## 3. 텍스트 및 속성 조작

```js
const el = document.querySelector('#name');
el.textContent = '홍길동';

const img = document.querySelector('img');
img.setAttribute('src', 'profile.jpg');
img.setAttribute('alt', '프로필 이미지');
```

## 4. 요소 반복 처리

```js
const items = document.querySelectorAll('b');
items.forEach(el => {
  el.classList.add('highlight');
});
```

## 5. DOM 요소 생성 및 삽입

```js
const newP = document.createElement('p');
const newB = document.createElement('b');
newB.id = 'sns';
newB.textContent = 'hgd@sns.com';
newP.append('SNS : ', newB);

const h2List = document.querySelectorAll('h2');
let contactTitle;
h2List.forEach(h2 => {
  if (h2.textContent.trim() === '연락처') {
    contactTitle = h2;
  }
});
contactTitle.insertAdjacentElement('afterend', newP);
```

## 6. 스타일 직접 조작

```js
const el = document.querySelector('p');
el.style.color = 'blue';
el.style.fontSize = '2rem';
el.style.border = '1px solid black';
```

## 7. 실습용 구조 예시 (HTML)

```html
<h1 class="heading">DOM</h1>
<p class="content">content1</p>
<p class="content">content2</p>
<p class="content">content3</p>
<ul>
  <li>list1</li>
  <li>list2</li>
</ul>
```

> 이 문서는 자바스크립트 예습을 위해 사용된 핵심 코드와 개념들을 정리한 자료입니다.



## classList란 (상세 설명)
- HTML 요소의 `class` 속성을 **JavaScript로 조작**할 수 있게 해주는 속성.
- `add`, `remove`, `toggle` 등을 통해 클래스 이름을 동적으로 제어 가능.
- `.classList`는 `DOMTokenList` 객체이며, `배열처럼 여러 클래스 이름을 관리`할 수 있음.

### 예시
```js
const element = document.querySelector('.heading');
element.classList.add('red');
```

**결과**:
- `.heading` 요소가 `"red"` 클래스를 추가로 가지게 됨.
- HTML 구조: `<h1 class="heading red">DOM</h1>`
- 브라우저 화면: `.red` 클래스에 스타일이 지정되어 있다면 시각적으로 반영됨.
- 콘솔창: `element.classList` 출력 시 → `DOMTokenList(2) ['heading', 'red']`

---

## 주요 classList 메서드 정리 (상세)

| 메서드 | 설명 | 예시 | 예상 출력 |
|--------|------|------|-----------|
| `.add("클래스명")` | 클래스 추가 | `el.classList.add("red")` | `['기존', 'red']` |
| `.remove("클래스명")` | 클래스 제거 | `el.classList.remove("red")` | `['기존']` |
| `.toggle("클래스명")` | 있으면 제거, 없으면 추가 | `el.classList.toggle("red")` | 상태에 따라 `['기존', 'red']` 또는 `['기존']` |

---

### 예제 코드
```js
const h1Tag = document.querySelector('.heading');

h1Tag.classList.add('red');
console.log(h1Tag.classList);  // ['heading', 'red']

h1Tag.classList.remove('red');
console.log(h1Tag.classList);  // ['heading']

h1Tag.classList.toggle('red');
console.log(h1Tag.classList);  // ['heading', 'red']
```

### 콘솔 출력
```
DOMTokenList(2) ['heading', 'red', value: 'heading red']
DOMTokenList ['heading', value: 'heading']
DOMTokenList(2) ['heading', 'red', value: 'heading red']
```
