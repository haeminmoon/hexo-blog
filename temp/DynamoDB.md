---
title: DynamoDB
date: 2019-02-01
categories: [ DynamoDB ]
tags: [ Paas, Saas, Amazone, AWS, DB, NoSQL, DynamoDB ]
---

AWS의 대표적인 Full-Managed NoSQL 서비스인 DynamoDB에 대해 정리한 글입니다.

<!-- more -->

온디맨드


Dynamo DB (On-Demand and Transaction)

DynamoDB는 규모에 관계없이 완전히 관리되는 비관계형 데이터베이스

- Fully managed, Performance at scale, Enterprise

Scale-Out  /  Logical DB

기능
> 용량 계산, 계획 하거나 예약할 필요가 없음.
> 사용만 만큼만 과금 (Read, Write)

용량
> 용량을 낭비하거나 부족함이 없음.
> 트래픽에 따라 즉각적으로 작업 부하를 자동으로 조정


On-Demand 요금은?
서울 리전은? 다른 방식보다는 비쌈.
프로비저닝이나 오토스케일링 방식에 비해 비쌈.

$1.35 쓰기 요청 100만개당
$0.27 읽기 요청 100만개당
$2.0 온디맨다 100만개당


* On-Demand 방식은 언제 사용하나?

- 프로비져닝
싸다. 라이브 운영은 이것으로

- 오토스케일
스케일업 하는 지연시간
지정한 사용율을 유지하지 못하면 스케일링 안됨
상한 하한을 정할 수는 있지만.

- 온디맨드
서비스는 해야겠는데, 사용량이 예측 불가일때


——————


트랜잭션이 중요한 이유? 

트랜잭션 API로 실생활의 트랜잭션을 쉽게 구현 할 수 있다.

> 동시다발적 쓰기(Write), 여러 아이템을 갱신(Update)
> 처리하기 전에 여러가지 조건을 검사
> 다양한 테이블간에 데이터의 일관성 유지


1번의 API호출로 여러가지는 할 수 있다. 통상적인 트랜잭션 기능 제공

> 데드락 X
> 긴 트랜잭션 시간 X
> 열린 트랜젝션 X
> 관리되지 않은 동시성 X
> DBA의 괴로움 X

*추가된 트랜잭션 API (10개까지 묶을 수 있음)
- TransactWriteItems
- TransactGetItems

이전에는 단일 아이템연산에만 ACID 지원, 다중 아이템연산에도 ACID지원

이제는 REST Ful 한 API 제공, InsertItem, GetItem, PutItem, DeleteItem



트랜젝션이 실패하는 경우?
>사전 조건 실패
>읽기/쓰기 용량부족 (트랜젝션은 온디맨드와 같이)
>트랜젝션 충돌


다른이유
>트랜잭션 진행중
>서비스 에러
>잘못 구성된 요청
>퍼미션


————————


트랜잭션 API 비용?
트랜잭션은 비트랜젝션에 비해 2배의 일을 한다.
트랜젝션은 작업 당 2배 단위로 읽기/쓰기 용량을 사용한다.

## RDBMS, NoSQL 비교

### RDBMS
데이터들 간에 일련의 관계를 설계 및 정의하여, 데이터베이스에 저장시 데이터들 간의 관계를 함께 저장합니다. 이를 활용하여 목적에 부합하는 여러 형태의 데이터를 출력할 수 있게 합니다. 즉, 관계형 데이터 베이스는 데이터의 활용 측면에 초점이 맞추어져 있습니다. 또한 데이터들간의 관계를 이용해서 데이터의 정형성, 무결성등을 유지하여 데이터베이스에 대한 신뢰성을 높이는 목적도 존재합니다.

- SQL 사용 가능
- - 비지니스 로직을 SQL로 대체함으로서 애플리케이션 내, 간결하고 심플한 코딩을 가능하게끔 합니다.
- 


https://velog.io/@drakejin/DynamoDB%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90-1

빙글 