# 4. Sequence Diagram

이 장에서는 STARLET 서비스의 주요 기능별 Sequence Diagram과 그에 대한 설명을 제공한다.  
각 다이어그램은 해당 기능의 Use Case 시나리오 에 따라 설계되었으며,  
시스템 내 객체 간의 상호작용과 데이터 흐름을 시간 순서에 따라 시각적으로 표현한다.

본 장의 목적은 기능 단위의 동적 행위를 명확히 정의함으로써,  
시스템 구현 시 컴포넌트 간 연계 구조와 메시지 교환 절차를 명확히 파악하는 데 있다.

---

## 작성 및 고려 사항

1. **모든 Sequence Diagram은 특정 Use Case와 1:1 대응된다.**  
   각 Diagram은 SRS 문서의 기능 명세와 직접적으로 연결되며, Use Case를 기준으로 구성하였다.  
   예를 들어, “회원가입”의 경우 정상 플로우와 형식 검증 실패를 별도의 Diagram으로 세분화하여 표현하였다.

2. **모든 Sequence Diagram은 실제 API 흐름과 동일한 순서를 따른다.**  
   각 Diagram의 메시지 흐름은 Controller → Service → Repository → Domain 구조를 기준으로,  
   실제 소스코드의 로직 호출 순서 및 트랜잭션 범위와 일치하도록 설계하였다.  
   외부 연동이 포함될 경우, 해당 객체를 Lifeline으로 추가하여 상호 메시지 교환 과정을 명시하였다.

3. **메시지를 주고받는 모든 클래스는 Class Diagram에서 정의된 관계를 기반으로 한다.**  
   Sequence Diagram의 참여자는 [3. Class Diagram]에 명시된 컴포넌트, 엔티티(Entity), 서비스(Service), 외부 모듈 등의 인스턴스로 구성되며,  
   각 메시지는 그 관계에 따라 정방향으로 표현된다.

4. **Diagram은 Use Case의 시간적 순서와 논리적 일관성을 유지한다.**  
   메시지 호출의 순서, 조건 분기, 병렬 흐름 등은 UML 표준 표기법을 따른다.  
   또한 Transaction 범위는 `critical` 블록으로 구분하여 명시하였다.

5. **흐름 묘사는 단순 시각적 표현에 그치지 않고, 텍스트 설명과 병행한다.**  
   각 Diagram은 시나리오 이해를 돕기 위한 글 형태의 기술과 함께 제시되며,  
   Sequence Diagram만으로 이해되지 않는 비즈니스 로직, 예외처리 조건, 외부 연계 동작 등은 설명 단락에서 보완적으로 작성하였다.

6. **공통 모듈은 별도의 공용 Sequence Diagram으로 분리하여 표현하였다.**  
   JWT 인증, 예외 처리, Validation, S3 업로드 등은 여러 기능에서 공통적으로 호출되는 흐름이므로  
   개별 Diagram으로 정의하였다. 이를 통해 중복을 제거하고 시스템 전체의 구조적 일관성을 유지하였다.

7. **각 Diagram은 SDS 내 식별자(SD-4.x.x)로 관리된다.**  
   예시:
   - SD-4.1.1 회원가입  
   - SD-4.1.2 로그인  
   - SD-4.4.1 감정 일기 작성  

   각 기능 단위로 고유 번호를 부여하여 추적성과 관리 용이성을 확보하였다.

---

## 구성 체계

본 장의 Sequence Diagram은 **도메인별로 구분**되며,  
각 도메인 내에서 API 단위 또는 세부 시나리오 단위로 세분화하였다.

