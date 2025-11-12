# Starlet: 소프트웨어 설계 명세서 (SDS)

---

## 3. Class Diagram (클래스 다이어그램)

이번 장은 Class diagram과 각각에 대한 설명을 기술한다.

본 프로젝트의 클래스 다이어그램은 '엔티티', '공통 인프라', '기능별' 관점으로 나누어 기술한다.

### 3.1. 엔티티 클래스 다이어그램 (Entity Diagram)

프로젝트의 핵심 데이터 모델인 엔티티 간의 관계를 나타낸다.

1. 사용자 - User

2. 이메일 - Email

3. 검증 - Verify

4. 일기 - Diary

5. 별 - Star

6. 별자리 - Constellation

7. 별자리 선 - Connection


### 3.2. 공통 인프라 다이어그램 (Common Infrastructure Diagram)

특정 도메인에 종속되지 않고 프로젝트 전반에서 사용되는 공통 설정 및 인프라 클래스들을 묶은 다이어그램이다.

애플리케이션의 기반 설정(보안, 예외 처리, 외부 연동 설정 등)을 분리하여 관리하는 것이 목적이다.

1. 보안 - Security

2. 예외처리 - Exception

3. 외부 연동 클래스 설정 - External Config

4. API 명세서 - API Docs


### 3.3. 기능별 클래스 다이어그램 (Functional Diagrams)

주요 도메인(기능)별로 Controller, Service, Repository, Command(데이터 전송 클래스), Api(Interface) 간의 관계를 상세히 기술한다.

1. 사용자 - User

2. 이메일 - Email

3. 검증 - Verify

4. 일기 - Diary

5. 별 - Star

6. 별자리 - Constellation

7. 별자리 선 - Connection




### 클래스들을 정의할때 다음과 같은 규칙을 따른다.
- 구현한 클래스는 해당 문서에서 1회만 Attribute와 Operation 정보를 기술하며, 한번 정의된 클래스는 다시 출현 시 Attribute와 Operation 정보를 생략하고 클래스 이름만을 표기한다.
- Getter, Setter, Constructor(Builder 패턴 제외)는 시각적 편의를 위해 생략한다.
- 라이브러리로 존재하는 클래스 및 인터페이스들은 다이어그램에 표기하나, 설명을 적거나 Attribute, Operation 정보에 대해 필수로 기술하지 않는다.

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
| **Attribute** | `verify`    | 인증 정보          | `Verify` | `Private`           |
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

| 구분            | 이름                                 | 설명                | 타입             | 접근 제한자 (Visibility) |
|:--------------|:-----------------------------------|:------------------|:---------------|:--------------------|
| **Attribute** | `id`                               | 일기의 고유 식별자        | `Long`         | `Private`           |
| **Attribute** | `user`                             | 일기 작성자            | `User`         | `Private`           |
| **Attribute** | `emotion`                          | 일기의 감정            | `Emotion`      | `Private`           |
| **Attribute** | `factors`                          | 일기의 키워드 목록        | `List<Factor>` | `Private`           |
| **Attribute** | `content`                          | 일기 내용             | `String`       | `Private`           |
| **Attribute** | `createAt`                         | 일기 작성 날짜          | `LocalDate`    | `Private`           |
| **Attribute** | `star`                             | 연관된 별 정보          | `Star`         | `Private`           |
| **Attribute** | `version`                          | 레이스 컨디션 방지를 위한 버전 | `Long`         | `Private`           |
| **Operation** | `builder()`                        | Diary 객체 빌더 생성    | `Diary`        | `Public`            |
| **Operation** | `updateContent(String newContent)` | 일기 내용 업데이트        | `void`         | `Public`            |

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
| **Attribute** | `belongDate`                                  | 별자리가 속한 분기(2달 단위)      | `LocalDate`        | `Private`           |
| **Attribute** | `isRepresentative`                            | 대표 별자리 여부              | `boolean`          | `Private`           |
| **Attribute** | `x`                                           | 별자리의 X 좌표              | `Double`           | `Private`           |
| **Attribute** | `y`                                           | 별자리의 Y 좌표              | `Double`           | `Private`           |
| **Attribute** | `stars`                                       | 별자리에 속한 별 목록           | `List<Star>`       | `Private`           |
| **Attribute** | `connections`                                 | 별자리의 연결선 목록            | `List<Connection>` | `Private`           |
| **Operation** | `builder()`                                   | Constellation 객체 빌더 생성 | `Constellation`    | `Public`            |
| **Operation** | `changeRepresentative()`                      | 대표 별자리 상태 변경           | `void`             | `Public`            |
| **Operation** | `changePosition(Double x, Double y)`          | 별자리 위치 변경              | `void`             | `Public`            |
| **Operation** | `updateInfo(String name, String description)` | 별자리 정보 업데이트            | `void`             | `Public`            |
| **Operation** | `setBelongDate(LocalDate belongDate)`         | 별자리 소속 분기 설정           | `void`             | `Public`            |

---

### Class Diagram #7: Connection
Class Description: 별자리 내의 별들을 잇는 연결선 Entity

| 구분            | 이름              | 설명                  | 타입              | 접근 제한자 (Visibility) |
|:--------------|:----------------|:--------------------|:----------------|:--------------------|
| **Attribute** | `id`            | 연결선의 고유 식별자         | `Long`          | `Private`           |
| **Attribute** | `constellation` | 속한 별자리 정보           | `Constellation` | `Private`           |
| **Attribute** | `start`         | 시작 별                | `Star`          | `Private`           |
| **Attribute** | `end`           | 끝 별                 | `Star`          | `Private`           |
| **Operation** | `builder()`     | Connection 객체 빌더 생성 | `Connection`    | `Public`            |

---

## 3.2. 공통 인프라 다이어그램

### Common Infrastructure Diagram

---

### 3.2.1. Security
![security.png](Class%20Diagram%20UML/security.png)

### Class Diagram #8: SecurityConfig
Class Description: Spring Security 설정을 정의하는 클래스이다. JWT 필터 및 인증/권한 관련 빈을 설정한다.

| 구분            | 이름                                                                 | 설명                | 타입                               | 접근 제한자 (Visibility) |
|:--------------|:-------------------------------------------------------------------|:------------------|:---------------------------------|:--------------------|
| **Attribute** | `customUserDetailService`                                          | 사용자 상세 정보 서비스     | `CustomUserDetailService`        | `Private`           |
| **Attribute** | `jwtAuthenticationFilter`                                          | JWT 인증 필터         | `JwtAuthenticationFilter`        | `Private`           |
| **Attribute** | `customAccessDeniedHandler`                                        | 접근 거부 처리 핸들러      | `CustomAccessDeniedHandler`      | `Private`           |
| **Attribute** | `customAuthenticationEntryPoint`                                   | 인증되지 않은 사용자 접근 처리 | `CustomAuthenticationEntryPoint` | `Private`           |
| **Attribute** | `corsConfigurationSource`                                          | CORS 설정 소스        | `CorsConfigurationSource`        | `Private`           |
| **Operation** | `passwordEncoder()`                                                | 비밀번호 인코더 빈 생성     | `PasswordEncoder`                | `Public`            |
| **Operation** | `authenticationManager(AuthenticationConfiguration configuration)` | 인증 매니저 빈 생성       | `AuthenticationManager`          | `Public`            |
| **Operation** | `authenticationProvider()`                                         | 인증 제공자 빈 생성       | `AuthenticationProvider`         | `Public`            |
| **Operation** | `securityFilterChain(HttpSecurity http)`                           | 보안 필터 체인 설정       | `SecurityFilterChain`            | `Public`            |

---

### Class Diagram #9: JwtUtil
Class Description: JWT 토큰의 생성, 유효성 검증 및 정보 추출을 담당하는 유틸리티 클래스이다.

| 구분            | 이름                                                          | 설명                               | 타입        | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------|:---------------------------------|:----------|:--------------------|
| **Attribute** | `secretKey`                                                 | JWT 서명에 사용할 시크릿 키                | `String`  | `Private`           |
| **Attribute** | `accessValid`                                               | Access Token 유효 시간               | `long`    | `Private`           |
| **Attribute** | `refreshValid`                                              | Refresh Token 유효 시간              | `long`    | `Private`           |
| **Operation** | `createAccessToken(String email)`                           | Access Token 발급                  | `String`  | `Public`            |
| **Operation** | `createRefreshToken(String email)`                          | Refresh Token 발급                 | `String`  | `Public`            |
| **Operation** | `generateToken(String email, long validTime)`               | 토큰 발급 종합 로직                      | `String`  | `Private`           |
| **Operation** | `getSigningKey()`                                           | 서명에 사용할 키 반환                     | `Key`     | `Private`           |
| **Operation** | `getEmailFromToken(String token)`                           | 토큰에서 이메일 추출                      | `String`  | `Public`            |
| **Operation** | `validateToken(String token)`                               | 토큰 유효성 검증                        | `boolean` | `Public`            |
| **Operation** | `resolveToken(HttpServletRequest request)`                  | HTTP 요청 헤더에서 토큰 추출               | `String`  | `Public`            |
| **Operation** | `extractRefreshTokenFromCookie(HttpServletRequest request)` | 쿠키에서 Refresh Token 추출            | `String`  | `Public`            |

---

### Class Diagram #10: JwtAuthenticationFilter
Class Description: 모든 요청에 대해 JWT 토큰의 유효성을 검사하고 유효한 경우 Security Context에 인증 정보를 설정하는 필터이다.

| 구분            | 이름                                                                                                    | 설명             | 타입                        | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------------------------------------------------|:---------------|:--------------------------|:--------------------|
| **Attribute** | `jwtUtil`                                                                                             | JWT 관련 유틸리티    | `JwtUtil`                 | `Private`           |
| **Attribute** | `customUserDetailService`                                                                             | 사용자 상세 정보      | `CustomUserDetailService` | `Private`           |
| **Operation** | `doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)` | 필터 체인 내부 동작 정의 | `void`                    | `Protected`         |

