---
title: Title
date: 2019-02-01
categories: [ Javascript ]
tags: [ Javascript, ES6+ ]
---

...

<!-- more -->

Not yet.






Lambda, API Gateway기반 Websocket 앱 구현하기


API Gateway 기능 개요

인증 : IAM, Lambda/OAuth, Cognito
요청 조절 : API Key
페이로드 변환


WebSocket API 지원

기존에는 Rest기반의 API만 지원했으나, websocket이나옴.

즉, 실시간 양방향성 애플리케이션 구축 가능, 알람, 실시간 연결 채팅, 스트리밍 같은 것들을 할 수 있음.

————————
was://
————————


가격

처음 10억건 100만건당 $1.14
10억개 이상 $0.94
연결 시간(분) 연결시간 100만 분당 $0.285





------

Lambda

이벤트 기반 서버리스 컴퓨팅

람다의 핵심은 워커!
코드를 실행하는 것이 바로 워커이고, 이것이 성능을 결정한다. 워커가 샌드박스에서 실행 할 수 있게끔 도와줌


워커의 레이어
코드 > 람다런타임 > 샌드박스 > …. 


Firecaracker / 향후 람다 펑션의 모습 . 
람다레이어….

Firecaracker
높은 효율성, 고가용성과 스케일을 가능하게끔 한다.


---- https://github.com/nsriram/aws-lambda-layer-example

- 동작원리
Layer의 순서가 중요!
-/opt 디렉토리 아래에 순서대로 추출하여 덮어쓸 수 있음.
- 이런 방법으로 실행환경의 커스터마이즈 가능
- 첫 번째 레이어로 Custom Runtime, 두번째 레이어 부터 라이브러리

Limits : 동시 1000개
75GB / Region - 256MB / Function

/opt/node_modules

-각 함수당 다섯 개의 레이어 사용 가능
-레이어로 Custom Runtime 활용 가능
-함수 실행시, 처음 세팅한 순서대로 Layer 적재.
 -  중복요소를 덮어씀




sis package  - layer 기능 사용 가능  /   serverless-framework


Layer 단점 / 버그수정 및 테스트 , 함수 적용이 귀찮다.
모듈 다이어트를 도와줄 핵심 기능

관심사 분리 외부 패키지와 주 서비스로…

반복적으로 사용하는 함수, 프레임워크, 패키지 등…


외부 모듈들을 드디어 뺼 수 가 있다.



