---
title: Iterator - (1)
date: 2019-02-06
categories: [ Javascript ]
tags: [ Javascript, ES6+, Iterator ]
---

Javascript의 Iterator와 ES6+에서의 순회 기법에 대해 정리한 글 입니다.

<!-- more -->

## ES6에서의 순회
Iterator는 기본적으로 리스트를 순회하기 위한 객체이다. 즉, ES6부터 도입된 Iterator에 대해 알아보기 전에 ES6에서의 기본 순회 기법을 알아볼 필요가 있다고 느꼈다. 순회 기법이 어떻게 변화 되었는지를 살펴본 후, 심층적으로 Iterator에 대해 알아보고자 한다.

**ES5에서의 순회**
{% tabbed_codeblock example_1 %}
<!-- tab js -->
// Array - 배열
var arr = [1, 2, 3];
for (var i = 0; i < arr.length; i++) {
    console.log(arr[i]); // 1 2 3
}

// Array like type - 유사배열
var str = 'abc';
for (var i = 0; i < str.length; i++) {
    console.log(str[i]); // a b c
}
<!-- endtab -->
{% endtabbed_codeblock %}  
> 숫자키와 배열의 인덱스를 기반으로 순회  

**ES6에서의 순회**
{% tabbed_codeblock example_2 %}
<!-- tab js -->
// Array - 배열
const list = [1, 2, 3];
for (const i of list) {
    console.log(i); // 1 2 3
}

// Array like type - 유사배열
const str = 'abc';
for (const i of str) {
    console.log(i); // a b c
}
<!-- endtab -->
{% endtabbed_codeblock %}  
> for...of 문법을 통해 순회

**example_1**과 **example_2**에는 ES6이전과 ES6이후의 순회 기법에 대한 예제이다.

**example_1**에서는 숫자키와 배열의 인덱스를 기반으로 순회를 하였으며, **example_2** 에서는 for...of 문법을 통해 순회하는 것을 확인 할 수 있다.

단순한 시각에서 바라본다면 **'문법을 통해 간결해진 순회문.'** 정도로 생각 할 수 있겠으나, 이는 ES6가 개발자에게 '강력한 편의 기능을 제공하고 있으며 내재된 추상화를 통해 얼마나 예쁜 코드를 작성할 수 있는지'를 내포하고 있음을 알아야 한다.

## ES6의 순회와 Iterator
ES6부터는 Array 자료형 뿐만 아니라 Map, Set같은 자료형도 for...of 문을 통해 순회가 가능하다.

**ES6에서의 Array, Set, Map의 순회**
{% tabbed_codeblock example_3 %}
<!-- tab js -->
// Array
const arr = [1, 2, 3];
for (const i of list) console.log(i); // 1 2 3

// Set
const set = new Set([1, 2, 3]);
for (const i of list) console.log(i); // 1 2 3

// Map
const map = new Map(['a', 1], ['b', 2], ['c', 3]);
for (const i of list) console.log(i); // ['a', 1], ['b', 2], ['c', 3]
<!-- endtab -->
{% endtabbed_codeblock %}

**example_3**에서 처럼 for...of 문법만으로 각각 다른 자료형을 순회할 수 있는 이유는 바로 Iteraotr 덕분이다.

기본적으로 'Array, Set, Map' 자료형에는 'Symbol.iterator'가 포함되어 있는데, 이 객체의 규약을 통해 위와 같이 순회가 가능한 것이다.

만약 아래 예제와 같이 'Symbol.iterator'에 null을 대입하면 for...of문으로 순회 할 수 없다.
{% tabbed_codeblock example_4 %}
<!-- tab js -->
// Array
const arr = [1, 2, 3];
arr[Symbol.iterator] = null;
for (const i of list) console.log(i); // Uncaugth Type Error: arr is not iterable.
<!-- endtab -->
{% endtabbed_codeblock %}  

**example_4**의 예제는 'iterator - 자료형 - for...of'가 서로 연관성이 있음을 말해주고 있는데, 이 연관성이 바로 Iterable protocol에 의해 동작한다는 것이다. (연관성에 대한 자세한 내용은 다음 장에서 확인.)

Iterator에 대한 이해를 돕기 위해 ES6에서의 순회 기법에 대해 확인하였으니, 본격적으로 Iterator에 대해 알아보고자 한다. [Iterator - (2)](/2019/02/06/Iterator-2/)