| 구분 | 도메인 | 주요 내용 |
|------|---------|-----------|
| **SD-4.1** | User | 회원가입, 로그인, 로그아웃, 탈퇴 등의 사용자 관리 기능 |
| **SD-4.2** | Email | 인증 메일 발송, 확인, 비밀번호 재설정 |
| **SD-4.3** | Verify | 이메일 인증 검증 및 비밀번호 재설정 절차 |
| **SD-4.4** | Diary | 감정 일기 작성, 수정, 조회 및 별 생성 연계 |
| **SD-4.5** | Star | 별 생성, 조회, 좌표 수정, 삭제 |
| **SD-4.6** | Constellation | 별자리 생성, 수정, 아카이브, 대표 설정 |
| **SD-4.7** | MyPage | 사용자 레벨 및 통계 조회, 대표 별자리 표시 |
| **SD-4.8** | Common/System | 인증, 예외처리, 파일 업로드 등 공통 기능 |

---

## 4.1 User Sequence diagram
### SD-4.1.1 회원가입(입력 검증)
<img width="1029" height="922" alt="4-1-1 회원가입(입력 검증)" src="https://github.com/user-attachments/assets/759a012e-b34e-48d5-94dc-18a12fa92d73" />

사용자가 회원가입을 시도할 때, 서버는 입력된 **이메일, 닉네임, 비밀번호의 유효성 검증**을 수행한다.  
이 단계에서는 실제 사용자 생성은 이루어지지 않으며, 클라이언트에서 전달된 정보가 형식적 조건을 충족하는지 확인한다.  
검증은 `UserController`에서 DTO 단위의 Bean Validation(`@NotBlank`, `@Email`, `@Length` 등)을 통해 수행되며,  
검증 실패 시 `GlobalExceptionHandler`에 의해 `400 BAD_REQUEST` 응답이 반환된다.  
또한 이메일 또는 닉네임이 이미 사용 중인지 확인하여 중복 예외(`EMAIL_CONFLICT`, `NICKNAME_CONFLICT`)를 발생시킨다.


**흐름 요약**
1. **Client → UserController** : `POST /api/v1/user/signup` 요청 (SignUpDto)
2. **UserController** : DTO 유효성 검사(Bean Validation) 수행
3. **GlobalExceptionHandler** : 유효성 실패 시 `400 BAD_REQUEST` 반환
4. **UserService** : `EmailService.existsEmailAddress()` 및 `UserRepository.existsByNickname()` 호출
5. **중복 시 예외 발생** → `EMAIL_CONFLICT` 또는 `NICKNAME_CONFLICT`
6. **모든 검증 통과 시** 다음 단계(`SD-4.1.2 회원가입(이메일 인증 포함)`)로 진입
<br>

### SD-4.1.2 회원가입(이메일 인증 포함)
<img width="1469" height="963" alt="image" src="https://github.com/user-attachments/assets/fe752911-b0ab-46ab-a6cf-39fe97f300f4" />

이 기능은 이메일 인증이 완료된 사용자가 실제로 회원가입을 완료하는 단계이다.  
사용자가 입력한 이메일·닉네임·비밀번호 정보를 기반으로  
`UserController.signup()` → `UserService.signUp()` 순서로 호출된다.

`UserService.signUp()`은 먼저 `EmailService.findEmailByAddress()`를 통해  
해당 이메일이 존재하는지 확인하고,  
그 이메일의 `VerifyType`이 `VERIFY` 상태인지 검증한다.  
만약 인증이 완료되지 않았거나(`NOT_VERIFY_USER`),  
존재하지 않는 이메일(`EMAIL_NOT_FOUND`),  
닉네임이 중복(`NICKNAME_CONFLICT`)된 경우에는 예외를 발생시킨다.  

모든 검증이 통과하면 비밀번호를 암호화하여 `UserRepository.save()`로 사용자 정보를 저장하고,  
201 Created 응답과 함께 신규 사용자 URI(`/api/v1/user/{id}`)를 반환한다.

**흐름 요약**
1. **Client → UserController** : `POST /api/v1/user/signup` (요청 본문: `SignUpDto`)
2. **UserController → UserService** : `signUp(dto)` 호출
3. **UserService → EmailService** : `findEmailByAddress(dto.email)`  
   - 이메일 존재 확인 (`EmailRepository.findByAddress()`)
