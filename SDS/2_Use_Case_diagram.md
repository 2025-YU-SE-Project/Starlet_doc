# Starlet: 소프트웨어 설계 명세서 (SDS)

---

## 2. Use Case

## Use case analysis
이번 장은 STARLET 시스템의 Use Case Diagram과 Use Case Description을 제시한다.
이 장에서는 Diagram의 개요, 구성 목적, 그리고 각 Use Case 간의 관계를 중심으로 기술할 예정이다.

- 본 시스템은 사용자가 직접 작성한 일기를 바탕으로 기록된 내용을 별과 별자리 형태로 시각화하는 감정 일기 서비스이다.
- Use Case Diagram은 시스템의 전체 구조와 사용자(User)가 수행할 수 있는 주요 기능을 시각적으로 표시한다.
- Diagram에 표함된 Use Case들은 기능적 흐름에 따라 요약(Summary), 사용자 목표(User-goal), 하위 기능(Subfunction) 수준으로 구성되었다.
- 모든 Use Case는 로그인된 사용자를 중심으로 수행되며, 회원가입 기능만 비로그인 상태에서 수행가능하다.
- STARLET 시스템에 포함된 기능은 홈 화면 진입을 중심으로, 감정 일기 작성, 별자리 생성 및 조회, 아카이브, 마이페이지 등으로 세분화된다.

## 각 use case의 level은 summary, user-goal, subfunction로 구분한다
### Summary level
- 시스템 전체의 기본 진입과 구성을 나타낸다
- ** Use Case #1 홈 화면 집입 및 시스템 내 기능 확인 **이 이에 해당하며, 사용자는 홈 화면을 통해 주요 기능(Night Sky Page, My Diary, Constellation Archive)을 확인하고 접근할 수 있다.
- 비로그인 상태에서는 로그인 페이지로 이동된다.

### User level
- 사용자가 시스템 내에서 수행하고자 하는 주요 목적 중심의 Use Case이다.
- 대표적인 예로 다음과 같은 기능들이 포함된다 <br> 1. 감정일기 작성/조회/수정 <br> 2. 별자리 생성 및 조회 <br> 3. 별자리 아카이브 및 상세 조회 <br> 4. 마이페이지 조회
- 이러한 기능들은 독립적이며, 시스템 주요 시나리오를 구성한다.

## Subfunction level
- 상위 User level Use Case의 일부 과정으로 수행되는 하위 기능이다.
- 예를 들어, 별자리 위치 및 크기조정은 ```별자리 생성```의 확장 Use Case로 생성 후 배치 조정 세부 기능을 수행한다. <br> ```별자리 정보 수정```은 ```별자리 상세 조회```의 확장 Use Case로, 별자리 조회 후 수정 기능을 포함한다. <br> ```대표 별자리 설정```은 ```별자리 아카이브 조회```의 확장 Use Case로, 아카이브 내 특정 별자리를 대표 별자리로 진행한다.
- 이와 같은 Subfunction들은 주기적으로 호출되며, 메인 시나리오를 보조한다.

## Use case Diagram

<img width="898" height="1264" alt="image" src="https://github.com/user-attachments/assets/99505388-8c0e-4f02-9323-97a0c0e4176e" />

``` [그림] use case diagram ```

## Use Case 관계
### Include
특정 Use Case가 반드시 다른 Use Case의 일부로 포함될 때 사용된다.
- 별자리 생성은 별 및 별자리 조회를 포함한다.
- 별자리 상세 조회는 별자리 아카이브 조회를 포함한다.
### Extend
기본 흐름에 선택적으로 추가되는 확장 기능이다.
한-영 변환 토글은 홈 화면 진입의 확장 기능으로 언어 전환을 제공한다.
별자리 위치 및 크기 조정은 별자리 생성의 확장 기능이다.
별자리 정보 수정은 별자리 상세 조회의 확장 기능이다.
대표 별자리 설정은 별자리 아카이브 조회의 확장 기능이다.

### [그림] Diagram 설명

```[그림]```은 STARLET 시스템의 Use Case Diagram을 나타낸다.
사용자는 시스템에 로그인한 상태에서 감정 일기를 작성하고, 해당 감정일기에 따른 별이 생성되며
밤하늘 페이지에서 별자리를 생성·조정·조회할 수 있다.
생성된 별자리는 별자리 아카이브에서 확인 및 관리가 가능하며, 대표 별자리 설정을 통해
마이페이지의 대표 이미지로 표시된다.
모든 주요 기능은 홈 화면에서 접근 가능하며, UI 언어를 한/영 토글을 통해 전환할 수 있다.

## Use case Description

###  Use Case #1 홈 화면 진입 및 시스템 내 기능 확인
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** |  사용자는 시스템을 접속하여 홈 화면을 통해 서비스 주요 기능(Night Sky Page, My Diary, Constellation Archive)을 확인하고 선택할 수 있다. <br> 단, 로그인하지 않은 사용자가 해당 기능을 선택할 경우 로그인 페이지로 이동되며, 로그인 후에만 해당 기능에 접근 가능하다.  |
| **Scope** | STARLET System |
| **Level** | Summary level |
| **Author** |  |
| **Last Update** |  |
| **Status** | Analysis |
| **Primary Actor** | User |
| **Preconditions** | 사용자는 시스템에 접속된 상태여야 한다. |
| **Trigger** | 사용자가 시스템에 진입하였을 때 |
| **Success Post Condition** | 사용자는 홈 화면에서 각 기능의 역할을 확인할 수 있다.  |
| **Failed Post Condition** | 사용자는 홈 화면에서 각 기능의 역할을 확인할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자가 시스템에 접속한다.  |
| 1 |  시스템은 홈 화면을 로드하고, 주요 기능을 표시한다. |
| 2 |  사용자는 기능 중 하나를 클릭한다. |
| 3 |  로그인된 사용자일 경우, 선택한 기능에 대한 페이지로 이동한다. |
| 4 |  로그인되지 않은 사용자일 경우, 로그인 페이지로 이동한다. |
| 5 |  사용자는 단계 1~4를 원할 때까지 반복한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| S | 1a. 네트워크 또는 통신에 문제가 있는 경우 <br> 1a1. 이용자는 어떠한 화면도 볼 수 없다. |