---

### Class Diagram #11: CustomUserDetailService
Class Description: Spring Security의 UserDetailsService 인터페이스를 구현하여 이메일을 기반으로 사용자 인증 정보를 로드하는 서비스이다.

| 구분            | 이름                                 | 설명                | 타입               | 접근 제한자 (Visibility) |
|:--------------|:-----------------------------------|:------------------|:-----------------|:--------------------|
| **Attribute** | `userRepository`                   | 사용자 데이터 저장소       | `UserRepository` | `Private`           |
| **Operation** | `loadUserByUsername(String email)` | 이메일로 사용자 상세 정보 로드 | `UserDetails`    | `Public`            |

---

### Class Diagram #12: CorsConfig
Class Description: 애플리케이션의 Cross-Origin Resource Sharing (CORS) 설정을 정의하는 클래스이다. FE 서버와 연결하기 위해 필수로 정의되어야 한다.

| 구분            | 이름                          | 설명                   | 타입                        | 접근 제한자 (Visibility) |
|:--------------|:----------------------------|:---------------------|:--------------------------|:--------------------|
| **Operation** | `corsConfigurationSource()` | CORS 설정 소스 빈 생성 및 구성 | `CorsConfigurationSource` | `Public`            |

---

### 3.2.2. Exception
![exception.png](Class%20Diagram%20UML/exception.png)

---

### Class Diagram #13: CustomAccessDeniedHandler
Class Description: 접근이 거부되었을 때(403 Forbidden) 사용자에게 커스텀된 JSON 응답을 반환하도록 처리하는 클래스이다.

| 구분            | 이름                                                                                                              | 설명                            | 타입     | 접근 제한자 (Visibility) |
|:--------------|:----------------------------------------------------------------------------------------------------------------|:------------------------------|:-------|:--------------------|
| **Operation** | `handle(HttpServletRequest request, HttpServletResponse response, AccessDeniedException accessDeniedException)` | 접근 거부 예외 발생 시 호출되어 403 응답을 처리 | `void` | `Public`            |

---

### Class Diagram #14: CustomAuthenticationEntryPoint
Class Description: 인증되지 않은 사용자 접근 시(토큰이 없거나 만료된 경우, 401 Unauthorized) 커스텀된 JSON 응답을 반환하도록 처리하는 클래스이다.

| 구분            | 이름                                                                                                          | 설명                         | 타입     | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------------------------------------------------------|:---------------------------|:-------|:--------------------|
| **Operation** | `commence(HttpServletRequest request, HttpServletResponse response, AuthenticationException authException)` | 인증 예외 발생 시 호출되어 401 응답을 처리 | `void` | `Public`            |

---

### Class Diagram #15: GlobalExceptionHandler
Class Description: 애플리케이션 전반에서 발생하는 다양한 예외(CustomException, 서버 오류, 유효성 검사 오류 등)를 중앙 집중식으로 처리하는 클래스이다.

| 구분            | 이름                                                                                                     | 설명                                   | 타입                                    | 접근 제한자 (Visibility) |
|:--------------|:-------------------------------------------------------------------------------------------------------|:-------------------------------------|:--------------------------------------|:--------------------|
| **Operation** | `customExceptionHandler(CustomException e)`                                                            | 커스텀 예외(`CustomException`) 발생 시 처리    | `ResponseEntity<?>`                   | `Protected`         |
| **Operation** | `customServerException(Exception e)`                                                                   | 일반 서버 예외(`Exception`) 발생 시 500 응답 처리 | `ResponseEntity<?>`                   | `Protected`         |
| **Operation** | `handleValidationException(MethodArgumentNotValidException e)`                                         | 메소드 인자 유효성 검사 실패(`@Valid` 관련) 처리     | `ResponseEntity<Map<String, String>>` | `Protected`         |
| **Operation** | `handleMissingParam(org.springframework.web.bind.MissingServletRequestParameterException ex)`          | 필수 요청 파라미터 누락(`@RequestParam` 관련) 처리 | `ResponseEntity<ErrorDto>`            | `Protected`         |
| **Operation** | `handleTypeMismatch(org.springframework.web.method.annotation.MethodArgumentTypeMismatchException ex)` | 메소드 인자 타입 불일치 (날짜 형식 오류 등) 처리        | `ResponseEntity<ErrorDto>`            | `Protected`         |

---

### Class Diagram #16: CustomException
Class Description: 애플리케이션의 비즈니스 로직에서 발생하는 특정 오류를 나타내기 위해 정의된 커스텀 런타임 예외 클래스이다.

| 구분            | 이름          | 설명        | 타입          | 접근 제한자 (Visibility) |
|:--------------|:------------|:----------|:------------|:--------------------|
| **Attribute** | `errorCode` | 정의된 오류 코드 | `ErrorCode` | `Private`           |

---

### Class Diagram #17: ErrorDto
Class Description: 클라이언트에게 오류 정보를 일관된 형식(상태 코드와 메시지)으로 전달하기 위한 데이터 전송 클래스이다.

| 구분            | 이름        | 설명         | 타입       | 접근 제한자 (Visibility) |
|:--------------|:----------|:-----------|:---------|:--------------------|
| **Attribute** | `status`  | HTTP 상태 코드 | `int`    | `Private`           |
| **Attribute** | `message` | 오류 메시지     | `String` | `Private`           |
---

### 3.2.3. External Config
![external.png](Class%20Diagram%20UML/external.png)

---

### Class Diagram #18: S3Config
Class Description: Amazon S3 서비스 사용에 필요한 S3 클라이언트와 S3Presigner를 설정하고 빈으로 등록하는 Configuration 클래스이다.

| 구분            | 이름              | 설명                  | 타입            | 접근 제한자 (Visibility) |
|:--------------|:----------------|:--------------------|:--------------|:--------------------|
| **Attribute** | `region`        | S3 리전 정보            | `String`      | `Private`           |
| **Attribute** | `accessKey`     | AWS 액세스 키           | `String`      | `Private`           |
| **Attribute** | `secretKey`     | AWS 시크릿 키           | `String`      | `Private`           |
| **Operation** | `s3Presigner()` | S3Presigner 객체 빈 생성 | `S3Presigner` | `Public`            |
| **Operation** | `s3Client()`    | S3Client 객체 빈 생성    | `S3Client`    | `Public`            |

---

### 3.2.4. API Docs
![apidocs.png](Class%20Diagram%20UML/apidocs.png)

---

### Class Diagram #19: SwaggerConfig
Class Description: Swagger 문서를 설정하는 Configuration 클래스이다. FE와 협업하기 위한 API 명세서의 역할을 한다.

| 구분            | 이름          | 설명                           | 타입               | 접근 제한자 (Visibility) |
|:--------------|:------------|:-----------------------------|:-----------------|:--------------------|
| **Operation** | `openApi()` | 모든 경로에 대한 OpenAPI 그룹 설정 빈 생성 | `GroupedOpenApi` | `Public`            |

---

## 3.3 기능별 클래스 다이어그램

### Functional Diagrams

해당 파트에서는 3.1에서 정의한 Entity 클래스에 대한 설명(표)은 생략한다.

---

### 3.3.1. User
![user.png](Class%20Diagram%20UML/user.png)

---

### Class Diagram #20: SignUpDto
Class Description: 회원가입 요청 시 사용자 정보를 담는 데이터 전송 클래스이다.

| 구분            | 이름                                              | 설명                                   | 타입       | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------|:-------------------------------------|:---------|:--------------------|
| **Attribute** | `nickname`                                      | 사용자 닉네임                              | `String` | `Private`           |
| **Attribute** | `password`                                      | 비밀번호                                 | `String` | `Private`           |
| **Attribute** | `email`                                         | 사용자 이메일                              | `String` | `Private`           |
| **Operation** | `toEntity(String encodedPassword, Email email)` | 암호화된 비밀번호와 이메일 객체를 포함하여 User 엔티티로 변환 | `User`   | `Public`            |

---
### Class Diagram #21: LoginInfoDto
Class Description: 로그인 성공 시 사용자 정보와 발급된 JWT 토큰을 담아 응답하는 데이터 전송 클래스이다. 토큰은 발급 이후 FE에서 저장하고 삭제한다.

| 구분            | 이름             | 설명                    | 타입             | 접근 제한자 (Visibility) |
|:--------------|:---------------|:----------------------|:---------------|:--------------------|
| **Attribute** | `userId`       | 사용자 고유 ID             | `Long`         | `Private`           |
| **Attribute** | `email`        | 사용자 이메일               | `String`       | `Private`           |
| **Attribute** | `nickname`     | 사용자 닉네임               | `String`       | `Private`           |
| **Attribute** | `accessToken`  | 발급된 Access Token      | `String`       | `Private`           |
| **Attribute** | `refreshToken` | 발급된 Refresh Token     | `String`       | `Private`           |
| **Operation** | `builder()`    | LoginInfoDto 객체 빌더 생성 | `LoginInfoDto` | `Public`            |

---
### Class Diagram #22: UserRepository
Class Description: User 엔티티의 영속성 관리를 위한 JPA Repository 인터페이스이다. 추가구현하지 않고 기본적으로 정의되어있는 JPA 메소드들은 생략한다.

| 구분            | 이름                                   | 설명                   | 타입               | 접근 제한자 (Visibility) |
|:--------------|:-------------------------------------|:---------------------|:-----------------|:--------------------|
| **Operation** | `existsByEmailAddress(String email)` | 이메일 주소로 사용자 존재 여부 확인 | `boolean`        | `Public`            |
| **Operation** | `existsByNickname(String nickname)`  | 닉네임으로 사용자 존재 여부 확인   | `boolean`        | `Public`            |
| **Operation** | `findByEmailAddress(String email)`   | 이메일 주소로 사용자 조회       | `Optional<User>` | `Public`            |

