---
layout: post
title: "[AWS] RDS Too many connection"
date: 2024-03-16 22:00 +0900
categories:
  - Troubleshooting
tags: 
math: true
---
# **문제**
- AWS RDS 사용 중, DB 연결이 끊기는 상황 발생


# 해결방법
- RDS 파라미터 중 `max_connections`, `connect_timeout` 설정 값 변경

> `max_connections`: 클라이언트가 **동시에 접속할 수 있는 커넥션 수**<br/>
> `connect_timeout`: 클라이언트가 **데이터베이스 서버에 연결하는 데 허용되는 최대 시간**

<br/><br/>

1. AWS RDS console에 접속<br/>
2. 좌측 탭에서 파라미터 그룹 클릭<br/>
3. 수정할 파라미터 그룹 선택
 ![](https://i.imgur.com/F7Oop9w.png)


`* 파라미터 그룹이 하나라면, connect_timeout 수정시 다음과 같은 에러가 뜨기 때문에 새로운 파라미터 그룹을 생성하고 수정해주면 된다.` <br/>
> `This parameter group myparameter cannot be modified because it is currently being applied to DB Instance errorpassing` 

<br/>

4.  `max_connections`, `connect_timeout` 각각 100, 180으로 수정
![](https://i.imgur.com/6OBZERm.png)
![](https://i.imgur.com/KuO3zlA.png)

<br/>

5. 다시 좌측 탭에서 데이터 베이스 클릭 후 수정
![](https://i.imgur.com/Qq4pprF.png)

<br/>

6. 추가 구성 - DB파라미터 그룹에서  `max_connections`, `connect_timeout` 값이 수정된 파라미터 그룹으로 지정
![](https://i.imgur.com/pWeI9dv.png)

<br/>

7. 수정 예약 - 즉시 적용 선택 후 저장하기
![](https://i.imgur.com/aF2oxww.png)
