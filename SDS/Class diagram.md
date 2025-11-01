# Starlet_BE: 소프트웨어 설계 명세서 (SDS)

---

## Class Diagram (클래스 다이어그램)

이번 장은 Class diagram과 각각에 대한 설명을 기술한다.

본 프로젝트의 클래스 다이어그램은 '엔티티', '공통 인프라', '기능별' 관점으로 나누어 기술한다.

### 3.1. 엔티티 클래스 다이어그램 (Entity Diagram)

프로젝트의 핵심 데이터 모델인 엔티티 간의 관계를 나타낸다.


### 3.2. 공통 인프라 다이어그램 (Common Infrastructure Diagram)

특정 도메인에 종속되지 않고 프로젝트 전반에서 사용되는 공통 설정 및 인프라 클래스들을 묶은 다이어그램이다.

애플리케이션의 기반 설정(보안, 예외 처리, 외부 연동 설정 등)을 분리하여 관리하는 것이 목적이다.

- Security

- Exception

- External Config

- API Docs


### 3.3. 기능별 클래스 다이어그램 (Functional Diagrams)

주요 도메인(기능)별로 Controller, Service, Repository, Command(DTO) 간의 관계를 상세히 기술한다.

1. 사용자 - User

2. 이메일 - Email

3. 검증 - Verify

4. 일기 - Diary

5. 별 - Star

6. 별자리 - Constellation

7. 별자리선 - Connection

8. 외부 서비스 - S3



클래스들을 정의할때 다음과 같은 규칙을 따른다.
1. 구현한 클래스는 해당 문서에서 1회만 Attribute와 Operation 정보를 기술한다.
2. 한번 정의된 클래스는 다시 출현 시 Attribute와 Operation 정보를 생략하고 클래스 이름만을 표기한다.
3. Getter, Setter, Constructor(Builder 패턴 제외)는 시각적 편의를 위해 생략한다.
4. 라이브러리로 존재하는 클래스 및 인터페이스들은 다이어그램에 표기하나, 설명을 적거나 Attribute, Operation 정보에 대해 필수로 기술하지 않는다.

---

## 3.1. 엔티티 클래스 다이어그램

### Entity Relation Diagram
![alt text](Class%20Diagram%20UML/erd.png)


### Entity Class Diagram
![entity.png](Class%20Diagram%20UML/entity.png)

---

### Class Diagram #1 : User
Class Description : 플랫폼의 사용자 Entity

| 구분            | 이름                                              | 설명               | 타입                    | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------|:-----------------|:----------------------|:--------------------|
| **Attribute** | `id`                                            | 사용자의 고유 식별자      | `Long`                | `Private`           |
| **Attribute** | `nickname`                                      | 사용자의 닉네임         | `String`              | `Private`           |
| **Attribute** | `password`                                      | 사용자의 비밀번호        | `String`              | `Private`           |
| **Attribute** | `email`                                         | 사용자의 이메일 정보      | `Email`               | `Private`           |
| **Attribute** | `profilePhotoUrl`                               | 사용자의 프로필 사진 URL  | `String`              | `Private`           |
| **Attribute** | `stars`                                         | 사용자가 소유한 별 목록    | `List<Star>`          | `Private`           |
| **Attribute** | `diaries`                                       | 사용자가 작성한 일기 목록   | `List<Diary>`         | `Private`           |
| **Attribute** | `constellations`                                | 사용자가 만든 별자리 목록   | `List<Constellation>` | `Private`           |
| **Operation** | `builder()`                                     | User 객체 빌더 생성    | `User`                | `Public`            |
| **Operation** | `toResDto()`                                    | 응답 데이터 전송 객체로 변환 | `UserResDto`          | `Public`            |
| **Operation** | `changePassword(String encodedPassword)`        | 비밀번호 변경          | `void`                | `Public`            |
| **Operation** | `changeProfilePhotoUrl(String profilePhotoUrl)` | 프로필 사진 URL 변경    | `void`                | `Public`            |
---