#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #2 회원가입
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** |  처음 해당 시스템을 접한 사용자가 시스템 기능을 이용하기 위한 절차이며, 해당 사용자는 기능을 이용하기 위해 회원가입을 해야한다.  |
| **Scope** | STARLET System |
| **Level** | User level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** | Analysis |
| **Primary Actor** | User |
| **Preconditions** | 사용자는 시스템에 접속된 상태여야 한다. |
| **Trigger** | 사용자가 홈 화면에서 회원가입(Sign up)을 누를 때  |
| **Success Post Condition** | 사용자는 로그인을 진행할 수 있다.  |
| **Failed Post Condition** | 사용자는 로그인을 진행할 수 없다. <br> 사용자는 시스템 기능을 이용할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자가 회원가입을 한다.  |
| 1 |  사용자는 홈 화면에서 회원가입(Sign up)을 누르고 회원가입 페이지에 진입한다. |
| 2 |  사용자는 이메일 주소를 입력 후 중복 확인 버튼을 클릭한다. |
| 3 |  시스템은 이메일 중복을 판단한다. |
| 4 |  사용자는 닉네임 입력 후 중복 확인 버튼을 클릭한다. |
| 5 |  시스템은 닉네임 중복을 판단한다. |
| 6 |  사용자는 비밀번호, 비밀번호 확인 필드를 입력한다.  |
| 7 |  시스템은 비밀번호, 비밀번호 확인 필드 입력값이 같은지 판단한다. |
| 8 |  모든 입력필드를 입력 후 SIGNUP 버튼을 누른다. |
| 9 |  시스템은 회원가입이 성공한지 판단한다. |
| 10 | 이 use case는 회원가입이 성공하면 끝난다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 2 | 2a. 이메일 중복으로 회원가입에 실패한다. <br> 2a1. 이메일 중복 메시지를 보여준다. |
| 4 | 4a. 닉네임 중복으로 회원가입에 실패한다. <br> 2a1. 닉네임 중복 메시지를 보여준다. |
| 6 | 6a. 비밀번호와 비밀번호 확인 입력 필드 값이 달라 회원가입에 실패한다. <br> 2a1. 비밀번호와 비밀번호 확인 입력 필드 값이 다르다는 메시지를 보여준다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 사용자당 1번 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #3 로그인
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** |  시스템 기능을 사용하고자 하는 사용자가 이메일 주소, 비밀번호를 입력하여 로그인을 한다.  |
| **Scope** | STARLET System |
| **Level** | User level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 사용자는 회원가입이 되어있어야 한다. <br> 사용자는 현재 로그인되지 않은 상태여야 한다. |
| **Trigger** | 1. 사용자가 홈 화면에서 로그인(Sign in)을 누를 때 <br> 2. 사용자가 회원가입 페이지에서 SIGN IN을 누를 때  |
| **Success Post Condition** | 사용자는 로그인에 성공하여 시스템의 모든 기능을 사용할 수 있다.  |
| **Failed Post Condition** | 사용자는 로그인에 실패하여 시스템의 회원가입을 제외한 모든 기능을 사용할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자가 로그인을 한다.  |
| 1 |  사용자는 홈 화면 또는 회원가입 페이지 하단의 SIGN IN 을 눌러 로그인 페이지에 진입한다. |
| 2 |  사용자는 이메일과 비밀번호를 입력 후 LOGIN 버튼을 누른다.  |
| 3 |  시스템은 사용자 정보를 체크하여 로그인 성공 유무를 판단한다. |
| 4 |  시스템은 등록된 사용자라면 로그인에 성공하고 로그인 완료된 사용자의 홈 화면을 제공한다. |


#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 3 | 3a. 로그인에 실패한다. <br> 3a1. 이메일 또는 비밀번호 둘 중 하나라도 입력하지 않고 LOGIN 버튼을 클릭 시 오류 메시지를 출력한다 <br> 3a2. 등록되지 않는 정보면 로그인 실패 메시지를 출력한다.  |


#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #4 비밀번호 찾기
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** |  시스템 기능을 사용하고자 하는 사용자가 비밀번호를 재설정 한다.  |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 사용자는 회원가입이 되어있어야 한다. <br> 사용자는 현재 로그인되지 않은 상태여야 한다. |
| **Trigger** | 사용자가 로그인 화면에서 비밀번호 찾기를 누를 때  |
| **Success Post Condition** | 사용자는 비밀번호를 재설정할 수 있다.  |
| **Failed Post Condition** | 사용자는 비밀번호 재설정에 실패하여 로그인을 할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자가 비밀번호를 재설정한다.  |
| 1 |  사용자는 로그인 화면에서 비밀번호 찾기를 눌러 비밀번호를 제설정하는 페이지에 진입한다. |
| 2 |  사용자는 가입한 이메일 주소를 입력 후 비밀번호 재설정 메일 보내기를 클릭한다.  |
| 3 |  시스템은 사용자 이메일을 체크하여 이메일 존재 여부를 판단한다. |
| 4 |  사용자는 입력한 이메일 주소 메일함에서 시스템에서 전송된 이메일 확인 버튼을 클릭한다.  |
| 5 |  사용자는 시스템으로 돌아와 인증 상태 확인 버튼을 클릭한다.  |
| 6 |  인증 완료된 사용자라면 비밀번호, 비밀번호 확인을 입력 후 비밀번호 변경을 클릭한다.  |
| 7 |  시스템은 비밀번호가 변경된 사용자라면 로그인 화면을 제공한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 2 | 2a. 비밀번호 재설정 메일 보내기를 실패한다. <br> 2a1. 가입되지 않은 이메일로 비밀번호 재설정 메일 보내기를 클릭 시 오류 메시지를 출력한다 <br> 2a2. 이메일 입력 형식이 맞지 않으면 오류 메시지를 출력한다.  |
| 4 | 4a. 이메일 인증상태 확인을 실패한다. <br> 4a1. 사용자가 자신의 메일함에서 인증 확인 버튼을 클릭하지 않고 인증 상태 확인 버튼을 클릭했을 경우 오류 메시지를 출력한다.  |
| 6 | 6a. 비밀번호 재설정을 실패한다. <br> 6a1. 사용자가 새 비밀번호와 새 비밀번호 확인 입력 필드값을 다르게 입력했을 경우, 오류 메시지를 출력한다. <br> 6a2. 비밀번호 조건과 맞지 않을 경우, 오류 메시지를 출력한다. |


