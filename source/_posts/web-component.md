---
title: Web Component
date: 2020-02-08
categories: [ Web ]
tags: [ Web, Web tech, WC, Web Component ]
---

웹 컴포넌트(Web Component) 기술이 무엇인지에 대해 정리한 글 입니다.

<!-- more -->

## 웹 컴포넌트란?

W3C에서는 HTML의 한계 및 이슈들을 개선하고자 "웹 컴포넌트(Web Component)"라는 표준 및 명세를 만들었다. 즉, 표준을 기준으로 개발자가 자체적으로 "HTML Element"를 만드는 기술이다.

#### HTML의 한계 : 
- HTML Element는 아무리 같은 요소라도 다각화된 여러 브라우저와 운영체제에 따라 각각 다르게 동작할 수 있다. 특정 표준이 완벽하게 지원되는 상태가 아니다. 이는 개발에 대한 생산성과 유지보수 측면에 있어 비효율 적이다.

- HTML5 이외에도 여러 기능을 지원하는 엘리먼트들이 필요하다. 이를 해결하기 위해 JS Component를 사용하기도 하지만, 적용적인 측면에 있어 일정 수준의 러닝커브가 필요하며 성능적인 이슈가 동봉된다.

## 웹 컴포넌트는 왜 이제서야 화두가 되고 있는가?

- 사실 웹 컴포넌트 기술은, 이미 오래 전부터 시작된 기술이었고 우리가 인지하기 훨씬 이전부터 표준이 정의되어 있었다. 하지만 계속해서 주목을 받지 못하다가 'Google - Polymer'에 의해 다시 수면 위로 떠오르고 있는 실정이다.

> "전시와 비슷한 현재의 자바스크립트 세상 -> 프레임워크 전쟁"

한 때는 jQuery 하나로 모든일을 해결 할 때도 존재했다. 

당시 자바스크립트는 정적인 페이지 내에서의 제한된 역할을 맡았고, 복잡도는 페이지를 새로 로드 하는 것외에는 크게 올라가지 않았다. 그러나 AJAX의 도입으로 자바스크립트의 역할이 늘어남과 함께 코드의 복잡도는 올라갔고, 또한 SPA 방식의 FE 개발에 대한 득세는 코드를 한없이 복잡하게 만들었다. 이를 해결하기 위한 다양한 프레임워크들의 등장은 너무나도 당연할 수 밖에 없었다.

명백한 이유로 인해 당연하지만서도...

요즘 채감하는 것은  '너무나도 다양한 프레임워크의 등장이라기 보다' 는 거의 폭탄처럼 쏟아져 나오고 있는 실정인듯 하다. ( "AngularJS, React, VueJS, Bootstrap, ExtJS..."  )

"웹 개발을 좋아하고 심도있게 고민하는 개발자"라면 누구나 한 번쯤은 고뇌해 봤을법 하다. 

- 앞으로의 웹 트렌드는?
- 어떤 프레임워크를 공부해야 내 몸값이 높아질까?
- 어떤 스택으로 웹 개발을 하는게 최강의 웹 개발일까?

이러한 고민들이 웹 개발자들 사이에서 팽배해질 쯤, 

"Google I/O 2016"에서는 "#UseThePlatform"이란 키워드로 웹 표준에 대한 중요성을 다시 한 번 자각시켜주는 계기를 마련하게 되었다.

```
- 프레임워크들은 다양한 문제를 해결할 강력한 도구이지만?
  > 무거운 덩치는 앱을 무겁게 만든다.
  > 리소스를 사용자에게 전가 시킨다.
  > 프레임워크 종속적인 코드를 생산한다.
  > 높은 러닝커브를 요구한다.

- 이러한 문제점들을 해결하려면?
  > 프레임워크 대신 브라우저 기능을 사용하여 해결하자.
  > 프레임워크를 경량화 시켜, 더 적은 자바스크립트 코드를 사용하자.
```

"프레임워크에 의존하지 말고 원하는 요구 기능을 표준으로 정하고 표준대로 코딩하자." 
> 표준 코드로 작성한 기능은 성능 좋고 호환성이 좋은 웹 앱을 개발 할 수 있다!

