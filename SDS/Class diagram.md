# Starlet_BE: 소프트웨어 설계 명세서 (SDS)


## Class Diagram (클래스 다이어그램)

이번 장은 Class diagram과 각각에 대한 설명을 기술한다.

본 프로젝트의 클래스 다이어그램은 '엔티티', '공통 모듈', '기능별' 관점으로 나누어 기술합니다.

### 3.1. 엔티티 클래스 다이어그램 (Entity Diagram)

프로젝트의 핵심 데이터 모델인 엔티티 간의 관계를 나타낸다.




### 3.2. 공통 단일 클래스 다이어그램 (Common Classes)

프로젝트 전반에서 사용되는 Enum, 공통 DTO, 유틸리티 클래스 등을 정의한다.

- 열거형
- 예외처리

### 3.3. 공유 모듈 클래스 다이어그램 (Shared Modules)

여러 도메인(기능)에서 공통으로 의존하는 서비스 모듈입니다.

- security 패키지
- S3 패키지
- 예외처리 패키지


### 3.4. 기능별 클래스 다이어그램 (Functional Diagrams)

주요 도메인(기능)별로 Controller, Service, Repository, Command(DTO) 간의 관계를 상세히 기술합니다.



## 3.1 엔티티 클래스 다이어그램

### Entity Relation Diagram
![alt text](Class%20Diagram%20UML/erd.png)


### Entity Class Diagram
![entity.png](Class%20Diagram%20UML/entity.png)