4. **EmailService → UserService** : 이메일 엔티티 반환  
   - 인증 상태(`VerifyType`) 검사
5. **UserService → UserRepository** : 닉네임 중복 검사 (`existsByNickname`)
6. **조건 분기**  
   - `NOT_VERIFY_USER` → 이메일 인증 미완료  
   - `NICKNAME_CONFLICT` → 닉네임 중복  
   - `EMAIL_NOT_FOUND` → 이메일 존재하지 않음
7. **UserService → PasswordEncoder** : 비밀번호 암호화 수행  
8. **UserService → UserRepository** : 신규 사용자 저장 (`save(User)`)
9. **UserController → Client** : `201 Created` 응답 + Location Header(`/api/v1/user/{id}`)
<br>

### SD-4.1.3 닉네임 중복 확인
<img width="1218" height="540" alt="image" src="https://github.com/user-attachments/assets/934b2040-3f1c-416f-9376-e4b830650961" />

회원가입 단계에서 입력된 닉네임이 이미 사용 중인지 확인하는 기능이다.  
`UserController.existNickname()`이 `UserService.existNickname()`을 호출하여,  
해당 닉네임이 DB에 존재하는지 여부를 검사한다.  
이미 존재하는 닉네임일 경우 `CustomException(ErrorCode.NICKNAME_CONFLICT)`를 발생시켜  
`409 CONFLICT` 응답을 반환하며, 사용 가능한 닉네임일 경우 `200 OK` 응답을 반환한다.  

이 기능은 회원가입 입력 검증 단계(`SD-4.1.1`)와 동일한 검증 로직을 수행하지만,  
**별도의 단일 API**로 분리되어 프론트엔드에서 실시간 중복 체크용으로 사용된다.

**흐름요약**
1. **Client → UserController** : `GET /api/v1/user/signup/nickname_available?nickname={nickname}`
2. **UserController → UserService** : `existNickname(nickname)` 호출
3. **UserService → UserRepository** : `existsByNickname(nickname)` 실행
4. **UserRepository → UserService** : `true`(중복) / `false`(미중복)
5. **중복 시** : `CustomException(NICKNAME_CONFLICT)` → `409 CONFLICT`
6. **중복이 아닐 시** : `ResponseEntity.ok().build()` → `200 OK`
<br>

### SD-4.1.4 이메일 중복 확인
<img width="1105" height="540" alt="image" src="https://github.com/user-attachments/assets/05530cb0-889d-41c4-b084-e8b3caee1ac4" />

회원가입 과정에서 입력된 이메일 주소가 이미 존재하는지 확인하는 기능이다.  
`EmailController.checkDuplication()`이 `EmailService.existsEmailAddress()`를 호출하여,  
해당 이메일이 DB에 등록되어 있는지 여부를 검사한다.  
이미 존재하는 이메일일 경우 `CustomException(ErrorCode.EMAIL_CONFLICT)`를 발생시켜  
`409 CONFLICT` 응답을 반환하며, 사용 가능한 이메일일 경우 `200 OK` 응답을 반환한다.  

이 기능은 회원가입 입력 검증 단계(`SD-4.1.1`)와 동일한 검증 로직을 수행하지만,  
**별도의 단일 API**로 분리되어 프론트엔드에서 실시간 중복 체크용으로 사용된다.

**흐름요약**
1. **Client → EmailController** : `GET /api/v1/email/check-duplication?address={email}`
2. **EmailController → EmailService** : `existsEmailAddress(address)` 호출
3. **EmailService → EmailRepository** : `existsByAddress(address)` 실행
4. **EmailRepository → EmailService** : `true`(중복) / `false`(미중복)
5. **중복 시** : `CustomException(EMAIL_CONFLICT)` → `409 CONFLICT`
6. **중복이 아닐 시** : `ResponseEntity.ok().build()` → `200 OK`
<br>