### Class Diagram #2: Email
Class Description: 사용자의 이메일 정보를 관리하는 Entity

| 구분            | 이름          | 설명             | 타입       | 접근 제한자 (Visibility) |
|:--------------|:------------|:---------------|:---------|:--------------------|
| **Attribute** | `id`        | 이메일의 고유 식별자    | `Long`   | `Private`           |
| **Attribute** | `address`   | 이메일 주소         | `String` | `Private`           |
| **Attribute** | `verify`    | 이메일 인증 정보      | `Verify` | `Private`           |
| **Attribute** | `user`      | 연관된 사용자 정보     | `User`   | `Private`           |
| **Operation** | `builder()` | Email 객체 빌더 생성 | `Email`  | `Public`            |

---

### Class Diagram #3: Verify
Class Description: 이메일 인증에 사용되는 인증 토큰 및 만료 정보 Entity

| 구분            | 이름                                                                      | 설명              | 타입              | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------------------|:----------------|:----------------|:--------------------|
| **Attribute** | `id`                                                                    | 인증 정보의 고유 식별자   | `Long`          | `Private`           |
| **Attribute** | `token`                                                                 | 인증 토큰 값         | `String`        | `Private`           |
| **Attribute** | `type`                                                                  | 인증 유형           | `VerifyType`    | `Private`           |
| **Attribute** | `expireTime`                                                            | 토큰 만료 시간        | `LocalDateTime` | `Private`           |
| **Attribute** | `email`                                                                 | 연관된 이메일 정보      | `Email`         | `Private`           |
| **Operation** | `builder()`                                                             | Verify 객체 빌더 생성 | `Verify`        | `Public`            |
| **Operation** | `updateStatus(String token, VerifyType type, LocalDateTime expireTime)` | 토큰 상태 업데이트      | `void`          | `Public`            |

---

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
| **Operation** | `builder()`                        | Diary 객체 빌더 생성 | `Diary`        | `Public`            |
| **Operation** | `updateContent(String newContent)` | 일기 내용 업데이트     | `void`         | `Public`            |

---

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
| **Operation** | `builder()`                                      | Star 객체 빌더 생성  | `Star`             | `Public`            |
| **Operation** | `joinConstellation(Constellation constellation)` | 별자리에 포함시키기     | `void`             | `Public`            |
| **Operation** | `changePosition(Double x, Double y)`             | 별 위치 변경        | `void`             | `Public`            |

---

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
| **Operation** | `builder()`                                   | Constellation 객체 빌더 생성 | `Constellation`    | `Public`            |
| **Operation** | `changeRepresentative()`                      | 대표 별자리 상태 변경           | `void`             | `Public`            |
| **Operation** | `changePosition(Double x, Double y)`          | 별자리 위치 변경              | `void`             | `Public`            |
| **Operation** | `updateInfo(String name, String description)` | 별자리 정보 업데이트            | `void`             | `Public`            |
| **Operation** | `setBelongDate(LocalDate belongDate)`         | 대표 별자리 지정 날짜 설정        | `void`             | `Public`            |

---

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

---

## 3.2. 공통 인프라 다이어그램

### Common Infrastructure Diagram

---

### 3.2.1. Security
![security.png](Class%20Diagram%20UML/security.png)

### Class Diagram #8: SecurityConfig
Class Description: Spring Security 설정을 정의하는 클래스. JWT 필터 및 인증/권한 관련 빈을 설정합니다.

