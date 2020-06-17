---
layout: post
title: "웹 디자인 패턴"
date: 2020-06-17
excerpt: MVC패턴 | MVVM패턴 비교
tags: [Web,Design,Pattern]
comments: true
---

## 용어 정리
* model : 데이터 처리부
* Controller : 사용자의 입력(Requst)를 받고 model에게 전달
* View : 사용자에게 보여지는 부분(UI)

## MVC패턴 
 - Model + View + Controller
 - 동작 순서
    1. 사용자의 요청을 Controller가 받아 Model에게 데이터를 준다.
    2. Model은 해당 데이터를 요청사항에 맞게 처리한다.
    3. View는 Model의 처리값을 사용자에게 보여준다.
 - 특징 : View 와 Model 사이의 의존성이 높아 대규모 시스템의 경우 로직이 복잡해지고 유지보수가 어렵다.
 
## MVVM패턴
 - Model + View + View Model
 - 동작 순서
    1. 사용자의 요청을 View가 받아 ViewModel에게 데이터를 준다.
    2. ViewModel은 Model에게 데이터 처리를 요청한다.
    3. Model은 데이터 처리 후 ViewModel에게 전달한다.
    4. View는 ViewModel과 Binding하여 사용자에게 보여준다.
 - 특징 : View 와 Model 사이의 의존성이 없어 각 부분을 모듈화하여 독립적으로 개발할 수 있다.

* MVP패턴 
  - Controller => Presenter(View와Model을 1:1로 연결해주는 역할을 한다)
  - view 와 model의 직접적인 연결이 없지만 View 와 Presenter의 의존성이 높아져 MVC패턴과 같은 문제가 발생한다.
  
 
 