---

## 4.2 Email Sequence diagram
### SD-4.2.1 이메일 인증 상태 조회
<img width="1489" height="569" alt="image" src="https://github.com/user-attachments/assets/408a4b35-f375-4680-81dd-3bdab50c39de" />


이메일 주소를 기반으로 현재 인증 상태(가입 인증, 비밀번호 재설정 요청, 인증 완료 등)를 조회하는 기능이다.  
`EmailController.getVerificationStatus()`가 `EmailService.getVerificationStatus()`를 호출하며,  
이 서비스는 내부적으로 `findEmailByAddress()`를 통해 이메일 객체를 조회하고,  
해당 이메일과 연결된 `Verify` 객체의 인증 타입(`VerifyType`) 및 만료 시간(`expireTime`)을 반환한다.  

해당 이메일이 존재하지 않을 경우 `CustomException(ErrorCode.EMAIL_NOT_FOUND)`가 발생하여  
`404 NOT_FOUND` 응답을 반환한다.  
정상 조회 시에는 `EmailInfoDto`(`emailId`, `emailAddress`, `verifyType`, `verifyExpireAt`)를 포함한  
`200 OK` 응답을 반환한다.

**흐름요약**
1. **Client → EmailController** : `GET /api/v1/email/verification-status?address={email}`
2. **EmailController → EmailService** : `getVerificationStatus(address)` 호출
3. **EmailService → EmailRepository** : `findByAddress(address)` 실행
4. **EmailRepository → EmailService** : `Email` 객체 반환
5. **EmailService → Verify(연관객체)** : `getType(), getExpireTime()` 조회
6. **EmailService → EmailInfoDto** : 이메일 상태 정보 매핑
7. **정상 응답 시** : `200 OK` + 인증 상태 정보 반환
8. **이메일 미존재 시** : `CustomException(EMAIL_NOT_FOUND)` → `404 NOT_FOUND`
<br>

### SD-4.2.2 초기 이메일 인증 전송
<img width="1433" height="1369" alt="image" src="https://github.com/user-attachments/assets/625b7a57-0797-4dc5-b096-2c9d658562e8" />


사용 가능한 이메일 주소에 대해 **가입 인증 메일을 최초 발송 또는 재전송**하는 기능이다.  
`EmailController.initEmail()`이 `EmailService.initEmail(dto)`를 호출하며, 이메일 존재 여부에 따라 분기한다.  
이미 해당 이메일로 **가입된 사용자**가 존재하면 `USER_ALREADY_EXIST` 예외로 방어하고,  
이메일은 존재하지만 가입이 완료되지 않은 경우에는 기존 `Verify`를 조회하여 **토큰/만료시간(8시간)** 을 갱신한 뒤 메일을 재전송한다.  
처음 시도하는 이메일이면 `VerifyService.createVerify()`로 인증 객체를 생성하고, `createEmail(address, verify)`로 이메일 엔티티를 만든 후 인증 메일을 발송한다.  
정상 처리 시 `200 OK`를 반환한다.

**흐름요약**
1. **Client → EmailController** : `POST /api/v1/email/init` (Body: `EmailAddressDto{ email }`)
2. **EmailController → EmailService** : `initEmail(dto)` 호출
3. **EmailService → EmailRepository** : `existsByAddress(email)` 실행
4. **[분기 A: 이메일 존재]**
   - **EmailService → UserRepository** : `existsByEmailAddress(email)` → 존재 시 `USER_ALREADY_EXIST`
   - **EmailService → VerifyRepository** : `findByEmail_Address(email)` → 없으면 `VERIFY_NOT_FOUND`
   - **EmailService** : `verify.updateStatus(verifyService.createToken(), EMAIL_VERIFICATION, now+8h)`
   - **EmailService → VerifyRepository** : `save(verify)`
   - **EmailService** : `findEmailByAddress(email)` 로 `Email` 조회
   - **EmailService** : `sendVerificationEmail(email, verify.token)` (실패 시 `EMAIL_SEND_FAILED`)