| 구분            | 이름                                                                 | 설명                   | 타입                               | 접근 제한자 (Visibility) |
|:--------------|:-------------------------------------------------------------------|:---------------------|:---------------------------------|:--------------------|
| **Attribute** | `customUserDetailService`                                          | 사용자 상세 정보 서비스        | `CustomUserDetailService`        | `Private`           |
| **Attribute** | `jwtAuthenticationFilter`                                          | JWT 인증 필터            | `JwtAuthenticationFilter`        | `Private`           |
| **Attribute** | `customAccessDeniedHandler`                                        | 접근 거부 처리 핸들러         | `CustomAccessDeniedHandler`      | `Private`           |
| **Attribute** | `customAuthenticationEntryPoint`                                   | 인증되지 않은 사용자 접근 처리    | `CustomAuthenticationEntryPoint` | `Private`           |
| **Attribute** | `corsConfigurationSource`                                          | CORS 설정 소스           | `CorsConfigurationSource`        | `Private`           |
| **Operation** | `passwordEncoder()`                                                | 비밀번호 인코더 빈 생성        | `PasswordEncoder`                | `Public`            |
| **Operation** | `authenticationManager(AuthenticationConfiguration configuration)` | 인증 매니저 빈 생성          | `AuthenticationManager`          | `Public`            |
| **Operation** | `authenticationProvider()`                                         | 인증 제공자 빈 생성 (Dao 방식) | `AuthenticationProvider`         | `Public`            |
| **Operation** | `securityFilterChain(HttpSecurity http)`                           | 보안 필터 체인 설정          | `SecurityFilterChain`            | `Public`            |

---

### Class Diagram #9: JwtUtil
Class Description: JWT 토큰의 생성, 유효성 검증 및 정보 추출을 담당하는 유틸리티 클래스입니다.

| 구분            | 이름                                                          | 설명                                | 타입        | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------|:----------------------------------|:----------|:--------------------|
| **Attribute** | `secretKey`                                                 | JWT 서명에 사용할 시크릿 키                 | `String`  | `Private`           |
| **Attribute** | `accessValid`                                               | Access Token 유효 시간 (1시간)          | `long`    | `Private`           |
| **Attribute** | `refreshValid`                                              | Refresh Token 유효 시간 (7일)          | `long`    | `Private`           |
| **Operation** | `createAccessToken(String email)`                           | Access Token 발급                   | `String`  | `Public`            |
| **Operation** | `createRefreshToken(String email)`                          | Refresh Token 발급                  | `String`  | `Public`            |
| **Operation** | `generateToken(String email, long validTime)`               | 토큰 발급 종합 로직                       | `String`  | `Private`           |
| **Operation** | `getSigningKey()`                                           | 서명에 사용할 키 반환                      | `Key`     | `Private`           |
| **Operation** | `getEmailFromToken(String token)`                           | 토큰에서 이메일(Subject) 추출              | `String`  | `Public`            |
| **Operation** | `validateToken(String token)`                               | 토큰 유효성 검증                         | `boolean` | `Public`            |
| **Operation** | `resolveToken(HttpServletRequest request)`                  | HTTP 요청 헤더에서 토큰 추출 ("Bearer " 제거) | `String`  | `Public`            |
| **Operation** | `extractRefreshTokenFromCookie(HttpServletRequest request)` | 쿠키에서 Refresh Token 추출             | `String`  | `Public`            |

---

### Class Diagram #10: JwtAuthenticationFilter
Class Description: 모든 요청에 대해 JWT 토큰의 유효성을 검사하고, 유효한 경우 Security Context에 인증 정보를 설정하는 필터입니다.

| 구분            | 이름                                                                                                    | 설명             | 타입                        | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------------------------------------------------|:---------------|:--------------------------|:--------------------|
| **Attribute** | `jwtUtil`                                                                                             | JWT 관련 유틸리티    | `JwtUtil`                 | `Private`           |
| **Attribute** | `customUserDetailService`                                                                             | 사용자 상세 정보 서비스  | `CustomUserDetailService` | `Private`           |
| **Operation** | `doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)` | 필터 체인 내부 동작 정의 | `void`                    | `Protected`         |

---

### Class Diagram #11: CustomUserDetailService
Class Description: Spring Security의 UserDetailsService 인터페이스를 구현하여, 이메일을 기반으로 사용자 인증 정보를 로드하는 서비스입니다.