---
### Class Diagram #23: UserApi
Class Description: 회원 관련 API 엔드포인트를 정의하는 인터페이스이다. (Swagger 문서용 Tag/Operation 정의 포함)

| 구분            | 이름                                                                    | 설명                  | 타입                  | 접근 제한자 (Visibility) |
|:--------------|:----------------------------------------------------------------------|:--------------------|:--------------------|:--------------------|
| **Operation** | `getUser(@PathVariable Long id)`                                      | 회원 고유 ID를 통한 회원 조회  | `ResponseEntity<?>` | `Public`            |
| **Operation** | `getUserList()`                                                       | 모든 회원 정보 조회         | `ResponseEntity<?>` | `Public`            |
| **Operation** | `signUp(@Valid @RequestBody SignUpDto dto)`                           | 회원가입 기능             | `ResponseEntity<?>` | `Public`            |
| **Operation** | `existNickname(@RequestParam String nickname)`                        | 사용 가능한 닉네임 검사       | `ResponseEntity<?>` | `Public`            |
| **Operation** | `login(@RequestBody LoginDto dto, HttpServletResponse res)`           | 로그인 및 토큰 발급         | `ResponseEntity<?>` | `Public`            |
| **Operation** | `deleteCurrentUser(@AuthenticationPrincipal UserDetails userDetails)` | 현재 로그인 사용자 회원탈퇴(삭제) | `ResponseEntity<?>` | `Public`            |
| **Operation** | `logout(HttpServletResponse response)`                                | 로그아웃                | `ResponseEntity<?>` | `Public`            |

---
### Class Diagram #24: UserService
Class Description: 사용자(User)의 비즈니스 로직(회원가입, 로그인, 탈퇴 등)을 처리하는 서비스 클래스이다.

| 구분            | 이름                                             | 설명                    | 타입                 | 접근 제한자 (Visibility) |
|:--------------|:-----------------------------------------------|:----------------------|:-------------------|:--------------------|
| **Attribute** | `userRepository`                               | 사용자 엔티티 저장소           | `UserRepository`   | `Private`           |
| **Attribute** | `passwordEncoder`                              | 비밀번호 인코더              | `PasswordEncoder`  | `Private`           |
| **Attribute** | `jwtUtil`                                      | JWT 유틸리티              | `JwtUtil`          | `Private`           |
| **Attribute** | `verifyRepository`                             | 인증 엔티티 저장소            | `VerifyRepository` | `Private`           |
| **Attribute** | `emailService`                                 | 이메일 관련 서비스            | `EmailService`     | `Private`           |
| **Operation** | `getUser(Long id)`                             | ID 기반 사용자 정보 단일 조회    | `UserResDto`       | `Public`            |
| **Operation** | `getUserList()`                                | 모든 사용자 목록 조회          | `List<UserResDto>` | `Public`            |
| **Operation** | `signUp(SignUpDto dto)`                        | 회원가입 처리 로직            | `User`             | `Public`            |
| **Operation** | `existNickname(String nickname)`               | 닉네임 존재 여부 확인          | `boolean`          | `Public`            |
| **Operation** | `login(LoginDto dto, HttpServletResponse res)` | 로그인 및 JWT 토큰 발급/쿠키 설정 | `LoginInfoDto`     | `Public`            |
| **Operation** | `deleteCurrentUser(String email)`              | 이메일 기반 현재 사용자 회원 탈퇴   | `void`             | `Public`            |
| **Operation** | `findByEmailAddress(String email)`             | 이메일 주소로 User 엔티티 조회   | `User`             | `Public`            |
| **Operation** | `logout(HttpServletResponse res)`              | 로그아웃                  | `void`             | `Public`            |

---
### Class Diagram #25: LoginDto
Class Description: 로그인 요청 시 사용자 이메일과 비밀번호를 담는 데이터 전송 클래스이다.

| 구분            | 이름         | 설명                 | 타입       | 접근 제한자 (Visibility) |
|:--------------|:-----------|:-------------------|:---------|:--------------------|
| **Attribute** | `email`    | 사용자 이메일            | `String` | `Private`           |
| **Attribute** | `password` | 비밀번호               | `String` | `Private`           |

---
### Class Diagram #26: UserResDto
Class Description: 사용자 목록 조회 및 단일 조회에 대한 응답 정보를 담는 데이터 전송 클래스이다.

| 구분            | 이름          | 설명                  | 타입           | 접근 제한자 (Visibility) |
|:--------------|:------------|:--------------------|:-------------|:--------------------|
| **Attribute** | `id`        | 사용자 고유 ID           | `Long`       | `Private`           |
| **Attribute** | `nickname`  | 사용자 닉네임             | `String`     | `Private`           |
| **Attribute** | `email`     | 사용자 이메일             | `String`     | `Private`           |
| **Operation** | `builder()` | UserResDto 객체 빌더 생성 | `UserResDto` | `Public`            |

---
### Class Diagram #27: UserController
Class Description: 사용자 관련 API 요청을 받아 UserService로 전달하는 REST Controller이다.

| 구분            | 이름                                                                    | 설명              | 타입                  | 접근 제한자 (Visibility) |
|:--------------|:----------------------------------------------------------------------|:----------------|:--------------------|:--------------------|
| **Attribute** | `userService`                                                         | 사용자 관리 서비스      | `UserService`       | `Private`           |
| **Attribute** | `emailService`                                                        | 이메일 관련 서비스      | `EmailService`      | `Private`           |
| **Operation** | `getUser(@PathVariable Long id)`                                      | 회원 ID 조회 엔드포인트  | `ResponseEntity<?>` | `Public`            |
| **Operation** | `getUserList()`                                                       | 회원 목록 조회 엔드포인트  | `ResponseEntity<?>` | `Public`            |
| **Operation** | `signUp(@Valid @RequestBody SignUpDto dto)`                           | 회원가입 엔드포인트      | `ResponseEntity<?>` | `Public`            |
| **Operation** | `existNickname(@RequestParam String nickname)`                        | 닉네임 중복 확인 엔드포인트 | `ResponseEntity<?>` | `Public`            |
| **Operation** | `login(@Valid @RequestBody LoginDto dto, HttpServletResponse res)`    | 로그인 엔드포인트       | `ResponseEntity<?>` | `Public`            |
| **Operation** | `deleteCurrentUser(@AuthenticationPrincipal UserDetails userDetails)` | 회원탈퇴 엔드포인트      | `ResponseEntity<?>` | `Public`            |
| **Operation** | `logout(HttpServletResponse response)`                                | 로그아웃 엔드포인트      | `ResponseEntity<?>` | `Public`            |


---

### 3.3.2. Email
![email.png](Class%20Diagram%20UML/email.png)

### Class Diagram #28: EmailAddressDto
Class Description: 이메일 주소만 포함하는 데이터 전송 클래스이다. 중복 확인, 인증 메일 발송 등에 사용된다.

| 구분            | 이름      | 설명                  | 타입       | 접근 제한자 (Visibility) |
|:--------------|:--------|:--------------------|:---------|:--------------------|
| **Attribute** | `email` | 사용자 이메일 (형식 검사, 필수) | `String` | `Private`           |

---
### Class Diagram #29: EmailAPI
Class Description: 이메일 관련 API 엔드포인트를 정의하는 인터페이스이다. (Swagger 문서용 Tag/Operation 정의 포함)

| 구분            | 이름                                                       | 설명                       | 타입                  | 접근 제한자 (Visibility) |
|:--------------|:---------------------------------------------------------|:-------------------------|:--------------------|:--------------------|
| **Operation** | `checkDuplication(@RequestParam String address)`         | 이메일 주소 중복확인              | `ResponseEntity<?>` | `Public`            |
| **Operation** | `getVerificationStatus(@RequestParam String address)`    | 이메일 정보(인증 상태 및 만료 기간) 조회 | `ResponseEntity<?>` | `Public`            |
| **Operation** | `initEmail(@RequestBody EmailAddressDto dto)`            | 가입 가능한 이메일에 인증 메일 발송     | `ResponseEntity<?>` | `Public`            |
| **Operation** | `requestPasswordReset(@RequestBody EmailAddressDto dto)` | 비밀번호 변경 요청 인증 메일 발송      | `ResponseEntity<?>` | `Public`            |

---
### Class Diagram #30: EmailRepository
Class Description: Email 엔티티의 영속성 관리를 위한 JPA Repository 인터페이스이다.

| 구분            | 이름                                | 설명                         | 타입                | 접근 제한자 (Visibility) |
|:--------------|:----------------------------------|:---------------------------|:------------------|:--------------------|
| **Operation** | `findByAddress(String email)`     | 이메일 주소로 Email 엔티티 조회       | `Optional<Email>` | `Public`            |
| **Operation** | `existsByAddress(String address)` | 이메일 주소로 Email 엔티티 존재 여부 확인 | `boolean`         | `Public`            |

---
### Class Diagram #31: EmailController
Class Description: 이메일 관련 API 요청을 처리하는 REST Controller이다.

| 구분            | 이름                                                       | 설명                    | 타입                  | 접근 제한자 (Visibility) |
|:--------------|:---------------------------------------------------------|:----------------------|:--------------------|:--------------------|
| **Attribute** | `userService`                                            | 사용자 관리 서비스            | `UserService`       | `Private`           |
| **Attribute** | `emailService`                                           | 이메일 관련 비즈니스 로직 서비스    | `EmailService`      | `Private`           |
| **Attribute** | `verifyService`                                          | 인증 관리 서비스             | `VerifyService`     | `Private`           |
| **Operation** | `checkDuplication(@RequestParam String address)`         | 이메일 중복 확인 엔드포인트       | `ResponseEntity<?>` | `Public`            |
| **Operation** | `getVerificationStatus(@RequestParam String address)`    | 이메일 인증 상태 조회 엔드포인트    | `ResponseEntity<?>` | `Public`            |
| **Operation** | `initEmail(@RequestBody EmailAddressDto dto)`            | 초기 이메일 인증 전송 엔드포인트    | `ResponseEntity<?>` | `Public`            |
| **Operation** | `requestPasswordReset(@RequestBody EmailAddressDto dto)` | 비밀번호 재설정 이메일 전송 엔드포인트 | `ResponseEntity<?>` | `Public`            |