5. **[분기 B: 이메일 최초]**
   - **EmailService → VerifyService** : `createVerify()` (type=EMAIL_VERIFICATION, expire=now+8h)
   - **EmailService** : `createEmail(address, verify)` 저장
   - **EmailService** : `sendVerificationEmail(email, verify.token)` (실패 시 `EMAIL_SEND_FAILED`)
6. **정상 응답** : `200 OK`
<br>

### SD-4.2.3 이메일 인증 확인

사용자가 이메일로 받은 인증 링크를 클릭하면, 해당 링크에 포함된 `token`을 통해 인증을 완료하는 기능이다.  
`VerifyService.emailVerification(token)`이 호출되어 토큰의 유효성과 타입을 검증한 뒤,  
인증 상태(`VerifyType.VERIFY`)로 업데이트한다.  
토큰이 존재하지 않거나 타입이 일치하지 않으면 각각 `VERIFY_NOT_FOUND`, `VERIFY_TYPE_NOT_MATCHED` 예외가 발생한다.  
정상적으로 인증이 완료되면 사용자의 이메일이 “인증 완료 상태”로 전환되며, 프론트엔드에서 완료 페이지를 표시한다.

**흐름요약**
1. **Client → VerifyController (또는 View 요청)** : `GET /view/v1/verify/init?token={token}`
2. **Controller → VerifyService** : `emailVerification(token)` 호출
3. **VerifyService → VerifyRepository** : `findByToken(token)` 실행
4. **토큰 없음** : `VERIFY_NOT_FOUND` → `404 NOT_FOUND`
5. **타입 불일치** : `VERIFY_TYPE_NOT_MATCHED` → `400 BAD_REQUEST`
6. **정상 흐름**
   - `verify.updateStatus(null, VERIFY, null)`  
   - `verifyRepository.save(verify)`
7. **정상 응답** : `200 OK`
<br>

### SD-4.2.3 이메일 인증 확인
<img width="1117" height="788" alt="image" src="https://github.com/user-attachments/assets/528b694e-568c-41c0-a634-8e74ef22618e" />

사용자가 이메일로 받은 인증 링크를 클릭하면, 해당 링크에 포함된 `token`을 통해 인증을 완료하는 기능이다.  
`VerifyService.emailVerification(token)`이 호출되어 토큰의 유효성과 타입을 검증한 뒤,  
인증 상태(`VerifyType.VERIFY`)로 업데이트한다.  
토큰이 존재하지 않거나 타입이 일치하지 않으면 각각 `VERIFY_NOT_FOUND`, `VERIFY_TYPE_NOT_MATCHED` 예외가 발생한다.  
정상적으로 인증이 완료되면 사용자의 이메일이 “인증 완료 상태”로 전환되며, 프론트엔드에서 완료 페이지를 표시한다.

**흐름요약**
1. **Client → VerifyController (또는 View 요청)** : `GET /view/v1/verify/init?token={token}`
2. **Controller → VerifyService** : `emailVerification(token)` 호출
3. **VerifyService → VerifyRepository** : `findByToken(token)` 실행
4. **토큰 없음** : `VERIFY_NOT_FOUND` → `404 NOT_FOUND`
5. **타입 불일치** : `VERIFY_TYPE_NOT_MATCHED` → `400 BAD_REQUEST`
6. **정상 흐름**
   - `verify.updateStatus(null, VERIFY, null)`  
   - `verifyRepository.save(verify)`
7. **정상 응답** : `200 OK`
<br>

### SD-4.2.4 비밀번호 재설정 요청  
<img width="1691" height="1386" alt="image" src="https://github.com/user-attachments/assets/090e8df3-54be-4767-b6a2-ac656d4626e9" />