| 구분            | 이름                                 | 설명                | 타입               | 접근 제한자 (Visibility) |
|:--------------|:-----------------------------------|:------------------|:-----------------|:--------------------|
| **Attribute** | `userRepository`                   | 사용자 데이터 저장소       | `UserRepository` | `Private`           |
| **Operation** | `loadUserByUsername(String email)` | 이메일로 사용자 상세 정보 로드 | `UserDetails`    | `Public`            |

---

### Class Diagram #12: CorsConfig
Class Description: 애플리케이션의 Cross-Origin Resource Sharing (CORS) 설정을 정의하는 클래스입니다.

| 구분            | 이름                          | 설명                   | 타입                        | 접근 제한자 (Visibility) |
|:--------------|:----------------------------|:---------------------|:--------------------------|:--------------------|
| **Operation** | `corsConfigurationSource()` | CORS 설정 소스 빈 생성 및 구성 | `CorsConfigurationSource` | `Public`            |

---

### 3.2.2. Exception
![exception.png](Class%20Diagram%20UML/exception.png)

---

### Class Diagram #13: CustomAccessDeniedHandler
Class Description: 접근이 거부되었을 때(403 Forbidden) 사용자에게 커스텀된 JSON 응답을 반환하도록 처리하는 클래스입니다.

| 구분            | 이름                                                                                                              | 설명                            | 타입     | 접근 제한자 (Visibility) |
|:--------------|:----------------------------------------------------------------------------------------------------------------|:------------------------------|:-------|:--------------------|
| **Operation** | `handle(HttpServletRequest request, HttpServletResponse response, AccessDeniedException accessDeniedException)` | 접근 거부 예외 발생 시 호출되어 403 응답을 처리 | `void` | `Public`            |

---

### Class Diagram #14: CustomAuthenticationEntryPoint
Class Description: 인증되지 않은 사용자 접근 시(토큰이 없거나 만료된 경우, 401 Unauthorized) 커스텀된 JSON 응답을 반환하도록 처리하는 클래스입니다.

| 구분            | 이름                                                                                                          | 설명                         | 타입     | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------------------------------------------------------|:---------------------------|:-------|:--------------------|
| **Operation** | `commence(HttpServletRequest request, HttpServletResponse response, AuthenticationException authException)` | 인증 예외 발생 시 호출되어 401 응답을 처리 | `void` | `Public`            |

---

### Class Diagram #15: GlobalExceptionHandler
Class Description: 애플리케이션 전반에서 발생하는 다양한 예외(CustomException, 서버 오류, 유효성 검사 오류 등)를 중앙 집중식으로 처리하는 클래스입니다.

| 구분            | 이름                                                                                                     | 설명                                   | 타입                                    | 접근 제한자 (Visibility) |
|:--------------|:-------------------------------------------------------------------------------------------------------|:-------------------------------------|:--------------------------------------|:--------------------|
| **Operation** | `customExceptionHandler(CustomException e)`                                                            | 커스텀 예외(`CustomException`) 발생 시 처리    | `ResponseEntity<?>`                   | `Protected`         |
| **Operation** | `customServerException(Exception e)`                                                                   | 일반 서버 예외(`Exception`) 발생 시 500 응답 처리 | `ResponseEntity<?>`                   | `Protected`         |
| **Operation** | `handleValidationException(MethodArgumentNotValidException e)`                                         | 메소드 인자 유효성 검사 실패(`@Valid` 관련) 처리     | `ResponseEntity<Map<String, String>>` | `Protected`         |
| **Operation** | `handleMissingParam(org.springframework.web.bind.MissingServletRequestParameterException ex)`          | 필수 요청 파라미터 누락(`@RequestParam` 관련) 처리 | `ResponseEntity<ErrorDto>`            | `Protected`         |
| **Operation** | `handleTypeMismatch(org.springframework.web.method.annotation.MethodArgumentTypeMismatchException ex)` | 메소드 인자 타입 불일치 (날짜 형식 오류 등) 처리        | `ResponseEntity<ErrorDto>`            | `Protected`         |

