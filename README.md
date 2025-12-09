# Starlet_doc
Starlet 프로젝트 문서

## Team members

|                                           임태현                                           |                                           조민서                                           |                                           조은별                                           |                                           이나현                                           |                                           최정                                           |
|:---------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------:|
|                                        22112080                                         |                                        22311967                                         |                                        22110330                                         |                                        22311897                                         |                                        22112155                                        |
| <img src="https://avatars.githubusercontent.com/u/165642906?v=4" alt="임태현" width="150"> | <img src="https://avatars.githubusercontent.com/u/165632548?v=4" alt="조민서" width="150"> | <img src="https://avatars.githubusercontent.com/u/122366232?v=4" alt="조은별" width="150"> | <img src="https://avatars.githubusercontent.com/u/164346626?v=4" alt="이나현" width="150"> | <img src="https://avatars.githubusercontent.com/u/160298290?v=4" alt="최정" width="150"> |
|                                           FE                                            |                                           FE                                            |                                           FE                                            |                                           BE                                            |                                           BE                                           |
|                        [GitHub](https://github.com/Limtaehyeon)                         |                       [GitHub](https://github.com/chominseo0723)                        |                          [GitHub](https://github.com/eveveev)                           |                          [GitHub](https://github.com/lnahyun)                           |                        [GitHub](https://github.com/chlwjd0803)                         |

---

## Role

[//]: # (나머지분들 역할에서 뭐했는지 정리해주세요. 일단 제가 간략하게만 적었습니다. 제가 모르는 수행한것들도 넣어주세요 - 최정)

|       이름        |              보고 문서 (Document)               |                                                          개발 (Development)                                                           |        협업 문서        |
|:---------------:|:-------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------:|:-------------------:|
|     **임태현**     | SDS: Introduction, User interface prototype |                                                밤하늘 별자리 페이지, 친구 기능, FE 서버 배포 및 CI/CD 활성화                                                 |    Figma Design     |
|     **조민서**     |           SDS: Use case analysis            |                                                로그인, 회원가입, 이메일 인증 등 회원관련 전체, 별자리 아카이브                                                |    Figma Design     |
|     **조은별**     |         SDS: State machine diagram          |                                                      감정일기 달력 및 작성 관련 전체, 마이페이지 및 프로필 편집                                                     |    Figma Design     |
|     **이나현**     |  SRS All,<br> SDS: Title, Sequence diagram  |                     Diary API, MyPage API, AWS S3 Setting, MySQL RDBMS management, Continuous Testing Reporting                     |    Figma Design     |
| **최정 (Leader)** |          SDS: Title, Class diagram          | User/Email/Verify API, Star API, Constellation/Connection API, Archive API, AWS EC2 (Docker Deployment, CD), MySQL RDBMS management | Notion Meeting Page |
---

### 📌 문서 저장소 브랜치 전략
## 2025/11/13 15:30 이후부터 적용

* **`main`**: 프로젝트를 볼 수 있는 방문자들이 해당 문서를 읽을 수 있도록 하는 기본 브랜치입니다.
* **`srs/`**: srs 문서 작업을 할 때 생성하는 브랜치입니다.
* **`sds/<index>/`**: sds 문서 작업을 할 때 생성하는 브랜치입니다. index는 수정하는 목차의 이름입니다. ex) sds/classdiagram/mypage

---

### 📚 커밋 메시지 컨벤션


| 메시지        | 설명                 |
|:-----------|:-------------------|
| **`add`**  | 🥥 문서 추가, 문서 내용 추가 |
| **`edit`** | 🐛 문서 수정, 문서 이름 수정 |
| **`rmv`**  | 문서 삭제, 문서 내용 삭제    |


---