#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #5 한/영 변환 토글
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** |  모든 사용자는 홈 화면의 언어 토글을 통해 한국어와 영어 중 원하는 언어로 UI를 바꿀 수 있다.  |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 사용자는 홈 화면에 진입한 상태여야한다. |
| **Trigger** | 사용자가 홈 화면에서 Select Language 를 누를 때  |
| **Success Post Condition** | 사용자는 한국어와 영어 중 원하는 언어로 UI를 바꿀 수 있다.  |
| **Failed Post Condition** | 사용자는 한국어와 영어 중 원하는 언어로 UI를 바꿀 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 한국어와 영어 중 원하는 언어로 UI를 바꿀 수 있다.  |
| 1 |  사용자는 홈 화면에서 Select Language 버튼을 누른다. |
| 2 |  1. 사용자가 KR 한국어로 선택 할 시 홈 화면의 기능에 대한 주제들이 한국어로 변경된다. <br> 2. 사용자가 KR 한국어로 선택 할 시 사이드바를 열었을 때 나타나있는 기능들이 한국어로 변경된다. |
| 3 |  1. 사용자가 US 영어로 선택 할 시 홈 화면의 기능에 대한 주제들이 영어어로 변경된다. <br> 2. 사용자가 US 영어로 선택 할 시 사이드바를 열었을 때 나타나있는 기능들이 영어로 변경된다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 네트워크 또는 통신에 문제가 있는 경우 <br> 1a1. 이용자는 어떠한 화면도 볼 수 없다. |


#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #6 감정 일기 작성
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** |  로그인한 사용자는 캘린더 페이지로 진입하여 사용자 감정 일기를 작성 후 그 감정에 맞는 별을 받을 수 있다.  |
| **Scope** | STARLET System |
| **Level** | User level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br> 2.사용자는 calendar 페이지에 진입한 상태여야한다. |
| **Trigger** | 사용자에서 홈 화면 또는 네브바에서 My Diary(나의 일기)를 누를 때  |
| **Success Post Condition** | 사용자는 달력에서 클릭한 날짜의 일기를 작성 후 감정에 맞는 별을 받을 수 있다.  |
| **Failed Post Condition** | 1. 사용자는 달력에서 클릭한 날짜의 일기를 작성할 수 없다. <br> 2. 사용자는 작성한 일기에 맞는 감정 별을 받을 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 달력에서 클릭한 날짜에 감정 일기를 작성한 후 별을 받는다.  |
| 1 |  사용자는 홈 화면 또는 사이드바에서 My Diary(나의 일기)를 누른다. |
| 2 |  사용자는 일기를 작성하고자하는 달로 이동한다.  |
| 3 |  사용자는 일기작성을 원하는 날짜를 선택한다. |
| 4 |  사용자는 감정 선택창에서 감정을 선택한다.  |
| 5 |  사용자는 감정 요인 태그 선택창에서 감정 요인 태그를 1개 이상 선택한다.  |
| 6 |  사용자는 감정에 맞는 별을 부여받고, 일기를 작성할 수 있다.  |
| 6 |  사용자는 완료버튼을 누르고 밤하늘 페이지로 이동하는 모달창에서 예를 누를 경우 밤하늘 페이지로 이동하고, 아니요를 누를 경우 캘린더 페이지로 이동한다.  |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 2 | 2a 캘린더 로딩 실패 2a1. 네트워크 및 서버 오류로 캘린더가 표시되지 않는다. 오류 메시지를 제공한다. |
| 4 | 4a. 감정을 선택하지 않은 경우 <br> 4a1. 사용자는 일기를 작성할 수 없다. |
| 5 | 5a. 감정 요인을 선택하지 않은 경우 <br> 5a1. 사용자는 일기를 작성할 수 없다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #7 감정 일기 및 감정별 조회
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** |  로그인한 사용자는 캘린더 페이지로 진입하여 자신이 작성한 감정 일기와 감정 별을 조회할 수 있다.  |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br> 2. 사용자는 감정 일기를 작성한 상태여야한다. |
| **Trigger** | 1. 사용자가 캘린더 페이지에서 감정 일기를 작성한 달로 진입했을 때 <br> 2. 사용자가 캘린더에서 감정일기를 작성한 날짜를 선택했을 때 |
| **Success Post Condition** | 사용자는 해당 날짜의 감정 별과 일기를 조회할 수 있다.  |
| **Failed Post Condition** | 사용자는 해당 날짜의 감정 별과 일기를 조회할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 캘린더에서 감정일기를 작성한 날짜의 일기와 감정별을 조회한다.  |
| 1 |  사용자는 홈 화면 또는 사이드바에서 My Diary(나의 일기)를 누른다. |
| 2 |  사용자는 감정 일기와 감정 별 조회를 원하는 날짜의 달로 이동한다.  |
| 3 |  사용자는 해당 달에서 감정 별을 조회한다.  |
| 4 |  사용자는 해당 달/원하는 날짜를 클릭하여 그 안의 일기 내용과 감정 별, 감정 요인 태그를 조회한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 2 | 2a 캘린더 로딩 실패 2a1. 네트워크 및 서버 오류로 캘린더가 표시되지 않는다. 오류 메시지를 제공한다. |
| 3 | 3a 선택한 달에 일기가 없는 경우 3a1. 캘린더에는 아무 별도 표시되지 않으며 일기를 조회 할 수 없다. |