## 웹 컴포넌트의 구성 : 
- "Templates, Shadow DOM, HTML Imports, Custom Element" 으로 구성되어 있다.

![Web-Components](https://poiemaweb.com/img/web-component.png)


#### 1. Custom Element

**[ 정의 ]**
  - HTML Element를 개발작 직접 정의하여 사용할 수 있도록 제공되는 기능이다.

**[ Custom Element 알아보기 ]**
{% tabbed_codeblock example_1 %}
<!-- tab html -->
    <!-- Used custom element -->
    <!DOCTYPE html>
    <html>
        <head>
            <script src="../src/baseComponents.js"></script>
        </head>
        <body>
            <!-- Custom Element의 이름 작성시 '-'를 포함해야 한다. [ 예약어는 X ] -->
            <spin-nav>
                <!-- Fallback value -->
                - 관리하기
                - 등록하기
                - 마이페이지
            </spin-nav>
        </body>
    </html>


    <!-- Unused custom element -->
    <!DOCTYPE html>
    <html>
        <head>
            <script src="../src/baseComponents.js"></script>
        </head>
        <body>
            <div class="spin-nav">
                <!-- Fallback value -->
                - 관리하기
                - 등록하기
                - 마이페이지
            </div>
        </body>
    </html>
<!-- endtab -->
{% endtabbed_codeblock %}

**[ Custom Element 만들기 ]**
{% tabbed_codeblock example_2 %}
<!-- tab js -->
    // HTMLElement를 항상 상속받아야 한다.
    class SpinNav extends HTMLElement {
        constructor() {
            super();
            console.log('Example~~~');
        }
    }
    window.customElements.define('spin-nav', SpinNav);
    // 이렇게 선언을 해주면 HTML 태그에서 "<spin-nav></spin-nav>" 이렇게 사용할 수 있음 :)
<!-- endtab -->
{% endtabbed_codeblock %}

**[ 상세 설명 ]**
  - 'div' 대신 'spin-nav'처럼 적절한 이름의 태그를 사용할 수 있다.
  - HTML Element와 Javascript Class를 한 몸으로 만들어 준다.
  - IE11 이상만 지원, Polyfill 필요할 수도 있다.
  - HTMLElement를 항상 상속받아야 한다.
  - Custom Element의 이름 작성시 "-" 를 포함해야 한다. [ 예약어는 X ]

#### 2. Shadow DOM

**[ 정의 ]**
- HTML과 CSS의 스코프를 독립적으로 다룰 수 있게끔 지원하는 개념 및 기능

우리가 작성하고 있는 'HTML, CSS, Javascript'는 어떻게 작성하던 결국 모두 하나의 페이지에 작성되고 동작한다. 이는 결국 글로벌하게 모든 코드들을 관리한다는 이야기가 된다. 예를들어 'document.querySelector()' 하나면 모든 엘리먼트와 돔에 접근 할 수 있는 이유도 모두 한 페이지에 작성되기 때문이다.

Global, Public.. 이러한 점들을 해결하기 위해 우리는 여러 프레임워크와 툴을 사용하고 있으며, SASS와 LESS 같은 도구들을 사용하는 것도 같은 이유일 것이다. 하지만 문제점을 해결하기 위해 **"새로운 의존성을 유입할 뿐, 근본적인 문제의 해결 방법"**은 아니다.

**[ 스코프를 독립적으로 관리할 수 있는 기술? ]**

'iframe'을 사용하면 되는거 아니야? 라는 생각을 할 수 있지만, 'iframe을 사용했을 때'는
> http 요청이 한차례 더 일어난다.
> 별도의 페이지이기 때문에, 소비되는 리소스도 높고 느리다.
> iframe의 주소가 같은 도메인이 아닌 경우 접근 불가능하다.

위와 같은 문제들이 존재한다. 해서 'iframe'형식으로 지원하던 기능을 브라우저에서도 'Shadow DOM'으로 변경하고 있는 추세이다. [ slot 기능을 활용 ]

**[ Shadow DOM 정의하기 ]**

{% tabbed_codeblock example_3 %}
<!-- tab HTML -->
    <div id="spin-nav">
        <!-- Light DOM -->
        <span slot="nav1">캠페인 관리</span>
        <span slot="nav2">마이 페이지</span>
    </div>

    // Shadow DOM
    document.querySelector('#spin-nav').attachShadow({ mode: 'open' })
    .innerHTML = `
        <p>
            <slot name="nav1"></slot>
        </p>
        <p>
            <slot name="nav2"></slot>
        </p>
    `;
<!-- endtab -->
{% endtabbed_codeblock %}

- Shadow DOM: 위 코드에서 p들, Shadow Root에 붙어있는 DOM
- Shadow Root: #shadow-root
- Shadow Host: Shadow Root의 부모. 위 코드에서 div#spin-nav
- Light DOM: Documnet의 Shadow Host에 붙어있는 Node들. span

>
**[ Web Component를 활용한 Shadow DOM 활용 - OOP <Shadow DOM + Custom Element>]**
>
![Web-Components](https://miro.medium.com/max/1026/0*7jwsF1nzzwm572Ib.png)
>
{% tabbed_codeblock example_4 %}
<!-- tab HTML -->
    <!-- GOOD : Custom Element는 기본적으로 Shadow DOM으로 생성된다. -->
    <spin-element></spin-element>

    <!-- BAD -->
    document.querySelector('spin-element')
        .shadowRoot
        .querySelector('div')
        .innerText = 'TEST'
<!-- endtab -->
{% endtabbed_codeblock %}
>
{% tabbed_codeblock example_5 %}
<!-- tab js -->
    // GOOD
    const spinElement = document.querySelector('spin-element');
    spinElement.execute();

    // BAD
    const execute = document.querySelector('spin-element')
        .shadowRoot
        .querySelector('div')
        .innerText;

    alert(execute);
<!-- endtab -->
{% endtabbed_codeblock %}


**[ 상세 설명 ]**
- textarea, input, image와 같은 엘리먼트들은 쉐도우 돔을 가질 수 없다.
- 쉐도우 돔은 여러번 중첩될 수 있다.
- 쉐도우 호스트의 스타일은 :host로 변경한다.
- 쉐도우 호스트의 클래스에 따른 스타일은 :host-context(.classname)으로 가능하다.
- attachShadow({mode: 'closed'})로 쉐도우 루트를 생성하면, 쉐도우 돔에 접근이 불가능하다.
- 쉐도우 돔 내부에서 발생한 이벤트의 target은 외부에서 쉐도우 호스트로 변경된다.

#### 3. Template Element

**[ 정의 ]**
- Element들을 재사용하고 모듈화 시키기 위해 사용하는 개념 및 기술

**[ Old fashion template ]**
{% tabbed_codeblock example_6 %}
<!-- tab js -->
    const spinNav = document.createElement('div');
    const nav1 = document.createElement('p');

    document.body.appendChild(spinNav);
    spinNav.appendChild(nav1);

    // 편하고 직관적이기는 하지만, 코드의 양이 너무 많아지고 복잡해진다. 유지보수는 최악..
    // innerHTML = `` 을 쓰면 보다 편할 수는 있겠지만, 반복문 같은 효율적인 코드 작성은 쉽지 않다.
<!-- endtab -->
{% endtabbed_codeblock %}

**[ 다른 대안들은? ]**

1. Template Engine
    - 템플릿 엔진들은 유용하지만 문자열로 처리되기에 어쩔 수 없는 문제점들을 내포한다. XSS 공격에 노출될 위험이 있으며, innerHTML의 사용이 강제된다. 또한 DOM API들을 템플릿에 사용할 수 없다는 약점이 존재한다.
>
2. Virtual DOM
    - Virtual DOM은 주어진 상태에 따라 DOM의 일부분만 업데이트 해주는 역할을 한다. 템플릿 관점에서 보자면, 상태에 따라 템플릿을 컴포넌트 단위로 업데이트 해주는 일을 한다고 할 수 있다. 다만 특정 프레임워크에 국한된다는 사실과 러닝커브는 피해갈 수 없다는 것이 현실이다.

**[ Template Element ]**

{% tabbed_codeblock example_7 %}
<!-- tab html -->
    <!-- 위에서 언급한 문제점들을 보완하고자 'Template Element'가 표준으로 정의되었다.  -->
    <template id="spin-nav">
        <p>nav1</p>
        <p>nav2</p>
    </template>
<!-- endtab -->
{% endtabbed_codeblock %}

**[ 상세 설명 ]**

- Template Element는 자바스크립트 코드로 많은 양의 코드를 적지 않아도 되고 조건에 따라 DOM의 변경도 가능하다. 이러한 변경은 DOM API들을 그대로 사용할 수 있어 편리하며, DOM에 한 번 정의되면 필요할 때마다 복사하여 붙여넣기가 가능하기 때문에 성능 또한 훌륭하다.  
>
- Template Element는 스크립트와 스타일도 포함할 수 있다. 스크립트와 스타일은 템플릿에 있을때는 적용되지 않지만, 복사되어 Document에 붙을때 적용된다. 이는 Shadow DOM을 기반으로 하여금 시너지를 일으켜 웹 컴포넌트의 템플릿 기능을 수행하는데 충분한 장점으로 작용한다.  
>
- Template Element는 템플릿이 HTML로 작성되어야 한다는 것이 오히려 약점이 될 수 있다. 컴포넌트의 컨트롤러에 해당하는 자바스크립트와 템플릿 뷰에 해당하는 HTML이 분리되어야 한다는 점이다. 컴포넌트와 모듈이 정확히 동의어라고 할 수는 없지만, 모듈로서 분리되어야만 재사용의 의미가 있는 것이다. 즉,  Template Element는 컴포넌트로 구성하려면 HTML, JS 두 개의 파일이 필요하게 되며 이 방식은 웹 컴포넌트를 모듈로 만들기에 큰 걸림돌이다.  

>
#### 4. HTML Import

**[ 정의 ]**
-  HTML 기반의 의존성을 해결해주는 기능

{% tabbed_codeblock example_8 %}
<!-- tab html -->
    <!-- main page -->
    <head>
        <link rel="import" href="spin-sub.html">
    </head>

    <!-- spin-sub.html -->
    <div>abcd</div>
<!-- endtab -->
{% endtabbed_codeblock %}
>
**[ 상세 설명 ]**
- HTML Imports의 문법은 스타일을 연결하는 것과 유사하지만 스크립트, 스타일, HTML 엘리먼트들의 의존성을 한 번에 해결해 주는 강력한 방법이다.
- Firefox가 HTML Imports를 지원하지 않는다는 사실을 필두로, 타브라우저 들도 서서히 지원을 하지 않기 시작함.
>
## So.. What?
>
사실 웹 컴포넌트 기술은 아직까지 100% 성숙하다고 할 수는 없다. 심지어, 'Template Element와 HTML Imports 기능'들의 경우에는 몇 가지 약점과 대내외 적인 이유로 인해 현재는 힘을 잃은 웹 컴포넌트의 기술들이 되었다. 정의되었던 표준들이 없어졌다고 판단할 수도 있겠지만, 이는 명확하게 약점을 보완하고 장점들만을 살리고자 하는 웹 컴포넌트의 진영에서의 긍정적인 액션이라고 판단된다.
>
'기술 표준'이라는 패러다임 속에서 파생되는 이점들은 너무나도 강력하기 때문에, 현재는 이를 강요하고 부각시키기 위해 'Template literal' 같은 ES6의 공식 문법이 지원되고 있으며, 이를 기반으로한 Google Polymer의 'lit-html'과 같은 웹 컴포넌트 기반 초경량 라이브러리가 등장하기도 하였다.
>
계속해서 긍정적인 방향성으로 웹 컴포넌트 기술이 발전한다면 파편화 되어있는 웹 기술 진영에서 고생하고 있는 개발자들이 조금이라도 덜 고생할 수 있는(?) 세상이 올 수 있지 않을...까...?
