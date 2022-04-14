---
title:  "[JavaScript] 유용한 10가지 배열 함수들"

categories:
  - JavaScript
tags:
  - [JavaScript]

toc: true
toc_sticky: true
 
date: 2022-04-14
last_modified_at: 2022-04-14
---
# 🙂 배열 (Array)
## 1. 배열을 문자열로 변환 (join)
### 내 답
```js
const fruits = ['apple', 'banana', 'orange'];
let str = '';
for(let i=0; i<fruits.length; i++){
    str += fruits[i];
    str += ' ';
}
console.log(str);
```
### API 사용
```js
const fruits = ['apple', 'banana', 'orange'];
const result1 = fruits.join();
const result2 = fruits.join(', ');
console.log(result1); // apple,banana,orange
console.log(result2); // apple, banana, orange
```

## 2. 문자열을 배열로 변환 (split)
### 내 답
```js
const fruits = '🍎, 🥝, 🍌, 🍒';
let arr = new Array();
for(let i=0; i<fruits.length; i++){
    arr.push(fruits);
}
console.log(arr);
```
### API 사용
```js
const fruits = '🍎, 🥝, 🍌, 🍒';
const result1 = fruits.split(',');
const result2 = fruits.split(',', 2); // 리턴받을 배열의 사이즈 지정
console.log(result1); // ['🍎', '🥝', '🍌', '🍒']
console.log(result2); // ['🍎', '🥝']
```

## 3. 배열의 순서 거꾸로 (reverse)
(정렬은 아님!)
### 내 답
```js
const arr = [1,2,3,4,5];
arr.sort(function(a,b){
    if(a<b) return 1;
    if(a===b) return 0;
    if(a>b) return -1;
});
console.log(arr);
```
### API 사용
```js
const arr = [1,2,3,4,5];
const result = arr.reverse();
console.log(result); // [ 5, 4, 3, 2, 1 ]
console.log(arr); // [ 5, 4, 3, 2, 1 ]
```
⚠️ reverse()를 사용할 때는 기존의 arr도 변경된다.

## 4. 주어진 배열의 첫번째와 두번째 요소를 제외한 새로운 배열 만들기 (slice)
### 내 답
```js
const arr = [1,2,3,4,5];
const newArr = new Array();
for(let i=0; i<arr.length; i++){
    newArr[i] = arr[i];
}
newArr.splice(0,2);
console.log(newArr);
```
⚠️ splice()를 사용할 때는 기존의 arr도 변경된다.
### API 사용
```js
const arr = [1,2,3,4,5];
const result = arr.slice(2, 5);
//const result = arr.slice(2, 4); // [3, 4] 
console.log(result);  // [3, 4, 5]
console.log(arr); // [1, 2, 3, 4, 5]
```
slice 사용법: `splice(시작 인덱스, 마지막 인덱스 + 1)`<br>
👍 slice()를 사용하면 기존의 arr는 변경되지 않는다.

# 🙂 오브젝트 배열 (Object Array)

```js
class Student {
    constructor(name, age, enrolled, score) {
      this.name = name;
      this.age = age;
      this.enrolled = enrolled;
      this.score = score;
    }
  }
  const students = [
    new Student('A', 29, true, 45),
    new Student('B', 28, false, 80),
    new Student('C', 30, true, 90),
    new Student('D', 40, false, 66),
    new Student('E', 18, true, 88),
  ];
```

## 5. score가 90인 학생 찾기 (find)
### 내 답
```js
students.forEach((std)=>{
    if(std.score===90)
        console.log(std.name);
});
```
### API 사용
```js
// const result = students.find(function(std) {
//   return std.score === 90; // 90점이라면 true 리턴
// })

// 위를 간단히!
const result = students.find((std) =>  std.score === 90);
console.log(result); // Student { name: 'C', age: 30, enrolled: true, score: 90 }
```

## 6. enrolled인 학생 배열 만들기 (filter)
### 내 답
```js
const stdArr = new Array();
students.forEach((std)=>{
    if(std.enrolled===true)
        stdArr.push(std.name);
});
console.log(stdArr);
```
### API 사용
```js
const result = students.filter((std) => std.enrolled);
console.log(result);
```
출력 결과
```js
[
  Student { name: 'A', age: 29, enrolled: true, score: 45 },
  Student { name: 'C', age: 30, enrolled: true, score: 90 },
  Student { name: 'E', age: 18, enrolled: true, score: 88 }
]
```