#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |


###  Use Case #8 감정 일기 내용 수정
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** |  로그인한 사용자가 기존에 작성한 특정 날짜의 감정일기 내용을 수정할 수 있다.   |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br> 2. 사용자는 감정 일기를 작성한 상태여야한다. |
| **Trigger** | 1. 사용자가 캘린더 페이지에서 감정 일기를 작성한 달로 진입했을 때 <br> 2. 사용자가 캘린더에서 감정일기를 작성한 날짜를 선택했을 때 |
| **Success Post Condition** | 사용자는 해당 날짜의 감정 별과 일기를 수정할 수 있다.  |
| **Failed Post Condition** | 사용자는 해당 날짜의 감정 별과 일기를 수정할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 캘린더에서 원하는 날짜를 선택하여 감정 일기 내용을 수정한다.  |
| 1 |  사용자는 홈 화면 또는 사이드바에서 My Diary(나의 일기)를 누른다. |
| 2 |  사용자는 감정 일기 수정을 원하는 날짜의 달로 이동한다.  |
| 3 |  사용자는 해당 달에서 수정을 원하는 일을 선택하여 누른다. |
| 4 |  사용자는 감정 일기 내용을 수정한다. |
| 5 |  사용자는 완료을 누른다. |
| 6 |  시스템은 사용자가 수정한 감정일기 내용을 반영한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 2 | 2a 캘린더 로딩 실패 2a1. 네트워크 및 서버 오류로 캘린더가 표시되지 않는다. 오류 메시지를 제공한다. |
| 3 | 3a 선택한 달에 일기가 없는 경우 3a1. 캘린더에는 아무 별도 표시되지 않으며 일기를 수정 할 수 없다. |


#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #9 별자리 생성
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** |  로그인한 사용자가 밤하늘 페이지에서 자신이 가진 별들을 선택해 별자리를 생성한다. 생성된 별자리게 밤하늘 페이지에 표시된다.   |
| **Scope** | STARLET System |
| **Level** | User level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br> 2. 사용자는 7개 이상의 별을 가진 상태여아한다. <br> 3. 밤하늘 페이지에 진입한 상태여한다. |
| **Trigger** | 1. 사용자가 홈화면 또는 사이드바에서 Night Sky Page(밤하늘 페이지)를 눌렀을 때 <br> 2. 사용자가 My Diary(나의 일기)에서 일기 작성후 밤하늘 페이지로 이동하는 모달창에서 예를 눌렀을 때  |
| **Success Post Condition** | 사용자는 소유하고있는 별로 별자리를 생성할 수 있다.  |
| **Failed Post Condition** | 사용자는 소유하고있는 별로 별자리를 생성할 수 없때  |
| **Success Post Condition** | 사용자가 선택한 별자리의 위치와 크기가 변경되어 Night Sky Page(밤하늘 페이지) 화면에 띄어진다.  |
| **Failed Post Condition** | 사용자가 선택한 별자리 위치와 크기가 Night Sky Page(밤하늘 페이지) 화면에 반영이 되지않고, 기존 위치에 기존과 동일한 크기로 저장된다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 별자리를 클릭하여 드래그를 하여 위치를 이동하고, 크기 조정 슬라이더로 선택한 별자리 크기를 변경한 뒤 저장한다.  |
| 1 |  사용자는 홈 또는 사이드바에서 Night Sky Page(밤하늘 페이지)로 이동한다. 또는 My Diary(나의 일기)페이지에서 일기 작성 후 밤하늘 페이지로 이동 여부 모달창에서 예를 클릭했을때 Night Sky Page(발하늘 페이지)로 이동한다. |
| 2 | 사용자는 크기와 위치를 변경하고자하는 별자리를 선택하거나 드래그한다. |
| 3 | 사용자는 원하고자하는 위치에 해당 별자리를 드래그 한 후 적용 버튼을 누른다. |
| 4 | 시스템은 사용자가 적용 버튼을 누른 시점의 위치에 별자리를 저장 후 Night Sky Page(발하늘 페이지)에 표시한다. |
| 5 | 사용자는 별자리 크기 조절 창의 슬라이더를 통해 드래그하여 별자리 크기를 조정 후 적용 버튼을 누른다. |
| 6 | 시스템은 사용자가 적용 버튼을 눌렀을 때의 별자리 크기를 저장 후 Night Sky Page(발하늘 페이지)에 표시한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 2 | 2a. 별자리 로딩 실패 2a1. 네트워크 및 서버 오류로 별이 표시되지 않는다. 오류 메시지를 제공한다. |
| 3 | 3a. 변경 후 적용 버튼을 누르지않고 해당 별자리가 아닌 화면을 클릭 또는 새로고침 했을 경우 3a1. 기존에 있던 별자리 위치와 크기로 유지된다. |