---
### Class Diagram #32: EmailInfoDto
Class Description: 이메일의 인증 상태 정보를 담아 응답하는 Response 데이터 전송 클래스이다.

| 구분            | 이름               | 설명                    | 타입             | 접근 제한자 (Visibility) |
|:--------------|:-----------------|:----------------------|:---------------|:--------------------|
| **Attribute** | `emailId`        | 이메일 고유 ID             | `Long`         | `Private`           |
| **Attribute** | `emailAddress`   | 이메일 주소                | `String`       | `Private`           |
| **Attribute** | `verifyType`     | 인증 상태 타입              | `String`       | `Private`           |
| **Attribute** | `verifyExpireAt` | 인증 만료 시각              | `String`       | `Private`           |
| **Operation** | `builder()`      | EmailInfoDto 객체 빌더 생성 | `EmailInfoDto` | `Public`            |

---
### Class Diagram #33: EmailService
Class Description: 이메일 엔티티 관리, 중복 확인, 인증 상태 조회, 인증/비밀번호 재설정 메일 전송 등의 비즈니스 로직을 담당하는 서비스 클래스이다.

| 구분            | 이름                                                  | 설명                           | 타입                 | 접근 제한자 (Visibility) |
|:--------------|:----------------------------------------------------|:-----------------------------|:-------------------|:--------------------|
| **Attribute** | `mailSender`                                        | JavaMailSender 객체            | `JavaMailSender`   | `Private`           |
| **Attribute** | `emailRepository`                                   | Email 엔티티 저장소                | `EmailRepository`  | `Private`           |
| **Attribute** | `verifyService`                                     | 인증 관리 서비스                    | `VerifyService`    | `Private`           |
| **Attribute** | `userRepository`                                    | User 엔티티 저장소                 | `UserRepository`   | `Private`           |
| **Attribute** | `verifyRepository`                                  | Verify 엔티티 저장소               | `VerifyRepository` | `Private`           |
| **Attribute** | `baseUrl`                                           | BE 서버 URL(서버단 FE View로 연결)   | `String`           | `Private`           |
| **Operation** | `createEmail(String address, Verify verify)`        | Email 엔티티 생성 및 저장            | `Email`            | `Protected`         |
| **Operation** | `findEmailByAddress(String address)`                | 이메일 주소로 Email 엔티티 조회         | `Email`            | `Public`            |
| **Operation** | `existsEmailAddress(String address)`                | 이메일 주소 존재 여부 확인              | `boolean`          | `Public`            |
| **Operation** | `getVerificationStatus(String address)`             | 이메일 인증 상태 정보 조회              | `EmailInfoDto`     | `Public`            |
| **Operation** | `initEmail(EmailAddressDto dto)`                    | 초기 가입 인증 이메일 전송 및 인증 상태 업데이트 | `void`             | `Public`            |
| **Operation** | `requestPasswordReset(EmailAddressDto dto)`         | 비밀번호 초기화 요청 인증 이메일 전송        | `void`             | `Public`            |
| **Operation** | `sendVerificationEmail(Email email, String token)`  | 가입 인증 이메일 실제 전송 로직           | `void`             | `Protected`         |
| **Operation** | `sendPasswordResetEmail(Email email, String token)` | 비밀번호 재설정 이메일 실제 전송 로직        | `void`             | `Protected`         |


---

### 3.3.3. Verify
![verify.png](Class%20Diagram%20UML/verify.png)


### Class Diagram #34: PasswordResetConfirmDto
Class Description: 비밀번호 재설정을 위해 이메일과 새로운 비밀번호를 담는 Request 데이터 전송 클래스이다.

| 구분            | 이름            | 설명               | 타입       | 접근 제한자 (Visibility) |
|:--------------|:--------------|:-----------------|:---------|:--------------------|
| **Attribute** | `email`       | 사용자 이메일 (필수)     | `String` | `Private`           |
| **Attribute** | `newPassword` | 새로 설정할 비밀번호 (필수) | `String` | `Private`           |

---
### Class Diagram #35: VerifyApi
Class Description: 인증 및 보안 관련 API 엔드포인트를 정의하는 인터페이스이다. (Swagger 문서용 Tag/Operation 정의 포함)

| 구분            | 이름                                                                | 설명            | 타입                  | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------------|:--------------|:--------------------|:--------------------|
| **Operation** | `confirmChangePassword(@RequestBody PasswordResetConfirmDto dto)` | 새 비밀번호로 최종 변경 | `ResponseEntity<?>` | `Public`            |

---
### Class Diagram #36: VerifyRepository
Class Description: Verify 엔티티의 영속성 관리를 위한 JPA Repository 인터페이스이다.

| 구분            | 이름                                             | 설명                             | 타입                 | 접근 제한자 (Visibility) |
|:--------------|:-----------------------------------------------|:-------------------------------|:-------------------|:--------------------|
| **Operation** | `findByToken(String token)`                    | 토큰 문자열로 Verify 엔티티 조회          | `Optional<Verify>` | `Public`            |
| **Operation** | `findAllByExpireTimeBefore(LocalDateTime now)` | 현재 시간 이전에 만료된 Verify 엔티티 목록 조회 | `List<Verify>`     | `Public`            |
| **Operation** | `findByEmail_Address(String emailAddress)`     | 이메일 주소로 Verify 엔티티 조회          | `Optional<Verify>` | `Public`            |

---
### Class Diagram #37: VerifyController
Class Description: 비밀번호 재설정 관련 API 요청을 처리하는 REST Controller이다.

| 구분            | 이름                                                                | 설명                | 타입                  | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------------|:------------------|:--------------------|:--------------------|
| **Attribute** | `verifyService`                                                   | 인증 관리 서비스         | `VerifyService`     | `Private`           |
| **Operation** | `confirmChangePassword(@RequestBody PasswordResetConfirmDto dto)` | 새로운 비밀번호 반영 엔드포인트 | `ResponseEntity<?>` | `Public`            |

---
### Class Diagram #38: VerifyViewController
Class Description: 이메일 인증 링크를 통해 접근 시 인증 로직을 수행하고 결과를 HTML 뷰로 반환하는 Controller이다.

| 구분            | 이름                                                                   | 설명                           | 타입              | 접근 제한자 (Visibility) |
|:--------------|:---------------------------------------------------------------------|:-----------------------------|:----------------|:--------------------|
| **Attribute** | `verifyService`                                                      | 인증 관리 서비스                    | `VerifyService` | `Private`           |
| **Operation** | `emailVerification(@RequestParam String token, Model model)`         | 초기 회원가입 이메일 인증 처리 후 결과 뷰 반환  | `String`        | `Public`            |
| **Operation** | `passwordResetVerification(@RequestParam String token, Model model)` | 비밀번호 재설정 이메일 인증 처리 후 결과 뷰 반환 | `String`        | `Public`            |

---
### Class Diagram #39: VerifyService
Class Description: 인증 객체 관리, 토큰 유효성 검증, 만료 객체 정리, 이메일 인증 처리, 비밀번호 재설정 상태 관리 등 인증 관련 핵심 비즈니스 로직을 담당하는 서비스이다.

| 구분            | 이름                                             | 설명                                          | 타입                 | 접근 제한자 (Visibility) |
|:--------------|:-----------------------------------------------|:--------------------------------------------|:-------------------|:--------------------|
| **Attribute** | `verifyRepository`                             | Verify 엔티티 저장소                              | `VerifyRepository` | `Private`           |
| **Attribute** | `userRepository`                               | User 엔티티 저장소                                | `UserRepository`   | `Private`           |
| **Attribute** | `emailRepository`                              | Email 엔티티 저장소                               | `EmailRepository`  | `Private`           |
| **Attribute** | `passwordEncoder`                              | 비밀번호 인코더                                    | `PasswordEncoder`  | `Private`           |
| **Operation** | `createToken()`                                | UUID 기반 랜덤 토큰 문자열 생성                        | `String`           | `Public`            |
| **Operation** | `createVerify()`                               | 이메일 인증 상태로 설정된 Verify 객체 생성 및 저장            | `Verify`           | `Public`            |
| **Operation** | `validateToken(String token, VerifyType type)` | 토큰 유효성 및 타입 일치 여부 검증                        | `Verify`           | `Protected`         |
| **Operation** | `cleanExpiredVerify()`                         | 30분마다 만료된 인증 객체 정리 및 상태 변경                  | `void`             | `Public`            |
| **Operation** | `emailVerification(String token)`              | 가입 인증 완료 처리 및 상태를 VERIFY로 변경                | `void`             | `Public`            |
| **Operation** | `passwordResetRequestStatus(Email email)`      | 비밀번호 초기화 요청 상태로 변경 (REQUEST_PASSWORD_RESET) | `void`             | `Public`            |
| **Operation** | `passwordResetVerification(String token)`      | 인증 후 비밀번호 변경 가능 상태로 전환 (CHANGING_PASSWORD)  | `void`             | `Public`            |
| **Operation** | `updatePassword(PasswordResetConfirmDto dto)`  | 새 비밀번호를 반영하고 인증 상태를 VERIFY로 원상복구            | `void`             | `Public`            |

---

### 3.3.4. Diary
![diary.png](Class%20Diagram%20UML/diary.png)

### Class Diagram #40: DiaryCreateReqDto
Class Description: 감정 일기 생성 요청에 필요한 데이터를 담는 Request 데이터 전송 클래스이다.

