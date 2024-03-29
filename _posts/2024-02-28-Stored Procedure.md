---
layout: post
title: Stored Procedure
date: 2024-02-28 21:32 +0900
categories:
  - Database
  - MySQL
tags: 
math: true
---
# procedure


- 일련의 쿼리를 하나의 함수처럼 실행하기 위한 쿼리의 집합

# Procedure의 장점


-  데이터베이스 서버와 클라이언트 간의 통신을 줄임으로써 네트워크 부하 감소로 쿼리 **실행 속도 향상**
-  사용자 입력을 매개변수로만 전달받기에 **SQL 인젝션 방지**

# Procedure의 단점


- 복잡한 비즈니스 로직을 프로시저 내에 구현할 시 **디버깅과 유지보수 어려움**
- CPU와 메모리 자원 상당량 증가

# Procedure의 형식

```sql
DELIMITER $$
CREATE PROCEDURE '프로시저명' (
	IN 파라미터명 데이터타입,
	IN 파라미터명 데이터타입,
	OUT 파라미터명 반환데이터타입
)
BEING
	DECLARE 변수명 데이터타입 DEFAULT NULL;

	수행할 쿼리문 작성

END $$
DELIMETER;

CALL 프로시저명(@변수명);
SELECT @변수명;
```


### DELIMITER \$\$


- 명령어의 끝을 나타내는 **기호 변경**
- 프로시저 혹은 함수처럼, 같은 블록 내에서 여러 SQL문이 포함될 경우 **각각의 독립적인 명령문으로 해석하는 것을 방지하기 위함**
- 보편적으로 '\$\$' 또는 '//' 사용하지만, 세미콜론(;)외 어떠한 구분 기호를 사용하여도 무방

### END \$\$


- 프로시저의 끝을 명시
- DELIMITER에서 정의한 구분기호 사용

### DELIMITER ;


- 구분기호를 다시 세미콜론(;)으로 변경

### IN


- 파라미터를 받을 경우에 사용

### OUT


- 결과 값을 내보내는 경우에 사용

### DECLARE


- 변수 선언시 사용


### CALL


- 생성한 프로시저 호출
- 출력 매개변수가 있을시, 즉 결과 값을 내보낼 시 SELECT @변수명; 까지