#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #11 별 및 별자리 조회
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** |  로그인한 사용자가 Night Sky Page(밤하늘 페이지)에서 자신이 소유한 별과 별자리를 조회한다. |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br> 2. 사용자는 최소 1개 이상의 별 또는 별자리를 보유하고 있어야한다. |
| **Trigger** | 1. 사용자가 홈화면 또는 사이드바에서 Night Sky Page(밤하늘 페이지)를 눌렀을 때 <br> 2. 사용자가 My Diary(나의 일기)에서 일기 작성후 밤하늘 페이지로 이동하는 모달창에서 예를 눌렀을 때   |
| **Success Post Condition** | 사용자는 자신의 별 및 별자리를 화면에서 확인할 수 있다.  |
| **Failed Post Condition** | 사용자는 자신의 별 및 별자리를 화면에서 확인할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 Night Sky Page(밤하늘 페이지)에서 자신이 소유한 별과 별자리를 확인한다.   |
| 1 |  사용자는 홈 또는 사이드바에서 Night Sky Page(밤하늘 페이지)로 이동한다. 또는 My Diary(나의 일기)페이지에서 일기 작성 후 밤하늘 페이지로 이동 여부 모달창에서 예를 클릭했을때 Night Sky Page(발하늘 페이지)로 이동한다. |
| 2 |  시스템은 사용자의 별과 별자리 정보를 조회한다. |
| 3 |  시스템은 2개월 기준으로 별과 별자리를 화면에 랜더링한다. |
| 4 |  사용자는 별자리 선을 호버하여 해당 별자리의 이름과 별자리 생성 시기를 조회한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 2 | 2a. 별자리 및 별 로딩 실패 2a1. 네트워크 및 서버 오류로 별자리 및 별이 표시되지 않는다. 오류 메시지를 제공한다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 2 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #12 별자리 아카이브 조회
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 로그인한 사용자가 자신이 만든 별자리를 Constellation Archive(별자리 아카이브)에서 확인할 수 있다. |
| **Scope** | STARLET System |
| **Level** | User level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br> 2. 사용자는 최소 1개 이상의 별자리를 생성하고 있어야 한다. |
| **Trigger** | 사용자가 홈 화면 또는 사이드바에서 Constellation Archive(별자리 아카이브)를 눌렀을 때   |
| **Success Post Condition** | 사용자는 자신이 생성한 별자리 목록을 시간순으로 조회할 수 있다.  |
| **Failed Post Condition** | 사용자는 자신이 생성한 별자리 목록을 조회할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 Constellation Archive(별자리 아카이브)에서 자신이 만든 별자리 목록을 조회한다.   |
| 1 |  사용자는 홈 또는 사이드 바에서 Constellation Archive(별자리 아카이브)를 클릭한다. |
| 2 |  시스템은 사용자 정보를 바탕으로 생성한 별자리 목록을 조회한다. |
| 3 |  시스템은  한 화면에 최대 4개의 별자리를 시간순으로 표시한다. |
| 4 |  사용자는 별자리의 생성시간, 이름, 설명을 조회한다. |
| 5 |  사용자는 “<”, “>” 버튼을 클릭하여 이전 또는 다음페이지로 이동하여 다른 시간대에 생성된 별자리를 조회한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 2 | 2a. 별자리 로딩 실패 2a1. 네트워크 및 서버 오류로 별자리가 표시되지 않는다. 오류 메시지를 제공한다. |
| 3 | 3a. 사용자가 만든 별자리가 없는 경우 3a1. 별자리가 없다는 메시지를 표시한다.  |
| 5 | 5a. 이전 페이지 또는 다음 페이지가 없는 경우 5a1. “<”, “>”이 비활성화된다.  |
#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 2 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #13 별자리 상세 조회
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 로그인한 사용자가 생성한 별자리 상세정보를 조회할 수 있다. |
| **Scope** | STARLET System |
| **Level** | User level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br> 2. 사용자는 최소 1개 이상의 별자리를 생성하고 있어야 한다.  |
| **Trigger** | Constellation Archive(별자리 아카이브)에서 특정 별자리를 클릭할 때   |
| **Success Post Condition** | 사용자는 특정 별자리의 상세정보를 조회할 수 있다.  |
| **Failed Post Condition** | 사용자는 특정 별자리의 상세정보를 조회할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 특정 별자리의 상세 정보를 확인할 수 있다.   |
| 1 |  사용자는 홈 또는 사이드 바에서 Constellation Archive(별자리 아카이브)를 클릭한다. |
| 2 |  use case #12를 실행한다. |
| 3 |  사용자는 상세조회하고자하는 특정 별자리를 클릭한다. |
| 4 |  시스템은 별자리 상세 데이터를 조회한다. |
| 5 |  시스템은 <br> 1. 별자리 생성 일자 <br> 2. 별자리 이름 <br> 3. 별자리 설명 <br> 4. 별자리에 사용된 별과 그에 따른 감정 <br> 4. 해당 별이 생성된 날짜를 랜더링한다.  |
| 6 |  사용자가 별자리 상세 내용을 조회한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 2 | 2a. 별자리 상세 데이터 로딩 실패 2a1. 네트워크 및 서버 오류로 별자리 상세내용이 표시되지 않는다. 오류 메시지를 제공한다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 2 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #14 별자리 정보 수정
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 로그인한 사용자가 별자리 상세 조회 페이지에서 별자리 이름과 소개를 수정한다. |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br> 2. 사용자는 최소 1개 이상의 별자리를 생성하고 있어야 한다.  |
| **Trigger** | 별자리 상세 페이지에서 수정 버튼을 클릭했을 때   |
| **Success Post Condition** | 별자리 이름, 소개가 수정된 정보로 저장되고, 별자리 아카이브와 밤하늘 별자리에 반영된다.  |
| **Failed Post Condition** | 변경 사항이 저장되지 않으며 기존 정보가 유지된다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 별자리 이름과 수정해 저장한다.   |
| 1 |  use case #13 이 실행된다. |
| 2 |  사용자는 별자리 상세 페이지에서 수정 버튼을 클릭한다. |
| 3 |  시스템은 별자리를 수정하는 페이지를 띄운다. |
| 4 |  사용자는 해당 별자리의 이름과 소개를 수정한다. |
| 5 |  사용자는 저장 버튼을 클릭한다.  |
| 6 |  시스템은 사용자가 수정한 정보를 저장하여 별자리 아카이브와 밤하늘 페이지에 반영한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 별자리 상세 데이터 로딩 실패 1a1. 네트워크 및 서버 오류로 별자리 상세내용이 표시되지 않는다. 오류 메시지를 제공한다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 2 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #15 대표 별자리 설정
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 로그인한 사용자가 대표 별자리를 설정할 수 있다. |
| **Scope** | STARLET System |
| **Level** | User levell |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br> 2. 사용자는 최소 1개 이상의 별자리를 생성하고 있어야 한다.  |
| **Trigger** | Constellation Archive(별자리 아카이브)에서 별자리 옆 즐겨찾기 버튼을 클릭했을때    |
| **Success Post Condition** |선택한 별자리가 대표 별자리로 설정되고 즐겨찾기 버튼이 활성화되어 표시된다.  |
| **Failed Post Condition** | 대표 별자리 설정이 이루어지지 않으며, 즐겨찾기 버튼이 활성화되지 않는다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 Constellation Archive(별자리 아카이브)에서 즐겨찾기 버튼을 눌러 대표 별자리를 설정한다.   |
| 1 |  use case #12 이 실행된다. |
| 2 |  사용자는 별자리 옆 즐겨찾기(별 모양) 버튼을 클릭한다. |
| 3 |  시스템은 대표별자리 설정 확인 모들창을 표시한다. |
| 4 |  사용자는 예를 선택한다. |
| 5 |  시스템은 해당 별자리를 대표 별자리로 설정한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 4 | 4a. 아니요를 눌렀을 경우 4a1. 해당 별자리는 대표별자리로 생성되지 않으며 기존을 유지한다. |
| 5 | 5a. 이미 다른 대표 별자리가 있을 경우 5a1. 사용자가 즐겨찾기 버튼을 누른 별자리로 대표 별자리가 변경된다. |
#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #16 마이페이지 조회
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 로그인한 사용자가 자신의 정보(닉네임, 레벨, 대표 별자리)와 활동 통계(월별 감정 통게, 연도별 별자리 생성수, 기록된 별, 생성한 별자리)를 조회할 수 있다. |
| **Scope** | STARLET System |
| **Level** | User level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. |
| **Trigger** |  사용자가 사이드바에서 My Page(마이페이지)를 클릭했을 때   |
| **Success Post Condition** |사용자는 자신의 정보와 해당 시스템 내의 활동 통계 및 대표별자리를 조회할 수 있다.  |
| **Failed Post Condition** | 사용자는 자신의 정보와 해당 시스템 내의 활동 통계 및 대표별자리를 조회할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 My Page(마이페이지)에서 자신의 정보 및 활동 통계, 대표별자리를 확인한다.   |
| 1 |  사용자는 사이드바에서 My Page(마이페이지)를 클릭한다. |
| 2 |  시스템은 사용자 데이터를 조회한다 |
| 3 |  시스템은 My Page(마이페이지)에 다음과 같은 항목을 표시한다 <br> 1. 사용자 닉네임 <br> 2. 사용자 레벨 <br> 3. 사용자가 설정한 대표 별자리 <br> 4. 월별감정통계 <br> 5. 연도별 별자리 생성수 <br> 6. 기록된 별 <br> 7. 생성한 별자리 <br> 8. 사용자 레벨 척도  |
| 4 |  사용자는 데이터 정보를 조회할 수 있다. |