사용자가 비밀번호를 잊은 경우, 가입된 이메일로 비밀번호 재설정 링크를 전송하는 기능이다.  
`EmailController.requestPasswordReset()`이 `EmailService.requestPasswordReset(dto)`를 호출하며,  
서비스는 (1) 가입 사용자 존재 여부를 `UserRepository.findByEmailAddress()`로 확인하고,  
(2) 이메일 엔티티를 `findEmailByAddress()`로 조회한다.  
이후 `VerifyService.passwordResetRequestStatus(email)`에서 인증 상태를  
`REQUEST_PASSWORD_RESET`으로 전환하고(토큰 재발급 + 24시간 만료 설정),  
`sendPasswordResetEmail(email, token)`으로 메일을 발송한다.  
가입 사용자가 없으면 `USER_NOT_FOUND`, Email 엔티티가 없으면 `EMAIL_NOT_FOUND`,  
인증 상태가 가입 미완(EMAIL_VERIFICATION)일 경우 `VERIFY_TYPE_NOT_MATCHED` 예외가 발생한다.  
정상 처리 시 `200 OK`를 반환한다.

**흐름요약**  
1. **Client → EmailController** : `POST /api/v1/email/password-reset/request` (EmailAddressDto{ email })  
2. **EmailController → EmailService** : `requestPasswordReset(dto)` 호출  
3. **EmailService → UserRepository** : `findByEmailAddress(email)` → 없으면 `USER_NOT_FOUND`  
4. **EmailService → EmailRepository** : `findByAddress(email)` → 없으면 `EMAIL_NOT_FOUND`  
5. **EmailService → VerifyService** : `passwordResetRequestStatus(email)`  
   - 상태 검증 (가입 미완이면 `VERIFY_TYPE_NOT_MATCHED`)  
   - `token=UUID`, `type=REQUEST_PASSWORD_RESET`, `expire=now+24h` 로 업데이트 및 저장  
6. **EmailService → JavaMailSender** : `sendPasswordResetEmail(email, token)` 실행  
7. **정상 응답** : `200 OK`  
<br>

### SD-4.2.5 비밀번호 재설정 완료  
<img width="1602" height="1110" alt="image" src="https://github.com/user-attachments/assets/8295e1b7-6308-4814-9aaf-5a9110c9fe6f" />


사용자가 비밀번호 재설정 허용 링크를 통해 페이지에 진입한 뒤,  
새로운 비밀번호를 입력하면 서버는 해당 계정의 비밀번호를 암호화하여 저장하고  
인증 상태를 정상(`VERIFY`)으로 되돌린다.  

`VerifyController.confirmChangePassword()`가  
`VerifyService.updatePassword(dto)`를 호출하며,  
서비스는 다음 순서로 로직을 수행한다.  
1. `EmailRepository.findByAddress()`로 이메일 존재 여부 확인  
2. `email.verify.type == CHANGING_PASSWORD` 검증  
3. `UserRepository.findByEmailAddress()`로 사용자 존재 여부 확인  
4. `PasswordEncoder`로 새 비밀번호 암호화 후 저장  
5. 인증정보(`Verify`)를 `VERIFY` 상태로 복원  
모든 절차가 완료되면 `200 OK`를 반환한다.  

예외 상황:
- 이메일이 없으면 `EMAIL_NOT_FOUND`  
- 인증 상태가 `CHANGING_PASSWORD`가 아니면 `VERIFY_TYPE_NOT_MATCHED`  
- 사용자가 없으면 `USER_NOT_FOUND`