| 구분            | 이름        | 설명                         | 타입             | 접근 제한자 (Visibility) |
|:--------------|:----------|:---------------------------|:---------------|:--------------------|
| **Attribute** | `emotion` | 감정 (`HAPPINESS` 등, 필수)     | `Emotion`      | `Private`           |
| **Attribute** | `factors` | 감정 요인 태그 목록 (최소 1개, 필수)    | `List<Factor>` | `Private`           |
| **Attribute** | `content` | 일기 내용 (15자 이상 300자 이하, 필수) | `String`       | `Private`           |
| **Attribute** | `date`    | 일기 작성 날짜 (필수)              | `LocalDate`    | `Private`           |

---
### Class Diagram #41: DiaryUpdateReqDto
Class Description: 감정 일기 수정 요청에 필요한 데이터를 담는 Request 데이터 전송 클래스이다.

| 구분            | 이름        | 설명                     | 타입          | 접근 제한자 (Visibility) |
|:--------------|:----------|:-----------------------|:------------|:--------------------|
| **Attribute** | `date`    | 수정 대상 날짜 (필수)          | `LocalDate` | `Private`           |
| **Attribute** | `content` | 일기 내용 (15자 이상 300자 이하) | `String`    | `Private`           |

---
### Class Diagram #42: DiaryResDto
Class Description: 일기 조회 및 생성/수정 성공 시 응답하는 Response 데이터 전송 클래스이다.

| 구분            | 이름            | 설명                        | 타입             | 접근 제한자 (Visibility) |
|:--------------|:--------------|:--------------------------|:---------------|:--------------------|
| **Attribute** | `date`        | 일기 작성 날짜                  | `LocalDate`    | `Private`           |
| **Attribute** | `emotion`     | 기록된 감정                    | `Emotion`      | `Private`           |
| **Attribute** | `color`       | 감정에 따른 별 색상               | `Color`        | `Private`           |
| **Attribute** | `factors`     | 감정 요인 태그 목록               | `List<Factor>` | `Private`           |
| **Attribute** | `content`     | 일기 내용                     | `String`       | `Private`           |
| **Operation** | `of(Diary d)` | Diary 엔티티를 데이터 전송 클래스로 변환 | `DiaryResDto`  | `Public`            |

---
### Class Diagram #43: StarMonthlyResDto
Class Description: 월별 별 목록 조회 시 응답하는 Response 데이터 전송 클래스의 요소이다.

| 구분            | 이름      | 설명        | 타입          | 접근 제한자 (Visibility) |
|:--------------|:--------|:----------|:------------|:--------------------|
| **Attribute** | `date`  | 별이 생성된 날짜 | `LocalDate` | `Private`           |
| **Attribute** | `color` | 별의 색상     | `Color`     | `Private`           |

---
### Class Diagram #44: DiaryApi
Class Description: 감정 일기 관련 API 엔드포인트를 정의하는 인터페이스이다. (Swagger 문서용 Tag/Operation 정의 포함)

| 구분            | 이름                                                                                                                 | 설명              | 타입                                        | 접근 제한자 (Visibility) |
|:--------------|:-------------------------------------------------------------------------------------------------------------------|:----------------|:------------------------------------------|:--------------------|
| **Operation** | `createDiary(@AuthenticationPrincipal UserDetails principal, @Valid @RequestBody DiaryCreateReqDto req)`           | 감정 일기 생성 및 별 생성 | `ResponseEntity<?>`                       | `Public`            |
| **Operation** | `updateDiary(@AuthenticationPrincipal UserDetails principal, @Valid @RequestBody DiaryUpdateReqDto req)`           | 일기 내용 수정        | `ResponseEntity<?>`                       | `Public`            |
| **Operation** | `getDiary(@AuthenticationPrincipal UserDetails principal, @PathVariable LocalDate date)`                           | 특정 날짜 일기 조회     | `ResponseEntity<?>`                       | `Public`            |
| **Operation** | `getMonthlyStars(@AuthenticationPrincipal UserDetails principal, @RequestParam int year, @RequestParam int month)` | 특정 월의 별 목록 조회   | `ResponseEntity<List<StarMonthlyResDto>>` | `Public`            |
| **Operation** | `removeDiary(@AuthenticationPrincipal UserDetails principal, @PathVariable("diaryId") Long diaryId)`               | (개발용) 감정 일기 삭제  | `ResponseEntity<?>`                       | `Public`            |

---
### Class Diagram #45: DiaryRepository
Class Description: Diary 엔티티의 영속성 관리를 위한 JPA Repository 인터페이스이다.

| 구분            | 이름                                                                                                | 설명                                      | 타입                | 접근 제한자 (Visibility) |
|:--------------|:--------------------------------------------------------------------------------------------------|:----------------------------------------|:------------------|:--------------------|
| **Operation** | `existsByUser_IdAndCreateAt(Long userId, LocalDate date)`                                         | 사용자 ID와 날짜로 일기 존재 여부 확인                 | `boolean`         | `Public`            |
| **Operation** | `findByUser_IdAndCreateAt(Long userId, LocalDate date)`                                           | 사용자 ID와 날짜로 일기 조회                       | `Optional<Diary>` | `Public`            |
| **Operation** | `findAllByUser_IdAndCreateAtBetweenOrderByCreateAtAsc(Long userId, LocalDate from, LocalDate to)` | 사용자 ID, 시작일, 종료일로 월별 일기 목록 조회 (날짜 오름차순) | `List<Diary>`     | `Public`            |
| **Operation** | `findByIdAndUser_Id(Long diaryId, Long userId)`                                                   | 일기 ID와 사용자 ID로 일기 조회                    | `Optional<Diary>` | `Public`            |

---
### Class Diagram #46: DiaryService
Class Description: 감정 일기(Diary) 생성, 수정, 조회 및 월별 별 조회 등 핵심 비즈니스 로직을 담당하는 서비스이다.

| 구분            | 이름                                           | 설명                                | 타입                        | 접근 제한자 (Visibility) |
|:--------------|:---------------------------------------------|:----------------------------------|:--------------------------|:--------------------|
| **Attribute** | `diaryRepository`                            | Diary 엔티티 저장소                     | `DiaryRepository`         | `Private`           |
| **Attribute** | `userRepository`                             | User 엔티티 저장소                      | `UserRepository`          | `Private`           |
| **Attribute** | `starRepository`                             | Star 엔티티 저장소                      | `StarRepository`          | `Private`           |
| **Attribute** | `em`                                         | 엔티티 매니저 (JPA)                     | `EntityManager`           | `Private`           |
| **Operation** | `create(Long userId, DiaryCreateReqDto req)` | 새로운 일기 생성 및 연관된 Star 엔티티 생성       | `DiaryResDto`             | `Public`            |
| **Operation** | `update(Long userId, DiaryUpdateReqDto req)` | 특정 날짜의 일기 내용 수정                   | `DiaryResDto`             | `Public`            |
| **Operation** | `getByDate(Long userId, LocalDate date)`     | 특정 날짜의 일기 조회                      | `DiaryResDto`             | `Public`            |
| **Operation** | `getMonthlyStars(Long userId, YearMonth ym)` | 특정 월에 작성된 일기 기반으로 별(날짜, 색상) 목록 조회 | `List<StarMonthlyResDto>` | `Public`            |
| **Operation** | `delete(Long userId, Long diaryId)`          | (개발용) 일기 삭제                       | `void`                    | `Public`            |
| **Operation** | `safeFactors(List<Factor> in)`               | Factor 목록을 안전하게 복사/초기화 (널 방지)     | `List<Factor>`            | `Private`           |

---
### Class Diagram #47: DiaryController
Class Description: 감정 일기 관련 API 요청을 받는 REST Controller이다.

| 구분            | 이름                                                                                                                 | 설명                       | 타입                                        | 접근 제한자 (Visibility) |
|:--------------|:-------------------------------------------------------------------------------------------------------------------|:-------------------------|:------------------------------------------|:--------------------|
| **Attribute** | `diaryService`                                                                                                     | 일기 관련 서비스                | `DiaryService`                            | `Private`           |
| **Attribute** | `userRepository`                                                                                                   | 사용자 엔티티 저장소              | `UserRepository`                          | `Private`           |
| **Operation** | `createDiary(@AuthenticationPrincipal UserDetails principal, @Valid @RequestBody DiaryCreateReqDto req)`           | 일기 생성 엔드포인트              | `ResponseEntity<DiaryResDto>`             | `Public`            |
| **Operation** | `updateDiary(@AuthenticationPrincipal UserDetails principal, @Valid @RequestBody DiaryUpdateReqDto req)`           | 일기 수정 엔드포인트              | `ResponseEntity<DiaryResDto>`             | `Public`            |
| **Operation** | `getDiary(@AuthenticationPrincipal UserDetails principal, @PathVariable LocalDate date)`                           | 특정 날짜 일기 조회 엔드포인트        | `ResponseEntity<DiaryResDto>`             | `Public`            |
| **Operation** | `getMonthlyStars(@AuthenticationPrincipal UserDetails principal, @RequestParam int year, @RequestParam int month)` | 월별 별 목록 조회 엔드포인트         | `ResponseEntity<List<StarMonthlyResDto>>` | `Public`            |
| **Operation** | `resolveUserId(UserDetails principal)`                                                                             | UserDetails에서 사용자 ID를 조회 | `Long`                                    | `Private`           |
| **Operation** | `removeDiary(@AuthenticationPrincipal UserDetails principal, @PathVariable("diaryId") Long diaryId)`               | (개발용) 일기 삭제 엔드포인트        | `ResponseEntity<Object>`                  | `Public`            |

---

### 3.3.5. Star
![star.png](Class%20Diagram%20UML/star.png)

