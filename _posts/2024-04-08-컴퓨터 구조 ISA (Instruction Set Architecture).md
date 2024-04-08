---
layout: post
title: "[컴퓨터 구조] ISA (Instruction Set Architecture)"
date: 2024-04-08 09:02 +0900
categories:
  - CS
  - Architecture
tags: 
math: true
---
## **ISA (Instruction Set Architecture)**
- **CPU가 이해하고 실행할 수 있는 기계어 명령어 집합**
- 소프트웨어와 하드웨어 사이의 약속
- 각 CPU 아키텍처마다 고유의 ISA를 가지고 있으며, 이는 명령어의 종류, 형식, 주소 지정 방식 등을 정의
- CPU 설계 시 명령어 파이프라이닝의 용이성에 영향을 미친다.
- 고급 언어의 컴파일 과정을 보면<br/>
	- `high-level language` → `assembly language`<br/>
	- `assembly language` → `machin language`<br/>
	- `low-level language`<br/>
	- **어셈블러와 컴파일러를 거쳐 저급 언어로 변환**된다.<br/>
	- 저급 언어로 변환된 후, 하드웨어에 명령을 내려줘야 하는데 이때 **소프트웨어와 하드웨어 사이를 연결해주는 것이 ISA**이다.
![](https://i.imgur.com/3srp3xP.png)


## **CISC (Complex Instrunction Set Computer)**
- CISC는 복잡하고 다양한 명령어 집합 사용 (x86, x86-64)
- 상대적으로 적은 수의 명령어로도 프로그램을 실행할 수 있다.
- **명령어 파이프라이닝이 불리하다**는 단점이 있다.
	- 복잡하고 다양한 명령어로 **명령어 하나를 실행하는 데에 여러 클럭 주기가 필요**하기 때문이다.
	- 파이프라이닝이 잘되려면 명령어 실행이 정형화 되어있어야 한다. (명령어의 길이 혹은 실행시간)
	- ![](https://i.imgur.com/gnwN68Q.png)
	- ![](https://i.imgur.com/xa9dV7k.png)
- 복잡하고 다양한 명령어를 활용한다지만 이는 사용 빈도가 낮다.
## **RISC (Reduced Instruction Set Computer)**
- RISC는 단순하고 적은 수의 고정 길이 명령어 집합을 활용
- 메모리 접근 최소화(road,store) , 레지스터 활용
- 범용 레지스터 종류가 더 많은 경우도 있다.
- CISC에 비해 명령어 종류는 적지만, 프로그램 실행에 필요한 명령어 수는 더 많다.


**CISC와 RISC의 차이점을 한 눈에 정리해보자**

| CISC                 | RISC                 |
| -------------------- | -------------------- |
| 복잡하고 다양한 명령어         | 단순하고 적은 명령어          |
| 가변 길이 명령어            | 고정 길이 명령어            |
| 다양한 주소 지정 방식         | 적은 주소 지정 방식          |
| 프로그램을 이루는 명령어의 수가 적음 | 프로그램을 이루는 명령어의 수가 많음 |
| 여러 클럭에 걸쳐 명령어 수행     | 1클럭 내외로 명령어 수행       |
| 파이프라이닝하기 어려움         | 파이프라이닝하기 쉬움          |


`* CISC 명령어는 내부적으로 RISC 형대의 마이크로 명령어로 변환되어 처리된다. 이를 통해 CISC의 호환성을 유지하면서도 RISC의 파이프라이닝 이점을 취할 수 있다.`