**흐름요약**  
1. **Client → VerifyController** : `POST /api/v1/verify/password-reset/new-password` (PasswordResetConfirmDto{ email, newPassword })  
2. **VerifyController → VerifyService** : `updatePassword(dto)` 호출  
3. **VerifyService → EmailRepository** : `findByAddress(dto.email)` → 없으면 `EMAIL_NOT_FOUND`  
4. **VerifyService** : `email.verify.type == CHANGING_PASSWORD` 검증 → 아니면 `VERIFY_TYPE_NOT_MATCHED`  
5. **VerifyService → UserRepository** : `findByEmailAddress(dto.email)` → 없으면 `USER_NOT_FOUND`  
6. **VerifyService** : `PasswordEncoder.encode(newPassword)` → `user.changePassword(encoded)` → 저장  
7. **VerifyService** : `verify.updateStatus(null, VERIFY, null)` → 저장  
8. **정상 응답** : `200 OK`  
<br>

---

## 4.3 Verify Sequence diagram
### SD-4.3.1 인증 링크 확인  
<img width="925" height="856" alt="image" src="https://github.com/user-attachments/assets/7c5e8378-ef94-4e0b-8617-b002266bc2a7" />

회원가입 시 사용자에게 발송된 인증 링크(`GET /view/v1/verify/init?token={token}`)를 사용자가 클릭하면,  
`VerifyViewController.emailVerification(token)`이 `VerifyService.emailVerification(token)`을 호출하여  
해당 **토큰의 존재 여부와 타입 일치 여부**를 검증한다.  

인증 객체가 존재하고 타입이 `EMAIL_VERIFICATION`일 경우,  
인증 상태를 `VERIFY`로 전환하여 최종 인증 완료 처리를 수행한다.  

성공 시 `verification-success` 템플릿을 반환하고,  
예외(`VERIFY_NOT_FOUND`, `VERIFY_TYPE_NOT_MATCHED`) 발생 시  
에러 메시지를 담아 `verification-error` 템플릿을 반환한다.  

**흐름요약**  
1. **Client → VerifyViewController** : `GET /view/v1/verify/init?token={token}`  
2. **VerifyViewController → VerifyService** : `emailVerification(token)` 호출  
3. **VerifyService → VerifyRepository** : `findByToken(token)` → 없으면 `VERIFY_NOT_FOUND`  
4. **VerifyService** : `verify.type == EMAIL_VERIFICATION` 검증 → 아니면 `VERIFY_TYPE_NOT_MATCHED`  
5. **VerifyService** : `verify.updateStatus(null, VERIFY, null)` → `verifyRepository.save(verify)`  
6. **성공 시** : `model.addAttribute(title, message)` → `verification-success.html` 반환  
7. **실패 시** : `CustomException` catch → `model.addAttribute(message)` → `verification-error.html` 반환  
<br>

### SD-4.3.2 인증 성공 처리  
<img width="1184" height="788" alt="image" src="https://github.com/user-attachments/assets/85b722f1-fcb3-41e4-982d-6e9b750d8daa" />

이 기능은 이메일 인증 완료 후 내부적으로 인증 객체(`Verify`)의 상태를  
최종적으로 `VERIFY`로 업데이트하는 과정이다.  

`VerifyService.emailVerification(token)`이 호출되면  
`validateToken(token, EMAIL_VERIFICATION)`을 통해 토큰 유효성 검증을 수행하고,  
성공 시 `verify.updateStatus(null, VERIFY, null)`로 상태를 갱신한 뒤 DB에 반영한다.  

컨트롤러 단에서 JSON 응답 대신 **200 OK**만 반환하며,  
이 로직은 뷰 렌더링(`SD-4.3.1`)에서도 동일하게 내부적으로 호출되어  
인증 완료 처리를 담당한다.  

**흐름요약**  
1. **Client → VerifyController** : `POST /api/v1/verify/email-confirm?token={token}` (가정 경로)  
2. **VerifyController → VerifyService** : `emailVerification(token)` 호출  
3. **VerifyService → VerifyRepository** : `findByToken(token)`  
4. **VerifyService** : `verify.type == EMAIL_VERIFICATION` 검증  
5. **VerifyService** : `verify.updateStatus(null, VERIFY, null)`  
6. **VerifyRepository → DB** : `save(verify)`  
7. **성공 시** : `ResponseEntity.ok().build()` (200 OK)  
8. **실패 시** : `CustomException` → GlobalExceptionHandler 변환 후 404/400 응답  
<br>

