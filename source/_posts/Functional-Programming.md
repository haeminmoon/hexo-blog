---
title: Functional Programming
date: 2018-02-01
categories: [ Javascript ]
tags: [ Javascript, ES6+ ]
---

# Functional programming & ES6+

**"Functional Programming + Javascript = Functional javascript"**

함수형 자바스크립트를 위한 기초 지식 정리

## 평가
- 코드가 계산(Evaluation) 되어 값을 만드는 것

## 일급
- 값으로 다룰 수 있다.
- 변수에 담을 수 있다.
- 함수의 인자로 사용될 수 있다.
- 함수의 결과롤 사용될 수 있다.

## 일급 함수
- 함수를 값으로 다룰 수 있다.
- 조합성과 추상화의 도구로 활용할 수 있다.

자바스크립트에서 함수는 일급이다. 함수가 일급이라는 것은, 함수를 값으로 다룰 수 있다는 이야기다.
함수를 값으로 다룰 수 있다는 이야기는 함수를 다음과 같이 활용 할 수 있다는 것이다.
```
// 함수를 변수에 담을 수 있다.
const add3 = a => a + 3;
console.log(add3);       // a => a + 3
console.log(add3(1));    // 4

const f = () => () => 1;
console.log(f());        // () => 1

const f2 = f();
console.log(f2());       // 1
```
즉, 함수가 일급이라는 것은 함수의 결과값으로 함수를 활용 할 수 있음을 의미한다.

## 고차 함수
- 일급 함수의 성질을 활용하여 함수를 값으로 다루는 함수  

고차 함수는 크게 두 가지로 나뉘어 진다.  

**함수를 인자로 받아서 실행하는 함수.**
```
const execute = f => f(1);
const add3 = a => a + 3;

console.log(execute(add3));         // 4
console.log(execute(a => a - 1));   // 0

```

***위와 같은 프로그래밍 방식을 'Applicative programming' 이라고도 한다.***

**함수를 만들어 리턴하는 함수 (클로저를 만들어 리턴하는 함수)**
```
const addMaker = a => b => a + b;
const add10 = addMaker(10);

console.log(add10(5));      // 15
console.log(add10(10));     // 20
```
위 예제에서 addMaker가 함수를 만들어 리턴하는 함수 이다.  
이때 리턴되는 함수인 ***'b => a + b'*** 는 클로저 이다. ***'b => a + b'*** 가 만들어질 때의 환경인 a를 기억하고 있기 때문이다. 