## 7. 학생들의 score 배열 만들기 (map)
### 내 답
```js
const scoreArr = new Array();
students.forEach((std)=>{
    scoreArr.push(std.score);
});
console.log(scoreArr);
```
### API 사용
만약 student를 받아서 그대로 student를 리턴한다면?
```js
const result = students.map((std) => std);
console.log(result);
```
출력 결과
```js
[
  Student { name: 'A', age: 29, enrolled: true, score: 45 },
  Student { name: 'B', age: 28, enrolled: false, score: 80 },
  Student { name: 'C', age: 30, enrolled: true, score: 90 },
  Student { name: 'D', age: 40, enrolled: false, score: 66 },
  Student { name: 'E', age: 18, enrolled: true, score: 88 }
]
```
student가 아니라 student가 가진 score를 리턴
```js
const result = students.map((std) => std.score);
console.log(result); // [45, 80, 90, 66, 88]
```
+) 만약 학생들이 가진 점수를 2배로 리턴하고 싶다면?
```js
const result = students.map((std) => std.score * 2);
console.log(result); // [90, 160, 180, 132, 176]
```

## 8. 50점 이하인 학생이 있는지 체크하기 (some)
`some`: 배열의 요소들 중 조건(콜백함수의 리턴이 true)을 만족하는게 있는지 확인<br>
`every`: 배열의 모든 요소가 조건(콜백함수의 리턴이 true)을 만족하는지 확인
### 내 답
```js
students.forEach((std)=>{
    if(std.score < 50)
    console.log(std.name);
});
```
### API 사용
```js
// 하나의 요소라도 score<50이면 true
const result1 = students.some((std) => std.score < 50); 
console.log(result1); // true

// 모든 요소가 score<50이면 true
const result2 = students.every((std) => std.score < 50); 
console.log(result2); // false
```

## 9. 학생들의 점수 평균 구하기 (reduce)
`reduce`: 배열에 있는 모든 요소들의 값을 누적할 때 사용
### 내 답
```js
let avg=0;
students.forEach((std)=>{
    avg+=std.score;
});
avg/=students.length;
console.log(avg); // 73.8
```
### API 사용
#### 우선 예제로 이해하기
```js
const result = students.reduce((prev, curr) => {
    console.log('=========');
    console.log(prev);
    console.log(curr);
    return curr;
});
```
출력 결과
```js
=========
Student { name: 'A', age: 29, enrolled: true, score: 45 }
Student { name: 'B', age: 28, enrolled: false, score: 80 }
=========
Student { name: 'B', age: 28, enrolled: false, score: 80 }
Student { name: 'C', age: 30, enrolled: true, score: 90 }
=========
Student { name: 'C', age: 30, enrolled: true, score: 90 }
Student { name: 'D', age: 40, enrolled: false, score: 66 }
=========
Student { name: 'D', age: 40, enrolled: false, score: 66 }
Student { name: 'E', age: 18, enrolled: true, score: 88 }
```
return하는 값(curr)이 다음 prev로 전달됨!<br>
#### 학생들의 점수를 누적하기
```js
const result = students.reduce((prev, curr) => {
    console.log('=========');
    console.log(prev);
    console.log(curr);
    return prev + curr.score;
}, 0); // 0부터 시작
```
출력 결과
```js
=========
0
Student { name: 'A', age: 29, enrolled: true, score: 45 }
=========
45
Student { name: 'B', age: 28, enrolled: false, score: 80 }
=========
125
Student { name: 'C', age: 30, enrolled: true, score: 90 }
=========
215
Student { name: 'D', age: 40, enrolled: false, score: 66 }
=========
281
Student { name: 'E', age: 18, enrolled: true, score: 88 }
```
💡 `prev`: 이전에 콜백함수에서 리턴된 값이 전달됨<br>
💡 `curr`: 배열의 item을 순차적으로 전달 받음<br>
#### 이제 문제를 풀어보자
```js
const sum = students.reduce((prev, curr) => prev + curr.score, 0); 
const result = sum / students.length;
console.log(result); // 73.8
```

## 10. 학생들의 점수를 문자열로 변환하기 (reduce)
### 내 답
```js
let str = '';
let flag=0;
students.forEach((std)=>{
    str+=std.score;
    flag++;
    if(flag<students.length)
        str+=',';
});
console.log(str);
```
### API 사용
student 배열을 점수 배열로 변환(map)한 뒤, 문자열로 변환(join)
```js
const result = students.map((std) => std.score).join();
console.log(result); // 45,80,90,66,88
```
+) 만약 점수가 50점 이상인 학생들만 문자열로 변환하고 싶다면?
```js
const result = students
.map((std) => std.score)
.filter((score) => score >= 50)
.join();
console.log(result); // 80,90,66,88
```

## 11. 학생들의 점수를 오름차순 정렬한 뒤 문자열로 변환 (sort)
### 내 답
```js
const sortStr = s => {
    return s.split(',').sort().join(','); 
}
console.log(sortStr(str));
```
### API 사용
```js
const result = students.map((std) => std.score)
.sort((a, b) => a - b) // 오름차순
// .sort((a, b) => a - b) // 내림차순
.join();
console.log(result);
```

***
<br>

    💛 개인 공부 기록용 블로그입니다. 👻

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}