---
title:  "[JavaScript] 11. async와 await"

categories:
  - JavaScript
tags:
  - [JavaScript]

toc: true
toc_sticky: true
 
date: 2022-04-16
last_modified_at: 2022-04-16
---
들어가기 앞서...<br>
`async`와 `await`은 깔끔하게 프로미스를 사용할 수 있는 방법<br>
하지만 모든 프로미스를 `async`와 `await`으로 대체하라는 것은 아님!

# async
사용자의 데이터를 백엔드로부터 받아오는 함수가 있다.
## promise를 이용하는 방법 (review)
내가 언제 user의 데이터를 받아올 지 모르겠지만 약속할게.<br>
이 Promise라는 오브젝트를 가지고 있으면,<br>
여기에 네가 then이라는 콜백함수만 등록해놓으면
user의 데이터가 준비되는 대로 네가 등록한 콜백함수를 내가 불러줄게.
```js
function fetchUser(){
   return new Promise((resolve, reject) => {
        // do network request in 10 secs...
        resolve('ann');
   });
}

const user = fetchUser();
user.then(console.log);
```
## async를 이용하는 방법
함수 앞에 `async` 키워드를 붙이면 자동적으로 함수 안에 있는 코드블럭이 프로미스로 변환됨
```js
async function fetchUser(){
    // do network request in 10 secs...
    return 'ann';
}

const user = fetchUser();
user.then(console.log);
```

# await
```js
function delay(ms){
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple(){
    await delay(1000); // delay()가 끝날때까지 1초 기다렸다가 🍎 리턴
    return '🍎';
}

async function getBanana(){
    await delay(1000); // delay()가 끝날때까지 1초 기다렸다가 🍌 리턴
    return '🍌';
}

// 너무 중첩적인 프로미스 체이닝
function pickFruits(){
    return getApple().then(apple => {
        return getBanana().then(banana => `${apple} + ${banana}`);
    });
}

pickFruits().then(console.log);  // 🍎 + 🍌
```
위 예제에서 pickFruits()를 `async`를 이용해 바꿔보자
```js
async function pickFruits(){
    const apple = await getApple();
    const banana = await getBanana();
    return `${apple} + ${banana}`;
}

pickFruits().then(console.log);  // 🍎 + 🍌
```
`async`와 `await`을 이용해 비동기적인 코드를 마치 동기적인 코드처럼 작성할 수 있고, 리턴값도 자연스럽게 줄 수 있음

## await 병렬처리
pickFruits()에서 getApple()과 getBanana()는 서로 연관이 없으므로 병렬적으로(동시에) 처리할 수 있다.
```js
async function pickFruits(){
    // promise를 만드는 순간 promise 안에 있는 코드블럭이 실행됨
    const applePromise = getApple();
    const bananaPromise = getBanana();
    const apple = await applePromise;
    const banana = await bananaPromise;
    return `${apple} + ${banana}`;
}

pickFruits().then(console.log);  // 🍎 + 🍌
```

### 깔끔하게 병렬처리 하기 (using Promise APIs)
#### all
`all()`: 프로미스 배열을 전달하면, 모든 프로미스들을 병렬적으로 다 받을때까지 모아줌
```js
function delay(ms){
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple(){
    await delay(1000); // 1초
    return '🍎';
}

async function getBanana(){
    await delay(1000); // 1초
    return '🍌';
}

function pickAllFruits(){
    return Promise.all([getApple(), getBanana()])
    .then(fruits => fruits.join(' + ')); // 배열을 스트링으로 변환
}

pickAllFruits().then(console.log); // 🍎 + 🍌
```
#### race
만약 더 먼저 딸 수 있는 과일만 받아오고 싶다면?<br>
`race()`: 프로미스 배열을 전달하면, 배열에 전달된 프로미스들 중에 가장 먼저 값을 리턴하는 프로미스만 전달
```js
function delay(ms){
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple(){
    await delay(1000); // 1초
    return '🍎';
}

async function getBanana(){
    await delay(3000); // 3초
    return '🍌';
}

function pickOnlyOne(){
    return Promise.race([getApple(), getBanana()]);
}

pickOnlyOne().then(console.log); // 🍎 
```

# 🤪 Homework
이전에 만들었던 `callback-to-promise.js`의 consumer 부분을 `async`와 `await`을 이용해 깔끔하게 변경하기
## Producer
```js
class UserStorage{
    loginUser(id, password){
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                if((id === 'ann' && password === 'hello') || (id === 'coder' && password === 'academy')){
                    resolve(id);
                }else{
                    reject(new Error('not found'));
                }
            }, 2000);
        });
    }

    getRoles(user){
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                if(user === 'ann'){
                    resolve({name: 'ann', role: 'admin'});
                }else{
                    reject(new Error('no access'));
                }
            }, 1000);
        });
    }
}
```
## Consumer - 변경 전
```js
const userStorage = new UserStorage();
const id = prompt('Enter your id');
const password = prompt('Enter your password');

userStorage.loginUser(id, password)
.then(userStorage.getRoles)
.then(user => alert(`Hello ${user.name}, you have a ${user.role} role.`))
.catch(console.log);
```
## Consumer - 변경 후
```js
const userStorage = new UserStorage();
const id = prompt('Enter your id');
const password = prompt('Enter your password');

async function loginResult() {
    try {
       const loginUser = await userStorage.loginUser(id, password);
       const user = await userStorage.getRoles(loginUser);
       alert(`Hello ${user.name}, you have a ${user.role} role`);
    } catch(error) {
        console.log(error);
    }
 }
 
 loginResult();
```
# 📁 참고
[DreamCoding](https://www.youtube.com/watch?v=aoQSOZfz3vQ&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=13)

***
<br>

    💛 개인 공부 기록용 블로그입니다. 👻

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}