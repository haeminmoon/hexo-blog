---
title: Iterator - (2)
date: 2019-02-06
categories: [ Javascript ]
tags: [ Javascript, ES6+, Iterator ]
---

Javascript의 Iterator 대해 정리한 글 입니다.

<!-- more -->

[Iterator - (1)](/2019/02/06/iterator-1/)에서는 Iterator와 ES6의 순회에 대해 알아보았으니, Iterator의 정확한 개념과 동작 방식에 대해 알아보고자 한다. 

## Iterator의 동작 방식
{% tabbed_codeblock example_1 %}
<!-- tab js -->
// Array
const arr = [1, 2, 3];
const iter = arr[Symbol.iterator](); // iter에 arr의 iterator를 담기.

console.log(iter.next()); // { value: 1, done: false }
console.log(iter.next()); // { value: 2, done: false }
console.log(iter.next()); // { value: 3, done: false }
console.log(iter.next()); // { value: undefined, done: true }
<!-- endtab -->
{% endtabbed_codeblock %}
example_1 예제 코드에서는 Iterator의 동작 방식을 보여주고 있다. next()가 평가되면 { value, done } 객체가 리턴되는 모습을 볼 수 있다.

여기서 Iterator의 한 가지 특징을 살펴보자면, Iterator는 next()가 평가되기 전까지는 다음 리턴 값을 반환하지 않는다는 특징을 가지고 있다.
{% tabbed_codeblock example_2 %}
<!-- tab js -->
// Array
const arr = [1, 2, 3];
const iter = arr[Symbol.iterator](); // iter에 arr의 iterator를 담기.

console.log(iter.next()); // { value: 1, done: false }
for (const i of iter) console.log(i) // 2 3
<!-- endtab -->
{% endtabbed_codeblock %}
> example_2 예제 코드와 같이 Iterator는 next() 메소드에 의해 value로 떨어지는 값만 평가하는 모습을 볼 수 있다.

## Iterable/Iterator protocol
- Iterable : Iterator를 리턴하는 {% hl_text danger %}
[Symbol.iterator]()
{% endhl_text %}를 가진 값
- Iterator : { value, done } 객체를 리턴하는 next() 메소드를 가진 값
- Iterable/Iterator protocol : Iterable을 for...of, 전개 연산자 등과 함께 동작하도록한 규약

{% tabbed_codeblock example_3 %}
<!-- tab js -->
// Array
const arr = [1, 2, 3];
for (const i of arr) console.log(i); // 1 2 3
<!-- endtab -->
{% endtabbed_codeblock %}

앞서 기술한 정의가 **example_1, example_2, example_3** 예제 코드에 어떻게 접목되어 동작하는지 설명해보자면, 다음과 같다.
> Array는 Iterable 이며, Iterator를 return 할 수 있다. 즉, Iterable/Iterator protocol에 따라 for...of 문법과 함께 순회 동작을 실행 할 수 있다.

## 사용자 정의 Iterable
{% tabbed_codeblock example_4 %}
<!-- tab js -->
const iterable = {
    [Symbol.iterator]() {
        let i = 0;
        return {
        next() {
            return i == 4 ? { done: true } : { value: i++, done: false };
        },
        [Symbol.iterator]() { return this; } 
        }
    }
};

let iterator = iterable[Symbol.iterator]();
console.log(iterator.next()); // { value: 0, done: false }
console.log(iterator.next()); // { value: 1, done: false }
for (const i of iterator) console.log(a); // 2 3
console.log(iterator.next()); // { value: undefined, done: true }
<!-- endtab -->
{% endtabbed_codeblock %}

**example_4**에서 사용자 정의 Iterable을 직접 구현해 봄으로써 Iterator와 Iterable에 대해 확실한 구분과 동작 원리에 대해 개념을 확립 할 수 있을 것이다.

## Iterator와 함수형 프로그래밍 그리고 ES6
Iterator에 대해 이렇게까지 세세하게 정리한 이유는 그만큼 중요한 개념이기 때문이다. 특히 Iterator는 자바스크립트에서 함수형 프로그래밍을 할 때, 아주 중요하다. 그 이유는 Iterable/Iterator protocol를 적극 활용하여 코드의 추상화와 다형성을 부여하여 보다 간결하고 예쁜 코드를 작성할 수 있기 때문이다. 뿐만 아니라 성능 측면에서도 '지연 평가(Lazy), 동시성 프로그래밍'을 가능하게끔 하기에 우수한 애플리케이션을 개발하기 위해서라도 아주 중요한 개념이라고 할 수 있다.