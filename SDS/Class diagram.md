# Starlet_BE: 소프트웨어 설계 명세서 (SDS)


## Class Diagram (클래스 다이어그램)

이번 장은 Class diagram과 각각에 대한 설명을 기술한다.

본 프로젝트의 클래스 다이어그램은 '엔티티', '공통 인프라', '기능별' 관점으로 나누어 기술한다.

### 3.1. 엔티티 클래스 다이어그램 (Entity Diagram)

프로젝트의 핵심 데이터 모델인 엔티티 간의 관계를 나타낸다.


### 3.2. 공통 인프라 다이어그램 (Common Infrastructure Diagram)

특정 도메인에 종속되지 않고 프로젝트 전반에서 사용되는 공통 설정 및 인프라 클래스들을 묶은 다이어그램이다.

애플리케이션의 기반 설정(보안, 예외 처리, 외부 연동 설정 등)을 분리하여 관리하는 것이 목적이다.

포함 클래스 (Infrastructure & Config)

- Security: SecurityConfig, JwtUtil, CustomUserDetailService, JwtAuthenticationFilter, CorsConfig

- Exception: GlobalExceptionHandler, CustomException, ErrorCode, ErrorDto, CustomAccessDeniedHandler, CustomAuthenticationEntryPoint

- External Config: S3Config (domains.S3.Config)

- API Docs: SwaggerConfig (swagger)



### 3.3. 기능별 클래스 다이어그램 (Functional Diagrams)

주요 도메인(기능)별로 Controller, Service, Repository, Command(DTO) 간의 관계를 상세히 기술한다.

1. 사용자 & 이메일 & 검증 기능 (User & Email & Verify)

2. 일기 기능 (Diary)

3. 별 기능 (Star)

4. 별자리 & 연결 기능 (Constellation & Connection)

5. 외부 서비스 (External Services: S3)



클래스들을 정의할때 다음과 같은 규칙을 따른다.
1. 한번 정의된 클래스는 다시 출현 시 Attribute와 Operation 정보를 생략하고 클래스 이름만을 표기한다.
2. Getter, Setter, Constructor(Builder 패턴 제외)는 시각적 편의를 위해 생략한다.



## 3.1 엔티티 클래스 다이어그램

### Entity Relation Diagram
![alt text](Class%20Diagram%20UML/erd.png)


### Entity Class Diagram
![entity.png](Class%20Diagram%20UML/entity.png)


