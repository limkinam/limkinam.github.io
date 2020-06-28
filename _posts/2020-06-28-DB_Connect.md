---
layout: post
title: "JDBC vs Mybatis vs JPA/Hibernate"
date: 2020-06-11
excerpt: "JDBC, JPA/Hibernate, Mybatis에 대해서 알아보고 비교해보자"
tags: [mybatis,jpa,hibernate,jdbc]
comments: true
---

## JDBC
 - 자바 언어로 다양한 RDB에 접속하여 SQL문을 수행하기 위한 인터페이스 API(인터페이스/드라이버)
 - 인터페이스 : java.sql 패키지
 - 드라이버 : java.sql 패키지를 상속하여 메소드의 몸체를 구현한 클래스 파일
 - Persistence Framework는 내부적으로 JDBC API를 사용  

## Persitence Framework
 - 데이터의 처리를 다루는 클래스 및 설정 파일의 집합
 - JDBC프로그래밍의 복잡함이나 번거로움 없이 간단한 작업만으로 DB연동 가능
 - SQL문으로 직접 DB데이터를 다루는 'SQL mapper':mybatic 와 자바 객체를 통해 간접적으로 DB데이터를 다루는 ORM(객체 관계 맵퍼)인 하이버네이트

* SQL Mapper : 객체와 SQL문을 매핑하여 데이터를 객체화하는 기술
* ORM : 객체와 RDBMS를 매핑하여 DB테이블을 객체지향적으로 사용하기 위한 기술

### Mybatis
 - 기존 JDBC의 코드 및 설정을 SQL Mapper로 처리하여 빠른 개발과 편리한 테스트 환경을 제공
 - 매핑을 위해 xml과 Annotation을 사용가능
 - 장 : 컨트롤에 적합하고 쿼리가 최적화 있을때 유용하다.
 - 단 : Application과 DB간의 모든 조작을 원할때 비적합(서로 잘 구조화되도록 많은 설정을 바꿔야 할 필요가 생긴다.)

### JPA(Java Persistent API)
 - 자바 ORM 기술에 대한 API 표준 명세
 - 구성요소 : 
    1.javax.persistance 패키지(API)
    2.JPAL(Java Persistence Query Language
    3.객체/관계 메타데이터
 - ORM Framework의 종류 : Hibernate, EclipceLink, OpenJPA 등
   
### Hibernate
 - HQL(Hibernate Query Language)를 사용
    - HQL은 완전히 객체 지향적(상속, 다형성, 관계)
    - HQL은 여러 테이블을 작업할 때 명시적인 join을 요구x
    - HQL은 쿼리 결과로 객체를 반환
 - 장 : 객체지향 개발 가능 / 테이블 생성, 변경, 관리가 쉬움 
 - 단 : 내부적으로 감싸져 있기 때문에 추상적

