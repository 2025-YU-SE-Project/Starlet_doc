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