[//]: # (템플릿)
### Class Diagram #번호 : 클래스 이름
Class Description :

| 구분            | 이름                      | 설명             | 타입             | 접근 제한자 (Visibility)            |
|:--------------|:------------------------|:---------------|:---------------|:-------------------------------|
| **Attribute** | `attribute1`            | 속성 1에 대한 설명    | `Type1`        | `Private`/`Public`/`Protected` |
| **Attribute** | `attribute2`            | 속성 2에 대한 설명    | `Type2`        | `Private`/`Public`/`Protected` |
| **(생략 가능)**   | ...                     | ...            | ...            | ...                            |
| **Operation** | `operation1()`          | 오퍼레이션 1에 대한 설명 | `Return Type1` | `Public`/`Private`/`Protected` |
| **Operation** | `operation2(arg: Type)` | 오퍼레이션 2에 대한 설명 | `Return Type2` | `Public`/`Private`/`Protected` |
| **(생략 가능)**   | ...                     | ...            | ...            | ...                            |




### Class Diagram #1 : User
Class Description : 플랫폼의 사용자 Entity

| 구분            | 이름                 | 설명             | 타입                    | 접근 제한자 (Visibility)           |
|:--------------|:-------------------|:---------------|:----------------------|:------------------------------|
| **Attribute** | `id`               | 속성 1에 대한 설명    | `Long`                | `Private`                     |
| **Attribute** | `nickname`         | 속성 2에 대한 설명    | `String`              | `Private`                     |
| **Attribute** | `password`         | 속성 2에 대한 설명    | `String`              | `Private`                     |
| **Attribute** | `email`            | 속성 2에 대한 설명    | `Email`               | `Private`                     |
| **Attribute** | `profilePhotoUrl`  | 속성 2에 대한 설명    | `String`              | `Private`                     |
| **Attribute** | `stars`            | 속성 2에 대한 설명    | `List<Star>`          | `Private`                     |
| **Attribute** | `diaries`          | 속성 2에 대한 설명    | `List<Diary>`         | `Private`                     |
| **Attribute** | `constellations`   | 속성 2에 대한 설명    | `List<Constellation>` | `Private`                     |
| ...           | ...                | ...            | ...                   | ...                           |
| **Operation** | `builder()`        | 오퍼레이션 1에 대한 설명 | `User`                | `Public`                      |
| **Operation** | `toResDto()`       | 오퍼레이션 2에 대한 설명 | `UserResDto`          | `Public`                      |
| **Operation** | `changePassword()` | 오퍼레이션 2에 대한 설명 | `void`                | `Public`                      |

### Class Diagram #2: Email
Class Description: 사용자의 이메일 정보를 관리하는 Entity

| 구분            | 이름          | 설명             | 타입       | 접근 제한자 (Visibility) |
|:--------------|:------------|:---------------|:---------|:--------------------|
| **Attribute** | `id`        | 이메일의 고유 식별자    | `Long`   | `Private`           |
| **Attribute** | `address`   | 이메일 주소         | `String` | `Private`           |
| **Attribute** | `verify`    | 이메일 인증 정보      | `Verify` | `Private`           |
| **Attribute** | `user`      | 연관된 사용자 정보     | `User`   | `Private`           |
| ...           | ...         | ...            | ...      | ...                 |
| **Operation** | `builder()` | Email 객체 빌더 생성 | `Email`  | `Public`            |

### Class Diagram #3: Verify
Class Description: 이메일 인증에 사용되는 인증 토큰 및 만료 정보 Entity

| 구분            | 이름                                                                      | 설명              | 타입              | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------------------|:----------------|:----------------|:--------------------|
| **Attribute** | `id`                                                                    | 인증 정보의 고유 식별자   | `Long`          | `Private`           |
| **Attribute** | `token`                                                                 | 인증 토큰 값         | `String`        | `Private`           |
| **Attribute** | `type`                                                                  | 인증 유형           | `VerifyType`    | `Private`           |
| **Attribute** | `expireTime`                                                            | 토큰 만료 시간        | `LocalDateTime` | `Private`           |
| **Attribute** | `email`                                                                 | 연관된 이메일 정보      | `Email`         | `Private`           |
| ...           | ...                                                                     | ...             | ...             | ...                 |
| **Operation** | `builder()`                                                             | Verify 객체 빌더 생성 | `Verify`        | `Public`            |
| **Operation** | `updateStatus(String token, VerifyType type, LocalDateTime expireTime)` | 토큰 상태 업데이트      | `void`          | `Public`            |

### Class Diagram #4: Diary
Class Description: 사용자가 작성하는 일기 Entity

| 구분            | 이름                                 | 설명             | 타입             | 접근 제한자 (Visibility) |
|:--------------|:-----------------------------------|:---------------|:---------------|:--------------------|
| **Attribute** | `id`                               | 일기의 고유 식별자     | `Long`         | `Private`           |
| **Attribute** | `user`                             | 일기 작성자         | `User`         | `Private`           |
| **Attribute** | `emotion`                          | 일기의 감정         | `Emotion`      | `Private`           |
| **Attribute** | `factors`                          | 일기의 요소/키워드 목록  | `List<Factor>` | `Private`           |
| **Attribute** | `content`                          | 일기 내용          | `String`       | `Private`           |
| **Attribute** | `createAt`                         | 일기 작성 날짜       | `LocalDate`    | `Private`           |
| **Attribute** | `star`                             | 연관된 별 정보       | `Star`         | `Private`           |
| **Attribute** | `version`                          | 낙관적 락을 위한 버전   | `Long`         | `Private`           |
| ...           | ...                                | ...            | ...            | ...                 |
| **Operation** | `builder()`                        | Diary 객체 빌더 생성 | `Diary`        | `Public`            |
| **Operation** | `updateContent(String newContent)` | 일기 내용 업데이트     | `void`         | `Public`            |

### Class Diagram #5: Star
Class Description: 사용자의 일기를 기반으로 생성되는 별 Entity

| 구분            | 이름                                               | 설명             | 타입                 | 접근 제한자 (Visibility) |
|:--------------|:-------------------------------------------------|:---------------|:-------------------|:--------------------|
| **Attribute** | `id`                                             | 별의 고유 식별자      | `Long`             | `Private`           |
| **Attribute** | `color`                                          | 별의 색상          | `Color`            | `Private`           |
| **Attribute** | `x`                                              | 별의 X 좌표        | `Double`           | `Private`           |
| **Attribute** | `y`                                              | 별의 Y 좌표        | `Double`           | `Private`           |
| **Attribute** | `constellation`                                  | 속한 별자리 정보      | `Constellation`    | `Private`           |
| **Attribute** | `diary`                                          | 연관된 일기 정보      | `Diary`            | `Private`           |
| **Attribute** | `user`                                           | 별의 소유 사용자      | `User`             | `Private`           |
| **Attribute** | `connectionsAsStart`                             | 시작점으로 연결된 선 목록 | `List<Connection>` | `Private`           |
| **Attribute** | `connectionsAsEnd`                               | 끝점으로 연결된 선 목록  | `List<Connection>` | `Private`           |
| ...           | ...                                              | ...            | ...                | ...                 |
| **Operation** | `builder()`                                      | Star 객체 빌더 생성  | `Star`             | `Public`            |
| **Operation** | `joinConstellation(Constellation constellation)` | 별자리에 포함시키기     | `void`             | `Public`            |
| **Operation** | `changePosition(Double x, Double y)`             | 별 위치 변경        | `void`             | `Public`            |

### Class Diagram #6: Constellation
Class Description: 사용자가 만드는 별자리 Entity

| 구분            | 이름                                            | 설명                     | 타입                 | 접근 제한자 (Visibility) |
|:--------------|:----------------------------------------------|:-----------------------|:-------------------|:--------------------|
| **Attribute** | `id`                                          | 별자리의 고유 식별자            | `Long`             | `Private`           |
| **Attribute** | `user`                                        | 별자리를 만든 사용자            | `User`             | `Private`           |
| **Attribute** | `name`                                        | 별자리 이름                 | `String`           | `Private`           |
| **Attribute** | `description`                                 | 별자리 설명                 | `String`           | `Private`           |
| **Attribute** | `createAt`                                    | 별자리 생성일                | `LocalDate`        | `Private`           |
| **Attribute** | `belongDate`                                  | 대표 별자리로 지정된 날짜         | `LocalDate`        | `Private`           |
| **Attribute** | `isRepresentative`                            | 대표 별자리 여부              | `boolean`          | `Private`           |
| **Attribute** | `x`                                           | 별자리의 X 좌표              | `Double`           | `Private`           |
| **Attribute** | `y`                                           | 별자리의 Y 좌표              | `Double`           | `Private`           |
| **Attribute** | `stars`                                       | 별자리에 속한 별 목록           | `List<Star>`       | `Private`           |
| **Attribute** | `connections`                                 | 별자리의 연결선 목록            | `List<Connection>` | `Private`           |
| ...           | ...                                           | ...                    | ...                | ...                 |
| **Operation** | `builder()`                                   | Constellation 객체 빌더 생성 | `Constellation`    | `Public`            |
| **Operation** | `changeRepresentative()`                      | 대표 별자리 상태 변경           | `void`             | `Public`            |
| **Operation** | `changePosition(Double x, Double y)`          | 별자리 위치 변경              | `void`             | `Public`            |
| **Operation** | `updateInfo(String name, String description)` | 별자리 정보 업데이트            | `void`             | `Public`            |
| **Operation** | `setBelongDate(LocalDate belongDate)`         | 대표 별자리 지정 날짜 설정        | `void`             | `Public`            |

### Class Diagram #7: Connection
Class Description: 별자리 내의 별들을 잇는 연결선 Entity

| 구분            | 이름              | 설명                  | 타입              | 접근 제한자 (Visibility) |
|:--------------|:----------------|:--------------------|:----------------|:--------------------|
| **Attribute** | `id`            | 연결선의 고유 식별자         | `Long`          | `Private`           |
| **Attribute** | `constellation` | 속한 별자리 정보           | `Constellation` | `Private`           |
| **Attribute** | `start`         | 시작 별                | `Star`          | `Private`           |
| **Attribute** | `end`           | 끝 별                 | `Star`          | `Private`           |
| ...           | ...             | ...                 | ...             | ...                 |
| **Operation** | `builder()`     | Connection 객체 빌더 생성 | `Connection`    | `Public`            |