#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 로그인 하지않은 사용자일 경우 1a1. 해당 페이지에 접근이 불가능하다. |
| 2 | 2a. 사용자 데이터 로딩 실패 2a1.  네트워크 및 서버 오류로 사용자 정보가 표시되지 않는다. 오류 메시지를 제공한다. |
| 3 | 3a. 사용자가 설정한 대표별자리가 없을 경우 3a1. 가장 최근 만들어진 별자리를 랜더링한다 3a2. 별자리 자체가 존재하지 않는 경우 오류메시지를 표시한다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 2 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #17 프로필 수정
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 로그인한 사용자가 자신의 프로필 정보(사진, 닉네임)을 수정할 수 있다. |
| **Scope** | STARLET System |
| **Level** | User level |
| **Scope** | STARLET System |
| **Author** |  |
| **Last Update** |  |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. |
| **Trigger** |  사용자가 사이드바에서 My Page(마이페이지)를 클릭했을 때   |
| **Success Post Condition** |사용자는 자신의 프로필 정보(사진, 닉네임)을 수정할 수 있다.  |
| **Failed Post Condition** | 사용자는 자신의 프로필 정보(사진, 닉네임)을 수정할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 My Page(마이페이지)에서 자신의 프로필 정보(사진, 닉네임)을 수정한다.   |
| 1 |  사용자는 사이드바에서 My Page(마이페이지)를 클릭한다. |
| 2 |  시스템은 사용자 데이터를 조회한다 |
| 3 |  사용자는 프로필 편집 버튼을 클릭한다.  |
| 4 |  시스템은 현재 프로필을 랜더링한다. |
| 5 |  사용자는 현재 프로필을 클릭하여 새로운 프로필을 local에서 선택 후 확인을 누른다. |
| 6 |  사용자는 새로운 닉네임을 입력한다. |
| 7 |  사용자가 중복 확인 버튼을 클릭한다. |
| 8 |  시스템은 사용자 닉네임 중복 여부를 검사한다. |
| 8 |  사용자가 완료 버튼을 클릭한다. |
| 9 |  사용자가 입력한 내용에 맞게 사용자 플필 정보(사진,닉네임)이 바뀐다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 로그인 하지않은 사용자일 경우 1a1. 해당 페이지에 접근이 불가능하다. |
| 2 | 2a. 사용자 데이터 로딩 실패 2a1.  네트워크 및 서버 오류로 사용자 정보가 표시되지 않는다. 오류 메시지를 제공한다. |
| 7 | 7a. 닉네임 중복일 경우 7a1. 닉네임 중복여부에 대한 오류 메시지를 표시한다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #18 AI 별자리 이름 및 설명 제공
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 별자리 모형까지 만든 사용자가 별자리 이름 및 설명을 AI를 통해 추천받을 수 있다. |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** | 조민서 |
| **Last Update** | 2025-12-11 |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br/> 2. 사용자는 별자리 모형을 만든 상태여야한다. |
| **Trigger** |  1. 사용자가 별자리 생성 모달창에서 추천받기 버튼을 클릭했을 때  |
| **Success Post Condition** | 사용자는 별자리 이름 및 설명을 AI에게 추천받을 수 있다.  |
| **Failed Post Condition** | 사용자는 별자리 이름 및 설명을 AI에게 추천받을 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 별자리 생성 모달창에서 별자리 이름 및 추천을 AI에게 추천받는다.   |
| 1 |  사용자는 홈 화면 또는 사이드바에서 NIGHT SKY(밤하늘 별자리)를 클릭한다. |
| 2 |  시스템은 별을 랜더링한다. |
| 3 |  사용자는 별(7개~14개)를 선택하여 Generate을 클릭한다. |
| 4 |  사용자는 별들을 이어 별자리 모형을 만든 후 다음을 클릭한다. |
| 5 |  사용자는 추천받기를 클릭한다. |
| 6 |  시스템은 별자리 이름 및 설명을 입력 필드에 자동으로 채운다. |
| 7 |  사용자는 AI가 채운 별자리 이름 및 설명으로 별자리를 만든다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 로그인 하지않은 사용자일 경우 1a1. 해당 페이지에 접근이 불가능하다. |
| 2 | 2a. 사용자 데이터 로딩 실패 2a1.  네트워크 및 서버 오류로 사용자 정보가 표시되지 않는다. 오류 메시지를 제공한다. |
| 5 | 5a. (?) 아이콘에 에 커서를 둔 경우 5a1. 추천받기 기능이 어떠한 기능인지 알 수 있다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 2 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #19 친구 검색
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | STARLET 사용자를 검색할 수 있다. |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** | 조민서 |
| **Last Update** | 2025-12-11 |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. |
| **Trigger** |  1. 사용자가 친구 추가 버튼을 클릭하여 STARLET 사용자 닉네임을 입력 후 Enter 혹은 돋보기 아이콘을 눌렀을 때 |
| **Success Post Condition** | 사용자는 해당 닉네임 사용자를 검색할 수 있다.  |
| **Failed Post Condition** | 사용자는 해당 닉네임 사용자를 검색할 수 없다.  |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 친구 목록 페이지에서 사용자 닉네임을 통해 다른 사용자를 검색할 수 있다.   |
| 1 |  사용자는 마이페이지에서 닉네임 오른쪽 n명의 친구를 클릭한다. |
| 2 |  사용자의 친구 목록 페이지로 이동한다. |
| 3 |  사용자는 친구 추가 버튼을 클릭한다. |
| 4 |  사용자는 검색하고자하는 사용자의 닉네임을 입력한다. |
| 5 |  시스템은 해당 닉네임을 가진 사용자를 랜더링한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 로그인 하지않은 사용자일 경우 1a1. 해당 페이지에 접근이 불가능하다. <br/> 2b. 사용자 데이터 로딩 실패 2b1.  네트워크 및 서버 오류로 사용자 정보가 표시되지 않는다. 오류 메시지를 제공한다. |
| 5 | 5a. 해당 닉네임을 가진 사용자가 없는 경우 5a1. 오류 메시지를 제공한다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #20 친구 신청
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | STARLET 사용자를 친구 신청할 수 있다. |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** | 조민서 |
| **Last Update** | 2025-12-11 |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. |
| **Trigger** | 사용자가 친구 검색 모달창에서 닉네임 입력 후 친구 신청을 눌렀을 때. |
| **Success Post Condition** | 사용자는 해당 닉네임 사용자에게 친구 신청을 할 수 있다. |
| **Failed Post Condition** | 사용자는 해당 닉네임 사용자에게 친구 신청을 할 수 없다.  |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 친구 목록 페이지에서 친구 신청을 할 수 있다.   |
| 1 |  사용자는 마이페이지에서 닉네임 오른쪽 n명의 친구를 클릭한다. |
| 2 |  사용자의 친구 목록 페이지로 이동한다. |
| 3 |  사용자는 친구 추가 버튼을 클릭한다. |
| 4 |  사용자는 검색하고자하는 사용자의 닉네임을 입력한다. |
| 5 |  시스템은 해당 닉네임을 가진 사용자를 랜더링한다. |
| 6 |  사용자는 친구 신청을 누른다. |
| 7 |  시스템은 사용자가 친구 신청한 버튼을 신청 완료로 바꾼다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 로그인 하지않은 사용자일 경우 1a1. 해당 페이지에 접근이 불가능하다. <br/> 2b. 사용자 데이터 로딩 실패 2b1.  네트워크 및 서버 오류로 사용자 정보가 표시되지 않는다. 오류 메시지를 제공한다. |
| 5 | 5a. 해당 닉네임을 가진 사용자가 없는 경우 5a1. 오류 메시지를 제공한다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #21 친구 수락
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 사용자는 자신에게 온 친구 요청을 수락할 수 있다. |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** | 조민서 |
| **Last Update** | 2025-12-11 |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br/> 2. 사용자는 친구 요청을 받은 상태여야한다. |
| **Trigger** | 사용자가 수락 버튼을 클릭하였을 때. |
| **Success Post Condition** | 사용자는 친구 요청을 수락할 수 있다. |
| **Failed Post Condition** | 사용자는 친구 요청을 수락할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 친구 요청 확인 모달창에서 친구 요청을 수락할 수 있다.  |
| 1 |  사용자는 마이페이지에서 닉네임 오른쪽 n명의 친구를 클릭한다. |
| 2 |  사용자의 친구 목록 페이지로 이동한다. |
| 3 |  사용자는 친구 요청 확인하기를 누른다. |
| 4 |  사용자는 자신에게 온 친구 요청을 확인한다. |
| 5 |  사용자는 수락하기를 누른다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 로그인 하지않은 사용자일 경우 1a1. 해당 페이지에 접근이 불가능하다. <br/> 2b. 사용자 데이터 로딩 실패 2b1.  네트워크 및 서버 오류로 사용자 정보가 표시되지 않는다. 오류 메시지를 제공한다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #22 친구 거절
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 사용자는 자신에게 온 친구 요청을 거절할 수 있다. |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** | 조민서 |
| **Last Update** | 2025-12-11 |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br/> 2. 사용자는 친구 요청을 받은 상태여야한다. |
| **Trigger** | 사용자가 거절 버튼을 클릭하였을 때. |
| **Success Post Condition** | 사용자는 친구 요청을 거절할 수 있다. |
| **Failed Post Condition** | 사용자는 친구 요청을 거절할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 친구 요청 확인 모달창에서 친구 요청을 거절할 수 있다.  |
| 1 |  사용자는 마이페이지에서 닉네임 오른쪽 n명의 친구를 클릭한다. |
| 2 |  사용자의 친구 목록 페이지로 이동한다. |
| 3 |  사용자는 친구 요청 확인하기를 누른다. |
| 4 |  사용자는 자신에게 온 친구 요청을 확인한다. |
| 5 |  사용자는 거절하기를 누른다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 로그인 하지않은 사용자일 경우 1a1. 해당 페이지에 접근이 불가능하다. <br/> 2b. 사용자 데이터 로딩 실패 2b1.  네트워크 및 서버 오류로 사용자 정보가 표시되지 않는다. 오류 메시지를 제공한다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #23 친구 조회
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 사용자는 친구를 조회할 수 있다. |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** | 조민서 |
| **Last Update** | 2025-12-11 |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. |
| **Trigger** | 사용자가 마이페이지 닉네임 오른쪽 n명의 친구를 눌렀을 때 |
| **Success Post Condition** | 사용자는 친구 조회를 할 수 있다. |
| **Failed Post Condition** | 사용자는 친구 조회를 할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 친구 목록 페이지에서 친구 정보(닉네임, 프로필, level, 별 개수, 별자리 개수)를 확인할 수 있다.  |
| 1 |  사용자는 마이페이지에서 닉네임 오른쪽 n명의 친구를 클릭한다. |
| 2 |  사용자의 친구 목록 페이지로 이동한다. |
| 3 |- 시스템은 사용자와 연결된 친구를 랜더링한다. |