---

### Class Diagram #16: CustomException
Class Description: 애플리케이션의 비즈니스 로직에서 발생하는 특정 오류를 나타내기 위해 정의된 커스텀 런타임 예외 클래스입니다.

| 구분            | 이름          | 설명        | 타입          | 접근 제한자 (Visibility) |
|:--------------|:------------|:----------|:------------|:--------------------|
| **Attribute** | `errorCode` | 정의된 오류 코드 | `ErrorCode` | `Private`           |

---

### Class Diagram #17: ErrorDto
Class Description: 클라이언트에게 오류 정보를 일관된 형식(상태 코드와 메시지)으로 전달하기 위한 데이터 전송 객체(`DTO`)입니다.

| 구분            | 이름        | 설명         | 타입       | 접근 제한자 (Visibility) |
|:--------------|:----------|:-----------|:---------|:--------------------|
| **Attribute** | `status`  | HTTP 상태 코드 | `int`    | `Private`           |
| **Attribute** | `message` | 오류 메시지     | `String` | `Private`           |
---

### 3.2.3. External Config
![external.png](Class%20Diagram%20UML/external.png)

---

### Class Diagram #18: S3Config
Class Description: Amazon S3 서비스 사용에 필요한 S3 클라이언트와 S3Presigner를 설정하고 빈으로 등록하는 Configuration 클래스입니다.

| 구분            | 이름              | 설명                                          | 타입            | 접근 제한자 (Visibility) |
|:--------------|:----------------|:--------------------------------------------|:--------------|:--------------------|
| **Attribute** | `region`        | S3 리전 정보 (`${s3.region}` 값 주입)              | `String`      | `Private`           |
| **Attribute** | `accessKey`     | AWS 액세스 키 (`${s3.access-key:}` 값 주입)        | `String`      | `Private`           |
| **Attribute** | `secretKey`     | AWS 시크릿 키 (`${s3.secret-key:}` 값 주입)        | `String`      | `Private`           |
| **Operation** | `s3Presigner()` | S3Presigner 객체 빈 생성 (Pre-signed URL 생성에 사용) | `S3Presigner` | `Public`            |
| **Operation** | `s3Client()`    | S3Client 객체 빈 생성 (S3 데이터 접근에 사용)            | `S3Client`    | `Public`            |

---

### 3.2.4. API Docs
![apidocs.png](Class%20Diagram%20UML/apidocs.png)

---

### Class Diagram #19: SwaggerConfig
Class Description: OpenAPI (Swagger) 문서를 설정하는 Configuration 클래스로, API 명세 정보, JWT 인증 방식 등을 정의합니다.

| 구분 | 이름 | 설명 | 타입 | 접근 제한자 (Visibility) |
| :--- | :--- | :--- | :--- | :--- |
| **Operation** | `openApi()` | 모든 경로에 대한 OpenAPI 그룹 설정 빈 생성 | `GroupedOpenApi` | `Public` |

---

## 3.3 기능별 클래스 다이어그램

### Functional Diagrams

해당 파트에서는 3.1에서 정의한 Entity 클래스에 대한 설명(표)은 생략한다.

---

### 3.3.1. User
![user.png](Class%20Diagram%20UML/user.png)


---

### 3.3.2. Email
![email.png](Class%20Diagram%20UML/email.png)


---

### 3.3.3. Verify
![verify.png](Class%20Diagram%20UML/verify.png)


---

### 3.3.4. Diary
![diary.png](Class%20Diagram%20UML/diary.png)


---

### 3.3.5. Star
![star.png](Class%20Diagram%20UML/star.png)


---

### 3.3.6. Constellation
![constellation.png](Class%20Diagram%20UML/constellation.png)


---

### 3.3.7. Connection
![connection.png](Class%20Diagram%20UML/connection.png)


---

### 3.3.8. External Services : S3
![s3.png](Class%20Diagram%20UML/s3.png)


---
