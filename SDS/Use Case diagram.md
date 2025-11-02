## Use case analysis

## Use case Diagram
(이미지 첨부 예정)

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
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Level** | User level |
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
| **Level** | Subfunction level |
| **Scope** | STARLET System |
| **Level** | User level |
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