### SD-4.3.3 비밀번호 재설정 링크 검증  
<img width="1165" height="856" alt="image" src="https://github.com/user-attachments/assets/3fbe3e63-6e33-4ca3-86e8-20d7dcaafeeb" />


비밀번호 재설정 이메일을 받은 사용자가 링크(`GET /view/v1/verify/password-reset/confirm?token={token}`)를 클릭하면,  
`VerifyViewController.passwordResetVerification(token)`이 호출되어  
`VerifyService.passwordResetVerification(token)`을 통해 토큰의 유효성을 검증하고,  
정상적인 요청일 경우 인증 상태를 `CHANGING_PASSWORD`로 변경한다.  

이 과정을 통해 사용자는 새 비밀번호를 입력할 수 있는 상태로 전환되며,  
성공 시 `password-reset-success` 뷰가 렌더링되고  
토큰이 유효하지 않거나 만료된 경우 `verification-error` 페이지로 이동한다.  

**흐름요약**  
1. **Client → VerifyViewController** : `GET /view/v1/verify/password-reset/confirm?token={token}`  
2. **VerifyViewController → VerifyService** : `passwordResetVerification(token)` 호출  
3. **VerifyService → VerifyRepository** : `findByToken(token)` 수행  
4. **토큰 없음** → `VERIFY_NOT_FOUND` 예외 발생  
5. **타입 불일치 (`type != REQUEST_PASSWORD_RESET`)** → `VERIFY_TYPE_NOT_MATCHED` 예외 발생  
6. **정상 토큰** → `verify.updateStatus(null, CHANGING_PASSWORD, null)`  
7. **VerifyRepository → DB** : `save(verify)`  
8. **성공 시** : `password-reset-success.html` 반환  
9. **실패 시** : `verification-error.html` 반환  
<br>

### SD-4.3.4 비밀번호 변경 완료  
<img width="1602" height="1110" alt="image" src="https://github.com/user-attachments/assets/548c7f5e-bb89-471d-b6f4-a087211ad2cf" />


사용자가 새 비밀번호를 제출하면  
`VerifyController.confirmChangePassword()`가 `VerifyService.updatePassword(dto)`를 호출하여  
해당 이메일의 인증 상태가 `CHANGING_PASSWORD`인지 확인한 뒤,  
`PasswordEncoder`로 새 비밀번호를 암호화해 저장하고 인증 상태를 `VERIFY`로 복원한다.  

예외 상황:  
- `EMAIL_NOT_FOUND` : 이메일 엔티티가 없음  
- `VERIFY_TYPE_NOT_MATCHED` : 인증 상태가 `CHANGING_PASSWORD`가 아님  
- `USER_NOT_FOUND` : 이메일에 해당하는 사용자가 없음  

**흐름요약**  
1. **Client → VerifyController** : `POST /api/v1/verify/password-reset/new-password` (PasswordResetConfirmDto{ email, newPassword })  
2. **VerifyController → VerifyService** : `updatePassword(dto)` 호출  
3. **VerifyService → EmailRepository** : `findByAddress(dto.email)` → 없으면 `EMAIL_NOT_FOUND`  
4. **VerifyService** : `email.verify.type == CHANGING_PASSWORD` 검증 → 아니면 `VERIFY_TYPE_NOT_MATCHED`  
5. **VerifyService → UserRepository** : `findByEmailAddress(dto.email)` → 없으면 `USER_NOT_FOUND`  
6. **VerifyService** : `PasswordEncoder.encode(newPassword)` → `user.changePassword(encoded)` → `userRepository.save(user)`  
7. **VerifyService** : `verify.updateStatus(null, VERIFY, null)` → `verifyRepository.save(verify)`  
8. **정상 응답** : `200 OK`  
<br>



