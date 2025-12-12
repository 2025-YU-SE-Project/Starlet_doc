## 📝 Starlet API 명세서

---

|         인덱스          | 기능                    |  메서드   | API Path                                            | 로그인(토큰) 여부 |
|:--------------------:|:----------------------|:------:|:----------------------------------------------------|:----------:|
|      **[User]**      |                       |        |                                                     |            |
|          1           | 회원가입                  |  POST  | `/api/v1/user/signup`                               |     X      |
|          2           | 사용가능 닉네임 확인 (중복, 유해성) |  GET   | `/api/v1/user/signup/nickname_available`            |     X      |
|          3           | 로그인                   |  POST  | `/api/v1/user/login`                                |     X      |
|          4           | 회원 탈퇴                 | DELETE | `/api/v1/user/me`                                   |     O      |
|          5           | 로그아웃                  |  POST  | `/api/v1/user/logout`                               |     O      |
|  **[Email/Verify]**  |                       |        |                                                     |            |
|          6           | 이메일 인증 정보 확인          |  GET   | `/api/v1/email/verification-status`                 |     X      |
|          7           | 이메일 주소 중복 확인          |  GET   | `/api/v1/email/check-duplication`                   |     X      |
|          8           | 가입 가능 이메일 인증메일 발송     |  POST  | `/api/v1/email/init`                                |     X      |
|          9           | 비밀번호 변경 요청 인증메일 발송    |  POST  | `/api/v1/email/password-reset/request`              |     X      |
|          10          | 새 비밀번호 반영             |  POST  | `/api/v1/verify/password-reset/new-password`        |     X      |
| **[Diary/Calendar]** |                       |        |                                                     |            |
|          11          | 감정 일기 생성 및 별 생성 연계    |  POST  | `/api/v1/calendar/diary`                            |     O      |
|          12          | 감정 일기 수정 (내용만)        | PATCH  | `/api/v1/calendar/diary`                            |     O      |
|          13          | 특정 날짜 감정 일기 조회        |  GET   | `/api/v1/calendar/diary/{date}`                     |     O      |
|          14          | 월별 별 목록 조회 (하이라이트)    |  GET   | `/api/v1/calendar/star`                             |     O      |
|          15          | 한 달 일기 분석 요약          |  GET   | `/api/v1/calendar/diary/summary`                    |     O      |
|      **[Star]**      |                       |        |                                                     |            |
|          17          | 별 정보 조회 (별/일기 ID)     |  GET   | `/api/v1/star/detail/{id}`                          |     O      |
|          18          | 별 위치 최신화              | PATCH  | `/api/v1/star/reposition/{id}`                      |     O      |
|  **[Starry Night]**  |                       |        |                                                     |            |
|          19          | 밤하늘 별자리들 조회 (2개월 단위)  |  GET   | `/api/v1/constellation`                             |     O      |
|          20          | 밤하늘 별들 조회 (2개월 단위)    |  GET   | `/api/v1/star`                                      |     O      |
|          21          | 별자리 생성                |  POST  | `/api/v1/constellation`                             |     O      |
|          22          | 별자리 위치 최신화            | PATCH  | `/api/v1/constellation/reposition/{id}`             |     O      |
|          23          | 별자리 이름 및 설명 추천 (AI)   |  POST  | `/api/v1/constellation/suggest`                     |     O      |
|    **[Archive]**     |                       |        |                                                     |            |
|          24          | 별자리 아카이브 목록 조회        |  GET   | `/api/v1/constellation/archive`                     |     O      |
|          25          | 별자리 아카이브 페이지 조회       |  GET   | `/api/v1/constellation/archive/paging`              |     O      |
|          26          | 별자리 아카이브 상세 조회        |  GET   | `/api/v1/constellation/archive/{id}`                |     O      |
|          27          | 별자리 이름 및 설명 수정        | PATCH  | `/api/v1/constellation/{id}`                        |     O      |
|          28          | 대표 별자리 설정             |  POST  | `/api/v1/constellation/archive/{id}/representative` |     O      |
|     **[MyPage]**     |                       |        |                                                     |            |
|          29          | 마이페이지 요약 정보 조회 (종합)   |  GET   | `/api/v1/mypage/summary`                            |     O      |
|          30          | 사용자 프로필 요약 조회         |  GET   | `/api/v1/mypage/user`                               |     O      |
|          31          | 사용자 레벨 조회             |  GET   | `/api/v1/mypage/level`                              |     O      |
|          32          | 대표 별자리 조회             |  GET   | `/api/v1/mypage/representative`                     |     O      |
|          33          | 연간 월별 별자리 수 통계        |  GET   | `/api/v1/mypage/year`                               |     O      |
|          34          | 월별 감정 통계              |  GET   | `/api/v1/mypage/month`                              |     O      |
|          35          | 프로필 사진 확정 (S3 업로드 후)  |  POST  | `/api/v1/mypage/photo/confirm`                      |     O      |
|          36          | 닉네임 중복 확인 (마이페이지)     |  GET   | `/api/v1/mypage/available`                          |     O      |
|          37          | 닉네임 수정                | PATCH  | `/api/v1/mypage/nickname`                           |     O      |
|    **[Friends]**     |                       |        |                                                     |            |
|          38          | 친구 검색                 |  GET   | `/api/v1/friends/search`                            |     O      |
|          39          | 친구 요청                 |  POST  | `/api/v1/friends/request`                           |     O      |
|          40          | 친구 요청 수락              |  POST  | `/api/v1/friends/accept`                            |     O      |
|          41          | 친구 요청 거절              | DELETE | `/api/v1/friends/reject`                            |     O      |
|          42          | 친구 삭제                 | DELETE | `/api/v1/friends/{friendId}`                        |     O      |
|          43          | 받은 친구 요청 목록 조회        |  GET   | `/api/v1/friends/requests`                          |     O      |
|          44          | 친구 목록 조회              |  GET   | `/api/v1/friends/list`                              |     O      |