#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 로그인 하지않은 사용자일 경우 1a1. 해당 페이지에 접근이 불가능하다. <br/> 2b. 사용자 데이터 로딩 실패 2b1.  네트워크 및 서버 오류로 사용자 정보가 표시되지 않는다. 오류 메시지를 제공한다. |
| 3 | 3a. 친구가 없는 경우 3a1. 친구가 없다는 것에 대한 메시지를 제공한다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #24 친구 삭제
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 사용자는 친구를 삭제할 수 있다. |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** | 조민서 |
| **Last Update** | 2025-12-11 |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br/> 2. 사용자는 1명 이상의 친구가 있는 상태여야한다. |
| **Trigger** | 사용자가 친구 목록 페이지에서 삭제하고자하는 친구 행의 쓰레기통 아이콘을 클릭하였을때  |
| **Success Post Condition** | 사용자는 친구 삭제를 할 수 있다. |
| **Failed Post Condition** | 사용자는 친구 삭제를 할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 친구를 삭제할 수 있다.  |
| 1 |  사용자는 마이페이지에서 닉네임 오른쪽 n명의 친구를 클릭한다. |
| 2 |  사용자의 친구 목록 페이지로 이동한다. |
| 3 | 시스템은 사용자와 연결된 친구를 랜더링한다. |
| 4 | 사용자는 삭제하고자하는 친구 행의 쓰레기통 아이콘을 클릭한다. |
| 5 | 시스템은 친구를 삭제할 것인지 확인하는 alert 창을 표시한다. |
| 6 | 사용자가 확인을 누른다. |
| 7 |  해당 친구가 삭제된다. |
#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 로그인 하지않은 사용자일 경우 1a1. 해당 페이지에 접근이 불가능하다. <br/> 2b. 사용자 데이터 로딩 실패 2b1.  네트워크 및 서버 오류로 사용자 정보가 표시되지 않는다. 오류 메시지를 제공한다. |
| 3 | 3a. 친구가 없는 경우 3a1. 친구가 없다는 것에 대한 메시지를 제공한다. |
| 6 | 6a. 취소를 누를 경우 6a1. 친구가 삭제되지 않는다. |
#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 1 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |

