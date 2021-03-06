---
title:  "[JavaScript] 3. Arrow Function"

categories:
  - JavaScript
tags:
  - [JavaScript]

toc: true
toc_sticky: true
 
date: 2022-04-13
last_modified_at: 2022-04-13
---
# π Function
## π‘ Parameters

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
objectλ **reference**λ‘ μ λ¬λκΈ° λλ¬Έμ, ν¨μ μμμ objectμ κ°μ λ³κ²½νλ©΄ λ³κ²½ μ¬ν­μ΄ κ·Έλλ‘ λ©λͺ¨λ¦¬μ μ μ©λ¨!<br>

## π‘ Default parameters (added in ES6)
```js
function showMessage(msg, from='unknown'){
  console.log(`${msg} by ${from}`);
}
showMessage('Hi'); // Hi by unknown μΆλ ₯
```

## π‘ Rest parameters (added in ES6)
```js
function printAll(...args){
  for(let i=0; i<args.length; i++){
    console.log(args[i]);
  }

  // λ κ°λ¨νκ² λ°°μ΄ μΆλ ₯νλ λ°©λ²
  for(const arg of args){
    console.log(arg);
  }

  // λλμ± κ°λ¨νκ² μΆλ ₯νλ λ°©λ²
  args.forEach((arg) => console.log(arg));
}
printAll('red', 'orange', 'blue'); 
```
μ΄λ `...args`λ printAll ν¨μλ₯Ό νΈμΆν  λ μ λ¬ν red, orange, blue μΈ κ°μ μΈμκ° λ΄κΈ΄ **λ°°μ΄**

## π‘ Local scope
λ°μμλ μμ΄ λ³΄μ΄μ§ μκ³ , **μμμλ§ λ°μ λ³Ό μ μλ€.**
```js
let global = 'msg';
function printMsg(){
  let local = 'hello';
  console.log(local);
  console.log(global); // μμμ μ μ­λ³μ μ κ·Ό κ°λ₯
}
printMsg();
// console.log(local); // λ°μμλ μ§μ­λ³μ μ κ·Ό λΆκ°λ₯
```

## π‘ Early return, early exit
### bad case
```js
function upgradeUser(user){
  if(user.point > 10){
    // long upgrade logic...
  }
}
```
blockμμμ κΈ΄ λ‘μ§μ μμ±νλ©΄ κ°λμ±μ΄ λ¨μ΄μ§
### good case
```js
function upgradeUser(user){
  if(user.point <=> 10){
    return;
  }
  // long upgrade logic...
}
```
μ‘°κ±΄μ΄ λ§μ§ μμ λλ λΉ¨λ¦¬ λ¦¬ν΄μ ν΄μ ν¨μλ₯Ό μ’λ£νκ³ , μ‘°κ±΄μ΄ λ§μ κ²½μ°μλ§ νμλ λ‘μ§λ€μ μ­ μ€ννλ κ²μ΄ μ’μ!<br>

# π Function Expression
## π‘ First-class function (λ³΅μ΅)
functionμ λ€λ₯Έ λ³μμ λ§μ°¬κ°μ§λ‘
1. λ³μμ ν λΉ λ  μ μκ³ 
2. λ€λ₯Έ ν¨μμ νλΌλ―Έν°λ‘ μ λ¬λ  μ μμΌλ©°
3. λ€λ₯Έ ν¨μμ λ¦¬ν΄κ°μΌλ‘λ μ¬μ© κ°λ₯νλ€.
μμ νΉμ§λ€μ κ°λ₯νκ² κ°λ κ²μ΄ λ°λ‘ function expression!

## π‘ Function expression
```js
// ν¨μλ₯Ό μ μΈν¨κ³Ό λμμ printλΌλ λ³μμ ν λΉ
const print = function(){ // anonymous function
  console.log('print');
}; 
print();
const printAgain = print;
printAgain();
```
### Function expressionκ³Ό Function declarationμ μ°¨μ΄μ ?
Function expressionμ ν λΉλ μ΄νλΆν° νΈμΆμ΄ κ°λ₯ν λ°λ©΄μ, <br>
Function declarationμ ν¨μκ° μ μΈλκΈ° μ΄μ μ νΈμΆ κ°λ₯νλ€. (hoisted)<br>
```js
// Function expression
// print(); // error λ°μ!!!
const print = function(){ 
  console.log('print');
}; 

// Function declaration
console.log(sum(1,3)); // μ μ μΆλ ₯
function sum(a,b){
  return a+b;
}
```

## π‘ Callback function using function expression
callback functionμ μν©μ λ§λ ν¨μλ₯Ό νΈμΆν  μ μμ
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
// λλ²κΉ ν  λ stack tracesμ ν¨μμ μ΄λ¦μ΄ λμ€κ² νκΈ° μν΄μ μ¬μ©
// νΉμ ν¨μ μμμ μκΈ° μμ μ νΈμΆνκΈ° μν recursionμ μν΄ μ¬μ©
function printWrong = function print(){
  console.log('That is wrong answer.');
}

randomQuiz('wrong', printCorrect, printWrong); // That is wrong answer.
randomQuiz('I love you', printCorrect, printWrong); // congratulations!
```
answerμ΄ 'I love you'μΈ κ²½μ°μλ printCorrect()λΌλ μ½λ°± ν¨μ νΈμΆ <br>
μλ κ²½μ°μλ printWrong()λΌλ μ½λ°± ν¨μ νΈμΆ

## π‘ Arrow function
Arrow functionμ μ¬μ©ν΄ ν¨μλ₯Ό κ°κ²°νκ² λ§λ€ μ μμ<br>
Arrow functionμ ν­μ anonymous function<br>
μ¬μ©λ²: `λ³μλͺ = νλΌλ―Έν° => ν¨μ body`
```js
// κΈ°μ‘΄ ν¨μ νΈμΆλ²
const print = function () {
  console.log('Print!');
};

// Arrow function
const simplePrint = () => console.log('simplePrint');
const add = (a,b) => a+b;

// bodyκ° νμ€μ΄ μλλΌλ©΄ block μ¬μ© κ°λ₯
// λμ  blockμ μ¬μ©νλ©΄ return ν€μλ₯Ό μ΄μ©ν΄ κ°μ λ¦¬ν΄ν΄μ£Όμ΄μΌν¨!
const simpleMultiply = (a,b) => {
  // do something more
  return a*b;
}
```

## π‘ IIFE: Immediately Invoked Function Expression
ν¨μλ₯Ό μ μΈν¨κ³Ό λμμ νΈμΆν  μ μμ
```js
// ν¨μλ₯Ό μ μΈν λ€μ νΈμΆ
function hello() {
  console.log('hello');
}
hello();

// IIFE
(function hi() {
  console.log('hi');
})();
```

# π μ°Έκ³ 
[DreamCoding](https://www.youtube.com/watch?v=e_lU39U-5bQ&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=5)


***
<br>

    π κ°μΈ κ³΅λΆ κΈ°λ‘μ© λΈλ‘κ·Έμλλ€. π»

[λ§¨ μλ‘ μ΄λνκΈ°](#){: .btn .btn--primary }{: .align-right}