### Class Diagram #48: DiaryToStarReqDto
Class Description: 일기 날짜를 통해 별을 조회하기 위한 요청 데이터 전송 클래스이다.

| 구분            | 이름     | 설명    | 타입       | 접근 제한자 (Visibility) |
|:--------------|:-------|:------|:---------|:--------------------|
| **Attribute** | `date` | 일기 날짜 | `String` | `Private`           |

---
### Class Diagram #49: StarPositionDto
Class Description: 별의 새로운 위치 좌표를 담는 요청 데이터 전송 클래스이다.

| 구분            | 이름       | 설명      | 타입       | 접근 제한자 (Visibility) |
|:--------------|:---------|:--------|:---------|:--------------------|
| **Attribute** | `starId` | 별 고유 ID | `Long`   | `Private`           |
| **Attribute** | `x`      | X 좌표    | `Double` | `Private`           |
| **Attribute** | `y`      | Y 좌표    | `Double` | `Private`           |

---
### Class Diagram #50: StarInfoDto
Class Description: 별 상세 조회 시 별과 연관 관계의 ID를 담아 응답하는 응답 데이터 전송 클래스이다.

| 구분            | 이름          | 설명                   | 타입            | 접근 제한자 (Visibility) |
|:--------------|:------------|:---------------------|:--------------|:--------------------|
| **Attribute** | `starId`    | 별 고유 ID              | `Long`        | `Private`           |
| **Attribute** | `userId`    | 사용자 고유 ID            | `Long`        | `Private`           |
| **Attribute** | `diaryId`   | 연관된 일기 고유 ID         | `Long`        | `Private`           |
| **Operation** | `builder()` | StarInfoDto 객체 빌더 생성 | `StarInfoDto` | `Public`            |

---
### Class Diagram #51: StarryNightStarDto
Class Description: 밤하늘 별 조회 시 별의 기본 정보를 담아 응답하는 응답 데이터 전송 클래스의 요소이다.

| 구분            | 이름          | 설명                          | 타입                   | 접근 제한자 (Visibility) |
|:--------------|:------------|:----------------------------|:---------------------|:--------------------|
| **Attribute** | `starId`    | 별 고유 ID                     | `Long`               | `Private`           |
| **Attribute** | `userId`    | 사용자 고유 ID                   | `Long`               | `Private`           |
| **Attribute** | `color`     | 별 색상                        | `String`             | `Private`           |
| **Attribute** | `date`      | 별이 생성된 날짜                   | `String`             | `Private`           |
| **Attribute** | `x`         | 별의 X 좌표                     | `Double`             | `Private`           |
| **Attribute** | `y`         | 별의 Y 좌표                     | `Double`             | `Private`           |
| **Operation** | `builder()` | StarryNightStarDto 객체 빌더 생성 | `StarryNightStarDto` | `Public`            |

---
### Class Diagram #52: StarArchiveDetailDto
Class Description: 별 아카이브 상세 조회에 사용되는 응답 데이터 전송 클래스이다.

| 구분            | 이름          | 설명                            | 타입                     | 접근 제한자 (Visibility) |
|:--------------|:------------|:------------------------------|:-----------------------|:--------------------|
| **Attribute** | `starId`    | 별 고유 ID                       | `Long`                 | `Private`           |
| **Attribute** | `x`         | X 좌표                          | `Double`               | `Private`           |
| **Attribute** | `y`         | Y 좌표                          | `Double`               | `Private`           |
| **Attribute** | `color`     | 별 색상                          | `String`               | `Private`           |
| **Attribute** | `date`      | 별 생성 날짜                       | `LocalDate`            | `Private`           |
| **Operation** | `builder()` | StarArchiveDetailDto 객체 빌더 생성 | `StarArchiveDetailDto` | `Public`            |

---
### Class Diagram #53: StarArchiveDto
Class Description: 별 아카이브 목록 조회에 사용되는 Response 데이터 전송 클래스이다.

| 구분            | 이름          | 설명                      | 타입               | 접근 제한자 (Visibility) |
|:--------------|:------------|:------------------------|:-----------------|:--------------------|
| **Attribute** | `starId`    | 별 고유 ID                 | `Long`           | `Private`           |
| **Attribute** | `x`         | X 좌표                    | `Double`         | `Private`           |
| **Attribute** | `y`         | Y 좌표                    | `Double`         | `Private`           |
| **Attribute** | `color`     | 별 색상                    | `String`         | `Private`           |
| **Operation** | `builder()` | StarArchiveDto 객체 빌더 생성 | `StarArchiveDto` | `Public`            |

---
### Class Diagram #54: StarApi
Class Description: 별 관련 API 엔드포인트를 정의하는 인터페이스이다. (Swagger 문서용 Tag/Operation 정의 포함)

| 구분            | 이름                                                                                                                      | 설명                               | 타입                  | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------------------------------------------------------------------|:---------------------------------|:--------------------|:--------------------|
| **Operation** | `getStar(@PathVariable Long id)`                                                                                        | 별과 연관관계 ID 조회                    | `ResponseEntity<?>` | `Public`            |
| **Operation** | `getStarryNightStar(@AuthenticationPrincipal UserDetails userDetails, @RequestParam int year, @RequestParam int month)` | 밤하늘 별 조회 (2달 간격, 별자리에 소속되지 않은 별) | `ResponseEntity<?>` | `Public`            |
| **Operation** | `repositionStar(@PathVariable Long id, @RequestBody StarPositionDto dto)`                                               | 별 위치 최신화                         | `ResponseEntity<?>` | `Public`            |

---
### Class Diagram #55: StarRepository
Class Description: Star 엔티티의 영속성 관리를 위한 JPA Repository 인터페이스이다.

| 구분            | 이름                                                                                                            | 설명                            | 타입           | 접근 제한자 (Visibility) |
|:--------------|:--------------------------------------------------------------------------------------------------------------|:------------------------------|:-------------|:--------------------|
| **Operation** | `existsByUserAndDiary(User user, Diary diary)`                                                                | 사용자 및 일기로 별 존재 여부 확인          | `boolean`    | `Public`            |
| **Operation** | `findByConstellation(Constellation constellation)`                                                            | 별자리에 속한 별 목록 조회               | `List<Star>` | `Public`            |
| **Operation** | `findByUserAndDiary_CreateAtBetweenAndConstellationIsNull(User user, LocalDate startDate, LocalDate endDate)` | 사용자, 기간, 별자리에 소속되지 않은 별 목록 조회 | `List<Star>` | `Public`            |
| **Operation** | `countByConstellationAndColor(Constellation constellation, Color color)`                                      | 별자리 내 특정 색상 별 개수 카운트          | `Integer`    | `Public`            |

---
### Class Diagram #56: StarController
Class Description: 별 관련 API 요청을 받아 StarService로 전달하는 REST Controller이다.

| 구분            | 이름                                                                                                                      | 설명             | 타입                  | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------------------------------------------------------------------|:---------------|:--------------------|:--------------------|
| **Attribute** | `starService`                                                                                                           | 별 관리 서비스       | `StarService`       | `Private`           |
| **Operation** | `getStar(@PathVariable Long id)`                                                                                        | 별 상세조회 엔드포인트   | `ResponseEntity<?>` | `Public`            |
| **Operation** | `getStarryNightStar(@AuthenticationPrincipal UserDetails userDetails, @RequestParam int year, @RequestParam int month)` | 밤하늘 별 조회 엔드포인트 | `ResponseEntity<?>` | `Public`            |
| **Operation** | `repositionStar(@PathVariable Long id, @RequestBody StarPositionDto dto)`                                               | 별 위치 최신화 엔드포인트 | `ResponseEntity<?>` | `Public`            |

---
### Class Diagram #57: StarService
Class Description: 별 정보 조회, 밤하늘 별 조회, 별 위치 최신화 등 별 관련 비즈니스 로직을 담당하는 서비스이다.

| 구분            | 이름                                                                 | 설명                                  | 타입                         | 접근 제한자 (Visibility) |
|:--------------|:-------------------------------------------------------------------|:------------------------------------|:---------------------------|:--------------------|
| **Attribute** | `userRepository`                                                   | 사용자 엔티티 저장소                         | `UserRepository`           | `Private`           |
| **Attribute** | `starRepository`                                                   | 별 엔티티 저장소                           | `StarRepository`           | `Private`           |
| **Operation** | `getStar(Long id)`                                                 | 별 상세 조회 (ID, 일기 ID, 사용자 ID 반환)      | `StarInfoDto`              | `Public`            |
| **Operation** | `getStarryNightStar(UserDetails userDetails, int year, int month)` | 밤하늘 별 목록 조회 (별자리에 소속되지 않은 별, 2달 단위) | `List<StarryNightStarDto>` | `Public`            |
| **Operation** | `repositionStar(Long id, StarPositionDto dto)`                     | 별 위치 업데이트 (좌표 범위 검증 포함)             | `void`                     | `Public`            |

---

### 3.3.6. Constellation
![constellation.png](Class%20Diagram%20UML/constellation.png)

---

### Class Diagram #58: CreateConstellationDto
Class Description: 별자리 생성 요청 시 필요한 정보(이름, 설명, 구성 별 및 연결선)를 담는 Request 데이터 전송 클래스이다.

| 구분            | 이름            | 설명            | 타입                      | 접근 제한자 (Visibility) |
|:--------------|:--------------|:--------------|:------------------------|:--------------------|
| **Attribute** | `name`        | 별자리 이름        | `String`                | `Private`           |
| **Attribute** | `description` | 별자리 설명        | `String`                | `Private`           |
| **Attribute** | `stars`       | 별자리를 구성할 별 목록 | `List<StarPositionDto>` | `Private`           |
| **Attribute** | `connections` | 별자리 연결선 목록    | `List<ConnectionDto>`   | `Private`           |

