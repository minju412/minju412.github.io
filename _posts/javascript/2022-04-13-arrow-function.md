---
title:  "[JavaScript] Arrow Function"

categories:
  - JavaScript
tags:
  - [JavaScript]

toc: true
toc_sticky: true
 
date: 2022-04-13
last_modified_at: 2022-04-13
---
# 💎 Function
## 💡 Parameters

premitive parameters: passed by value<br>
object parameters: passed by reference<br>

```js
function changeName(obj){
  obj.name = 'corder';
}
const Ann = { name: 'ann'};
changeName(Ann);
console.log(Ann);
```
object는 **reference**로 전달되기 때문에, 함수 안에서 object의 값을 변경하면 변경 사항이 그대로 메모리에 적용됨!<br>

## 💡 Default parameters (added in ES6)
```js
function showMessage(msg, from='unknown'){
  console.log(`${msg} by ${from}`);
}
showMessage('Hi'); // Hi by unknown 출력
```

## 💡 Rest parameters (added in ES6)
```js
function printAll(...args){
  for(let i=0; i<args.length; i++){
    console.log(args[i]);
  }

  // 더 간단하게 배열 출력하는 방법
  for(const arg of args){
    console.log(arg);
  }

  // 더더욱 간단하게 출력하는 방법
  args.forEach((arg) => console.log(arg));
}
printAll('red', 'orange', 'blue'); 
```
이때 `...args`는 printAll 함수를 호출할 때 전달한 red, orange, blue 세 개의 인자가 담긴 **배열**

## 💡 Local scope
밖에서는 안이 보이지 않고, **안에서만 밖을 볼 수 있다.**
```js
let global = 'msg';
function printMsg(){
  let local = 'hello';
  console.log(local);
  console.log(global); // 안에서 전역변수 접근 가능
}
printMsg();
// console.log(local); // 밖에서는 지역변수 접근 불가능
```

## 💡 Early return, early exit
### bad case
```js
function upgradeUser(user){
  if(user.point > 10){
    // long upgrade logic...
  }
}
```
block안에서 긴 로직을 작성하면 가독성이 떨어짐
### good case
```js
function upgradeUser(user){
  if(user.point <=> 10){
    return;
  }
  // long upgrade logic...
}
```
조건이 맞지 않을 때는 빨리 리턴을 해서 함수를 종료하고, 조건이 맞을 경우에만 필요란 로직들을 쭉 실행하는 것이 좋음!<br>

# 💎 Function Expression
## 💡 First-class function (복습)
function은 다른 변수와 마찬가지로
1. 변수에 할당 될 수 있고
2. 다른 함수의 파라미터로 전달될 수 있으며
3. 다른 함수의 리턴값으로도 사용 가능하다.
위의 특징들을 가능하게 가는 것이 바로 function expression!

## 💡 Function expression
```js
// 함수를 선언함과 동시에 print라는 변수에 할당
const print = function(){ // anonymous function
  console.log('print');
}; 
print();
const printAgain = print;
printAgain();
```
### Function expression과 Function declaration의 차이점?
Function expression은 할당된 이후부터 호출이 가능한 반면에, <br>
Function declaration은 함수가 선언되기 이전에 호출 가능하다. (hoisted)<br>
```js
// Function expression
// print(); // error 발생!!!
const print = function(){ 
  console.log('print');
}; 

// Function declaration
console.log(sum(1,3)); // 정상 출력
function sum(a,b){
  return a+b;
}
```

## 💡 Callback function using function expression
callback function은 상황에 맞는 함수를 호출할 수 있음
```js
function randomQuiz(answer, printCorrect, printWrong){
  if(answer === 'I love you'){
    printCorrect();
  } else{
    printWrong();
  }
}

// anonymous function
function printCorrect = function (){
  console.log('congratulations!');
}

// named function 
// 디버깅 할 때 stack traces에 함수의 이름이 나오게 하기 위해서 사용
// 혹은 함수 안에서 자기 자신을 호출하기 위한 recursion을 위해 사용
function printWrong = function print(){
  console.log('That is wrong answer.');
}

randomQuiz('wrong', printCorrect, printWrong); // That is wrong answer.
randomQuiz('I love you', printCorrect, printWrong); // congratulations!
```
answer이 'I love you'인 경우에는 printCorrect()라는 콜백 함수 호출 <br>
아닌 경우에는 printWrong()라는 콜백 함수 호출

## 💡 Arrow function
Arrow function을 사용해 함수를 간결하게 만들 수 있음<br>
Arrow function은 항상 anonymous function<br>
사용법: `변수명 = 파라미터 => 함수 body`
```js
// 기존 함수 호출법
const print = function () {
  console.log('Print!');
};

// Arrow function
const simplePrint = () => console.log('simplePrint');
const add = (a,b) => a+b;

// body가 한줄이 아니라면 block 사용 가능
// 대신 block을 사용하면 return 키워를 이용해 값을 리턴해주어야함!
const simpleMultiply = (a,b) => {
  // do something more
  return a*b;
}
```

## 💡 IIFE: Immediately Invoked Function Expression
함수를 선언함과 동시에 호출할 수 있음
```js
// 함수를 선언한 뒤에 호출
function hello() {
  console.log('hello');
}
hello();

// IIFE
(function hi() {
  console.log('hi');
})();
```

***
<br>

    💛 개인 공부 기록용 블로그입니다. 👻

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}