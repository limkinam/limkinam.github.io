---
layout: post
title: "Spring Security"
date: 2020-07-03
excerpt: "Spring Security 이용 로그인 구현하기"
tags: [JWT,Spring Security]
comments: true
---

## 1.Spring Sceurity의 Authorities 와 Role
 - 사용자들에게 부여한 권한
 - Authorities : 기능 단위의 Permission을 의미
 - Role : Authorities를 포함하는 포괄적인 permission을 가지며, 반드시 prefix에 "ROLE_"를 명시하는 규칙  
 
 
## 2.HTTP Basic Authentication
 - 특정 resource에 대한 접근을 요청할때 브라우저가 사용자에게 username과 password를 확인해 인가를 제한하는 방법
 - 과정
    1. 클라이언트가 접근 제한된 API에 요청
    2. 서버는 401 Unauthorized를 주고 username과 password를 요청
    3. browser는 사용자에게 username과 password를 입력받아 다시 요청(header에 입력받은 username과 password를 BASE64로 Encode한 값 포함)
    * BASE64는 'username : password'를 encode
    4. 입력받은 값으로 확인 후 정상적인 API이용
 - 전송되는 값들이 encrypte & hash 등의 기술이 적용되지 않아 보안에 취약, 보완하기 위해 HTTPS를 사용  
 
 
## 3.Form Based Authentication
  - web application이 작성한 HTML 페이지에 credentails 정보를 입력해 사용자를 인증하는 방식
  - 과정
    1. 클라이언트가 접근 제한된 API에 요청
    2. 서버는 login page로 redirect 
    3. 사용자는 username과 password를 form data 입력받아 POST 메소드를 통해 전달
    4. 서버는 data를 통해 authentication process를 수행 후 인증된 사용자에 대한 Session ID를 생성
    5. Session Id가 정상적으로 생성되면, client에게 OK sign과 함께 auth cookie를 전달
    6. 클라이언트는 접근이 제한된 resource를 요청시  auth cookie를 함께 전달
    7. 서버는 사용자가 전달한 auth cookie와 server에 저장되어 있는 session id를 이용 인증
  - 가장 보편적인 인증방법으로 오직 self-contained app에만 적합한 인증방법  
  

## 4. JWT Authentication
  - digitally signed된 token을 전달해 사용자를 인증하는 방식
  - JWT(Java Web Token)를 이용 apps 간의 data를 transmit하는데 compact하고 safe한 방법을 제공
  - 과정
    1. 클라이언트가 Auth Server에 로그인(Auth Servers는 application내 또는 google 등의 3자)
    2. Auth Server에서 인증한 사용자는 JWT Token을 전달 받음
    3. 클라이언트는 요청시 JWT Token을 Authorization Header에 전달
    4. 서버는 JWT Token를 이용하여 유효성 검사
  - application server는 사용자의 session을 관리하지 않고 오직 JWT기 유효한 토큰인지만 확인
  - 하나의 End Point가 아닌 Mobile/Web 등의 multiple endpoint 환경이라면 통합적인 인증/인가 환경을 제공하기위해선 반드시 JWT를 사용
  - JWT : Header,Payload,Signatue로 구성
    - Header : token의 type과 JWT를 digitally sign할때 사용한 algorithm을 정의
    - Payload : JWT에 담아서 전달할 data를 정의
    - Signature : 위의 Header와 Payload 값을 base64로 encode한 값을 JWT secret key 값으로 encrypt한 값을 명시  

## Reference
<a href="https://velog.io/@minholee_93/series/Spring-Security">https://velog.io/@minholee_93/series/Spring-Security<a>

    
  
  
    