---
### Class Diagram #59: ConstellationPositionDto
Class Description: 별자리 위치 최신화 요청 시 필요한 X, Y 좌표를 담는 Request 데이터 전송 클래스이다.

| 구분            | 이름  | 설명        | 타입       | 접근 제한자 (Visibility) |
|:--------------|:----|:----------|:---------|:--------------------|
| **Attribute** | `x` | 별자리의 X 좌표 | `Double` | `Private`           |
| **Attribute** | `y` | 별자리의 Y 좌표 | `Double` | `Private`           |

---
### Class Diagram #60: UpdateConstellationInfo
Class Description: 별자리의 이름 및 설명을 수정할 때 사용되는 Request 데이터 전송 클래스이다.

| 구분            | 이름            | 설명         | 타입       | 접근 제한자 (Visibility) |
|:--------------|:--------------|:-----------|:---------|:--------------------|
| **Attribute** | `name`        | 수정할 별자리 이름 | `String` | `Private`           |
| **Attribute** | `description` | 수정할 별자리 설명 | `String` | `Private`           |

---
### Class Diagram #61: ConstellationApi
Class Description: 별자리 관련 API 엔드포인트를 정의하는 인터페이스이다. (Swagger 문서용 Tag/Operation 정의 포함)

| 구분            | 이름                                                                                                                               | 설명                     | 타입                  | 접근 제한자 (Visibility) |
|:--------------|:---------------------------------------------------------------------------------------------------------------------------------|:-----------------------|:--------------------|:--------------------|
| **Operation** | `getStarryNightConstellation(@AuthenticationPrincipal UserDetails userDetails, @RequestParam int year, @RequestParam int month)` | 밤하늘 별자리 조회 (2달 간격)     | `ResponseEntity<?>` | `Public`            |
| **Operation** | `createConstellation(@AuthenticationPrincipal UserDetails userDetails, @RequestBody CreateConstellationDto dto)`                 | 별자리 생성                 | `ResponseEntity<?>` | `Public`            |
| **Operation** | `repositionConstellation(@PathVariable Long id, @RequestBody ConstellationPositionDto dto)`                                      | 별자리 위치 최신화             | `ResponseEntity<?>` | `Public`            |
| **Operation** | `getArchiveList(@AuthenticationPrincipal UserDetails userDetails)`                                                               | 사용자의 모든 별자리 아카이브 목록 조회 | `ResponseEntity<?>` | `Public`            |
| **Operation** | `getArchiveDetail(@PathVariable Long id)`                                                                                        | 특정 별자리 아카이브 상세 조회      | `ResponseEntity<?>` | `Public`            |
| **Operation** | `updateConstellationInfo(@PathVariable Long id, @RequestBody UpdateConstellationInfo dto)`                                       | 별자리 이름 및 설명 수정         | `ResponseEntity<?>` | `Public`            |
| **Operation** | `changeRepresentativeConstellation(@PathVariable Long id, @AuthenticationPrincipal UserDetails userDetails)`                     | 대표 별자리 설정/변경           | `ResponseEntity<?>` | `Public`            |

---
### Class Diagram #62: ConstellationRepository
Class Description: Constellation 엔티티의 영속성 관리를 위한 JPA Repository 인터페이스이다.

| 구분            | 이름                                                                                  | 설명                                         | 타입                        | 접근 제한자 (Visibility) |
|:--------------|:------------------------------------------------------------------------------------|:-------------------------------------------|:--------------------------|:--------------------|
| **Operation** | `findByUserAndBelongDateBetween(User user, LocalDate startDate, LocalDate endDate)` | 사용자별, 기간별 별자리 목록 조회                        | `List<Constellation>`     | `Public`            |
| **Operation** | `findByUser(User user)`                                                             | 사용자별 모든 별자리 목록 조회                          | `List<Constellation>`     | `Public`            |
| **Operation** | `findByUserAndIsRepresentative(User user, boolean isRepresentative)`                | 사용자별 대표 별자리 조회                             | `Optional<Constellation>` | `Public`            |

---
### Class Diagram #63: StarryNightConstellationDto
Class Description: 밤하늘 별자리 조회 시 반환되는 별자리 정보를 담는 Response 데이터 전송 클래스이다.

| 구분            | 이름                | 설명                                   | 타입                               | 접근 제한자 (Visibility) |
|:--------------|:------------------|:-------------------------------------|:---------------------------------|:--------------------|
| **Attribute** | `constellationId` | 별자리 고유 ID                            | `Long`                           | `Private`           |
| **Attribute** | `userId`          | 사용자 고유 ID                            | `Long`                           | `Private`           |
| **Attribute** | `x`               | 별자리 X 좌표                             | `Double`                         | `Private`           |
| **Attribute** | `y`               | 별자리 Y 좌표                             | `Double`                         | `Private`           |
| **Attribute** | `belongDate`      | 별자리가 소속된 월의 날짜                       | `LocalDate`                      | `Private`           |
| **Attribute** | `stars`           | 구성 별 정보 리스트                          | `List<StarryNightStarDto>`       | `Private`           |
| **Attribute** | `connections`     | 연결선 정보 리스트                           | `List<StarryNightConnectionDto>` | `Private`           |
| **Operation** | `builder()`       | StarryNightConstellationDto 객체 빌더 생성 | `StarryNightConstellationDto`    | `Public`            |

---
### Class Diagram #64: ArchiveDto
Class Description: 별자리 아카이브 목록 조회 시 반환되는 별자리 요약 정보를 담는 Response 데이터 전송 클래스이다.

| 구분            | 이름                 | 설명                  | 타입                     | 접근 제한자 (Visibility) |
|:--------------|:-------------------|:--------------------|:-----------------------|:--------------------|
| **Attribute** | `constellationId`  | 별자리 고유 ID           | `Long`                 | `Private`           |
| **Attribute** | `name`             | 별자리 이름              | `String`               | `Private`           |
| **Attribute** | `description`      | 별자리 설명              | `String`               | `Private`           |
| **Attribute** | `date`             | 별자리 생성일             | `LocalDate`            | `Private`           |
| **Attribute** | `isRepresentative` | 대표 별자리 여부           | `Boolean`              | `Private`           |
| **Attribute** | `stars`            | 구성 별 정보 리스트         | `List<StarArchiveDto>` | `Private`           |
| **Attribute** | `connections`      | 연결선 정보 리스트          | `List<ConnectionDto>`  | `Private`           |
| **Operation** | `builder()`        | ArchiveDto 객체 빌더 생성 | `ArchiveDto`           | `Public`            |

---
### Class Diagram #65: ArchiveDetailDto
Class Description: 별자리 아카이브 상세 조회 시 반환되는 별자리 정보와 감정별 별 개수를 담는 Response 데이터 전송 클래스이다.

| 구분            | 이름                 | 설명                        | 타입                           | 접근 제한자 (Visibility) |
|:--------------|:-------------------|:--------------------------|:-----------------------------|:--------------------|
| **Attribute** | `constellationId`  | 별자리 고유 ID                 | `Long`                       | `Private`           |
| **Attribute** | `name`             | 별자리 이름                    | `String`                     | `Private`           |
| **Attribute** | `description`      | 별자리 설명                    | `String`                     | `Private`           |
| **Attribute** | `date`             | 별자리 생성일                   | `LocalDate`                  | `Private`           |
| **Attribute** | `isRepresentative` | 대표 별자리 여부                 | `Boolean`                    | `Private`           |
| **Attribute** | `stars`            | 구성 별 상세 정보 리스트            | `List<StarArchiveDetailDto>` | `Private`           |
| **Attribute** | `connections`      | 연결선 정보 리스트                | `List<ConnectionDto>`        | `Private`           |
| **Attribute** | `happynessCount`   | 행복 감정 별 개수                | `Integer`                    | `Private`           |
| **Attribute** | `funnyCount`       | 재미 감정 별 개수                | `Integer`                    | `Private`           |
| **Attribute** | `neutralCount`     | 중립 감정 별 개수                | `Integer`                    | `Private`           |
| **Attribute** | `surprisingCount`  | 놀람 감정 별 개수                | `Integer`                    | `Private`           |
| **Attribute** | `angerCount`       | 분노 감정 별 개수                | `Integer`                    | `Private`           |
| **Attribute** | `sadnessCount`     | 슬픔 감정 별 개수                | `Integer`                    | `Private`           |
| **Operation** | `builder()`        | ArchiveDetailDto 객체 빌더 생성 | `ArchiveDetailDto`           | `Public`            |

---
### Class Diagram #66: ConstellationController
Class Description: 별자리 관련 API 요청을 받아 ConstellationService로 전달하는 REST Controller이다.

| 구분            | 이름                                                                                                                               | 설명                   | 타입                     | 접근 제한자 (Visibility) |
|:--------------|:---------------------------------------------------------------------------------------------------------------------------------|:---------------------|:-----------------------|:--------------------|
| **Attribute** | `constellationService`                                                                                                           | 별자리 관리 서비스           | `ConstellationService` | `Private`           |
| **Operation** | `getStarryNightConstellation(@AuthenticationPrincipal UserDetails userDetails, @RequestParam int year, @RequestParam int month)` | 밤하늘 별자리 조회 엔드포인트     | `ResponseEntity<?>`    | `Public`            |
| **Operation** | `createConstellation(@AuthenticationPrincipal UserDetails userDetails, @RequestBody CreateConstellationDto dto)`                 | 별자리 생성 엔드포인트         | `ResponseEntity<?>`    | `Public`            |
| **Operation** | `repositionConstellation(@PathVariable Long id, @RequestBody ConstellationPositionDto dto)`                                      | 별자리 위치 최신화 엔드포인트     | `ResponseEntity<?>`    | `Public`            |
| **Operation** | `getArchiveList(@AuthenticationPrincipal UserDetails userDetails)`                                                               | 별자리 아카이브 목록 조회 엔드포인트 | `ResponseEntity<?>`    | `Public`            |
| **Operation** | `getArchiveDetail(@PathVariable Long id)`                                                                                        | 별자리 아카이브 상세조회 엔드포인트  | `ResponseEntity<?>`    | `Public`            |
| **Operation** | `updateConstellationInfo(@PathVariable Long id, @RequestBody UpdateConstellationInfo dto)`                                       | 별자리 이름 및 설명 수정 엔드포인트 | `ResponseEntity<?>`    | `Public`            |
| **Operation** | `changeRepresentativeConstellation(@PathVariable Long id, @AuthenticationPrincipal UserDetails userDetails)`                     | 대표 별자리 설정/변경 엔드포인트   | `ResponseEntity<?>`    | `Public`            |