###  Use Case #25 한달 일기 분석
#### GENERAL CHARACTERISTICS

|  |  |
|:---|:---|
| **Summary** | 한 달 기준 작성한 일기 내용을 분석하여 한달 일기 요약을 제공한다. |
| **Scope** | STARLET System |
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Author** | 조민서 |
| **Last Update** | 2025-12-11 |
| **Status** |  |
| **Primary Actor** | User |
| **Preconditions** | 1. 사용자는 로그인된 상태여야한다. <br/> 2. 분석하고자하는 달에 사용자는 1개 이상 일기를 작성한 상태여야한다.  |
| **Success Post Condition** | 사용자는 한 달 일기 분석을 조회할 수 있다. |
| **Failed Post Condition** | 사용자는 한 달 일기 분석을 조회할 수 없다. |

#### MAIN SUCCESS SCENARIO
| Step | Action |
|:---|:---|
| S | 사용자는 한 달 일기 분석을 조회할 수 있다.  |
| 1 |  사용자는 사이드 바 혹은 홈 화면에서 DIARY(나의 일기) 를 누른다. |
| 2 |  사용자는 ```/calendar``` 페이지로 이동한다. |
| 3 | 시스템은 사용자 데이터를 랜더링한다. |
| 4 | 사용자는 상단 말풍선 아이콘을 누른다. |
| 5 | 시스템은 해당 달 일기를 바탕으로 일기 요약을 제공한다. |

#### EXTENSION SCENARIO
| Step | Branching Action |
|:---|:---|
| 1 | 1a. 로그인 하지않은 사용자일 경우 1a1. 해당 페이지에 접근이 불가능하다. <br/> 2b. 사용자 데이터 로딩 실패 2b1.  네트워크 및 서버 오류로 사용자 정보가 표시되지 않는다. 오류 메시지를 제공한다. |
| 4 | 4a. 해당 달의 일기가 없는 경우 4a1. 일기가 없다는 메시지를 제공한다. |

#### RELATED INFORMATION
|  |  |
|:---|:---|
| Performance | ≤ 2 seconds |
| Frequency | 제한없음 |
| Concurrency | 제한없음 |
| Due Date | |
