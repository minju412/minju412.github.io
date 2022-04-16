---
title:  "[JavaScript] 4. Class와 Object의 차이점"

categories:
  - JavaScript
tags:
  - [JavaScript]

toc: true
toc_sticky: true
 
date: 2022-04-13
last_modified_at: 2022-04-13
---
# Class와 Object 개념 정리
## Class: template
- template: 해당 클래스에는 어떠한 데이터가 들어갈 수 있는지 템플릿만 정의해놓음
- declare once: 한번만 선언
- no data in: 정의만 한 것으로 실제 메모리에 올라가지 않음

## Object: instance of a class
클래스에 실제 data를 집어넣은 것!
- instance of a class: 클래스를 이용해 생성한 오브젝트
- created many times: 클래스를 이용해 많이 생성할 수 있음
- data in: 실제 메모리에 올라감

# Class 선언과 Object 생성
```js
// class 선언
class Person{
  constructor(name, age){
    // fields
    this.name = name;
    this.age = age;
  }
  // method
  speak(){
    console.log(`${this.name}: hello!`);
  }
}

// object 생성
const ann = new Person('ann', 20);

console.log(ann.name);
console.log(ann.age);
ann.speak();
```

# Getter와 Setter
```js
class User{
  constructor(name, age){
    this.name = name;
    this.age = age;
  }
  get age(){
    return this._age;
  }
  set age(value){
    this._age = value > 0 ? value : 0; // value가 0보다 클 때에만 set age
  }
}

const user1 = new User('ann', -1); // 나이가 음수일 수 없으므로 setter가 0 대입
console.log(user1.age); // field에는 _age가 있지만 age로 호출 가능 (내부적으로 getter와 setter를 이용하기 때문)
```

# Fields (public, private)
너무 최근에 추가되어 아직까지 널리 사용되지는 않음
```js
class Experiment{
  publicField = 2;
  #privateField = 0; // #을 붙이게되면 private로 선언되어 외부에서 접근 불가능
}
const experiment = new Experiment();
cosole.log(experiment.publicField); // 2
cosole.log(experiment.privateField); // undefined
```

# Static
마찬가지로 최근에 추가되어 아직까지 널리 사용되지는 않음
```js
class Article{
  // 오브젝트에 상관없이 클래스가 가지고 있는 고유한 값을 static으로 선언!
  static publisher = 'Ann'; // static field

  constructor(articleNumber){
    this.articleNumber = articleNumber;
  }
  
  static printPublisher(){ // static method
    console.log(Article.publisher);
  }
}

const article1 = new Article(1);
const article2 = new Article(2);

// console.log(article1.publisher); // undefined
console.log(Article.publisher); // static 변수는 오브젝트(article1, article2)마다 할당되는 것이 아니라 Article이라는 클래스 자체에 할당된 것!

// article1.printPublisher();
Article.printPublisher(); // static method를 호출할 때에도 마찬가지로 오브젝트가 아닌 클래스로부터 호출
```
💡 오브젝트에 상관없이 (들어오는 데이터에 상관없이) 공통적으로 클래스에서 사용할 수 있는 변수 혹은 메서드라면 static을 이용해 선언하는 것이 메모리의 사용을 줄일 수 있음!

# 상속과 다형성
```js
class Shape{
  constructor(width, height, color){
    this.width = width;
    this.height = height;
    this.color = color;
  }
  draw(){
    console.log(`drawing ${this.color} color of`);
  }
  getArea(){
    return this.width * this.height;
  }
}

class Rectangle extends Shape {} 

// overriding - 함수 재정의
class Triangle extends Shape {
  draw(){
    super.draw(); // 부모의 draw 메서드 호출
    console.log('🔺'); // 자식에서 재정의
  }
  getArea(){
    return (this.width * this.height) / 2;
  }
}

new rec = new Rectangle(3,5,'yellow');
rec.draw();

new tri = new Triangle(4,4,'pink');
console.log(tri.getArea());
```

# instanceOf: Class checking
왼쪽에 있는 오브젝트가 오른쪽에 있는 클래스의 인스턴스인지 아닌지 확인
```js
console.log(rectangle instanceof Rectangle); // true
console.log(triangle instanceof Rectangle); // false
console.log(triangle instanceof Triangle); // true
console.log(triangle instanceof Shape); // true
console.log(triangle instanceof Object); // 🌟 true
```
자바스크립트에서 만드는 모든 오브젝트 클래스들은 자바스크립트에 있는 Object를 상속함!

# 자바스크립트 object들 (🌟 참고 URL)
> [MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)

자바스크립트 내부에 포함되어있는 오브젝트들은 어떤 것들이 있는지 확인 가능한 유용한 사이트!

# 📁 참고
[DreamCoding](https://www.youtube.com/watch?v=_DLhUBWsRtw&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=6)

***
<br>

    💛 개인 공부 기록용 블로그입니다. 👻

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}