---
### Class Diagram #67: ConstellationService
Class Description: 별자리 생성, 조회, 위치 최신화, 아카이브 관리 등 별자리 관련 핵심 비즈니스 로직을 담당하는 서비스이다.

| 구분            | 이름                                                                          | 설명                           | 타입                                  | 접근 제한자 (Visibility) |
|:--------------|:----------------------------------------------------------------------------|:-----------------------------|:------------------------------------|:--------------------|
| **Attribute** | `constellationRepository`                                                   | Constellation 엔티티 저장소        | `ConstellationRepository`           | `Private`           |
| **Attribute** | `connectionRepository`                                                      | Connection 엔티티 저장소           | `ConnectionRepository`              | `Private`           |
| **Attribute** | `starRepository`                                                            | Star 엔티티 저장소                 | `StarRepository`                    | `Private`           |
| **Attribute** | `userRepository`                                                            | User 엔티티 저장소                 | `UserRepository`                    | `Private`           |
| **Operation** | `createConstellation(UserDetails userDetails, CreateConstellationDto dto)`  | 별자리 생성 및 구성 별, 연결선 저장        | `void`                              | `Public`            |
| **Operation** | `getStarryNightConstellation(UserDetails userDetails, int year, int month)` | 밤하늘 별자리 조회 (2달 간격)           | `List<StarryNightConstellationDto>` | `Public`            |
| **Operation** | `repositionConstellation(Long id, ConstellationPositionDto dto)`            | 별자리 위치 최신화 및 좌표 범위 검증        | `void`                              | `Public`            |
| **Operation** | `getArchiveList(UserDetails userDetails)`                                   | 사용자의 모든 별자리 아카이브 목록 조회       | `List<ArchiveDto>`                  | `Public`            |
| **Operation** | `getArchiveDetail(Long id)`                                                 | 별자리 아카이브 상세 조회 및 감정별 별 개수 집계 | `ArchiveDetailDto`                  | `Public`            |
| **Operation** | `updateConstellationInfo(Long id, UpdateConstellationInfo dto)`             | 별자리 이름 및 설명 수정               | `void`                              | `Public`            |
| **Operation** | `changeRepresentativeConstellation(Long id, UserDetails userDetails)`       | 대표 별자리 설정/변경                 | `void`                              | `Public`            |


---

### 3.3.7. Connection
![connection.png](Class%20Diagram%20UML/connection.png)

---

### Class Diagram #68: Connection
Class Description: 별자리 내에서 두 별을 연결하는 선(관계)을 나타내는 Entity이다.

| 구분            | 이름              | 설명                  | 타입              | 접근 제한자 (Visibility) |
|:--------------|:----------------|:--------------------|:----------------|:--------------------|
| **Attribute** | `id`            | 연결선의 고유 식별자         | `Long`          | `Private`           |
| **Attribute** | `constellation` | 연결선이 속한 별자리 (필수)    | `Constellation` | `Private`           |
| **Attribute** | `start`         | 연결선의 시작 별 (필수)      | `Star`          | `Private`           |
| **Attribute** | `end`           | 연결선의 끝 별 (필수)       | `Star`          | `Private`           |
| **Operation** | `builder()`     | Connection 객체 빌더 생성 | `Connection`    | `Public`            |

---
### Class Diagram #69: ConnectionRepository
Class Description: Connection 엔티티의 영속성 관리를 위한 JPA Repository 인터페이스이다.

| 구분            | 이름                                                 | 설명                      | 타입                 | 접근 제한자 (Visibility) |
|:--------------|:---------------------------------------------------|:------------------------|:-------------------|:--------------------|
| **Operation** | `findByConstellation(Constellation constellation)` | 특정 별자리에 속한 모든 연결선 목록 조회 | `List<Connection>` | `Public`            |

---
### Class Diagram #70: ConnectionDto
Class Description: 별자리 생성 시 요청 본문에서 연결선의 시작/끝 별 ID를 담는 요청 데이터 전송 클래스이다.

| 구분            | 이름            | 설명                     | 타입              | 접근 제한자 (Visibility) |
|:--------------|:--------------|:-----------------------|:----------------|:--------------------|
| **Attribute** | `startStarId` | 시작 별의 ID               | `Long`          | `Private`           |
| **Attribute** | `endStarId`   | 끝 별의 ID                | `Long`          | `Private`           |
| **Operation** | `builder()`   | ConnectionDto 객체 빌더 생성 | `ConnectionDto` | `Public`            |

---
### Class Diagram #71: StarryNightConnectionDto
Class Description: 밤하늘 별자리 조회 시 연결선 정보를 담아 응답하는 응답 데이터 전송 클래스의 요소이다.

| 구분            | 이름             | 설명                                | 타입                         | 접근 제한자 (Visibility) |
|:--------------|:---------------|:----------------------------------|:---------------------------|:--------------------|
| **Attribute** | `connectionId` | 연결선 고유 ID                         | `Long`                     | `Private`           |
| **Attribute** | `startStarId`  | 시작 별의 ID                          | `Long`                     | `Private`           |
| **Attribute** | `endStarId`    | 끝 별의 ID                           | `Long`                     | `Private`           |
| **Operation** | `builder()`    | StarryNightConnectionDto 객체 빌더 생성 | `StarryNightConnectionDto` | `Public`            |


---

### 3.3.8. External Services : S3
![s3.png](Class%20Diagram%20UML/s3.png)

---

### Class Diagram #72: S3tempResDto
Class Description: 이미지 업로드를 위해 발급된 임시 URL과 해당 파일 키를 담아 응답하는 응답 데이터 전송 클래스이다.

| 구분            | 이름                        | 설명                          | 타입             | 접근 제한자 (Visibility) |
|:--------------|:--------------------------|:----------------------------|:---------------|:--------------------|
| **Attribute** | `presignedUrl`            | S3에 직접 업로드할 수 있는 사전 서명된 URL | `String`       | `Private`           |
| **Attribute** | `tempKey`                 | 업로드에 사용될 임시 파일 키            | `String`       | `Private`           |
| **Operation** | `of(URL url, String key)` | URL과 키를 데이터 전송 클래스로 변환      | `S3tempResDto` | `Public`            |

---
### Class Diagram #73: S3uploadResDto
Class Description: S3 업로드 완료 후 최종적으로 저장된 이미지 URL을 담아 응답하는 응답 데이터 전송 클래스이다.

| 구분            | 이름               | 설명                  | 타입               | 접근 제한자 (Visibility) |
|:--------------|:-----------------|:--------------------|:-----------------|:--------------------|
| **Attribute** | `imageUrl`       | 최종적으로 저장된 이미지의 URL  | `String`         | `Private`           |
| **Operation** | `of(String url)` | URL을 데이터 전송 클래스로 변환 | `S3uploadResDto` | `Public`            |

---
### Class Diagram #74: S3StorageService
Class Description: Amazon S3와의 통신을 담당하며, Pre-signed URL 발급, 파일 복사 및 최종 URL 생성 등의 비즈니스 로직을 처리하는 서비스이다.

| 구분            | 이름                                                | 설명                                        | 타입            | 접근 제한자 (Visibility) |
|:--------------|:--------------------------------------------------|:------------------------------------------|:--------------|:--------------------|
| **Attribute** | `presigner`                                       | S3 Presigner 객체                           | `S3Presigner` | `Private`           |
| **Attribute** | `s3Client`                                        | S3 Client 객체                              | `S3Client`    | `Private`           |
| **Attribute** | `bucket`                                          | S3 버킷 이름 (`${s3.bucket}` 값 주입)            | `String`      | `Private`           |
| **Attribute** | `region`                                          | AWS 리전 (`${s3.region}` 값 주입)              | `String`      | `Private`           |
| **Operation** | `createUploadUrl(String key, String contentType)` | 임시 저장용 사진을 위한 Pre-signed URL 발급           | `URL`         | `Public`            |
| **Operation** | `publishProfile(Long userId, String tempKey)`     | 임시 파일(tempKey)을 최종 프로필 경로로 복사 및 최종 URL 반환 | `String`      | `Public`            |

---
### Class Diagram #75: S3Controller
Class Description: S3 업로드 관련 API 요청을 받아 S3StorageService로 전달하고 사용자 인증 및 파일 키 생성을 처리하는 REST Controller이다.

| 구분            | 이름                                                                                          | 설명                              | 타입                 | 접근 제한자 (Visibility) |
|:--------------|:--------------------------------------------------------------------------------------------|:--------------------------------|:-------------------|:--------------------|
| **Attribute** | `s3StorageService`                                                                          | S3 스토리지 서비스                     | `S3StorageService` | `Private`           |
| **Attribute** | `userRepository`                                                                            | 사용자 엔티티 저장소                     | `UserRepository`   | `Private`           |
| **Operation** | `tempUrl(@AuthenticationPrincipal UserDetails principal, @RequestParam String contentType)` | 임시 업로드용 Pre-signed URL 발급 엔드포인트 | `S3tempResDto`     | `Public`            |
| **Operation** | `resolveUserId(UserDetails principal)`                                                      | UserDetails에서 사용자 ID를 조회        | `Long`             | `Private`           |


---