# Starlet: 소프트웨어 설계 명세서 (SDS)

---

## 6. User Interface Prototype

## 6.1. 로그인

![그림: 로그인](./User%20interface%20prototype%20image/image-login.png)

> 위 그림은 로그인 화면이다.  
> 이메일과 비밀번호를 입력하여 로그인을 할 수 있다.  
> 하단의 ‘가입하기’, ‘비밀번호 찾기’, ‘HOME’ 버튼을 클릭하여 각각 회원가입, 비밀번호 찾기 화면과 홈 화면으로 이동할 수 있다.

---

## 6.2. 회원가입

![그림: 회원가입](./User%20interface%20prototype%20image/image-signup.png)

> 위 그림은 회원가입 화면이다.  
> 이메일 주소, 닉네임, 비밀번호, 비밀번호 확인을 입력하여 회원가입할 수 있다.  
> 이메일 주소와 닉네임은 중복 확인 기능을 통해 중복을 방지한다.
> 하단의 'SIGNIN', 'HOME' 버튼을 클릭하여 로그인 화면 또는 홈 화면으로 이동할 수 있다.

---

## 6.3. 비밀번호 찾기

![그림: 비밀번호 찾기](./User%20interface%20prototype%20image/image-findpw.png)

> 위 그림은 비밀번호 찾기 화면이다.  
> 가입한 이메일 주소를 입력하면 비밀번호 재설정 메일을 받을 수 있다.  
> '로그인으로 돌아가기' 버튼을 클릭하면 로그인 화면으로 이동할 수 있다.

---

## 6.4. 홈화면

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-home-before-eng.png" width="100%" alt="홈화면(로그인 전) - 영어">
  <br>
  <sub>홈 화면(로그인 전) - 영어</sub>
</p>

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-home-before-kor.png" width="100%" alt="홈화면(로그인 후) - 한국어">
  <br>
  <sub>홈 화면(로그인 전) - 한국어</sub>
</p>

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-home-after-eng.png" width="100%" alt="홈화면(로그인 후) - 영어">
  <br>
  <sub>홈 화면(로그인 후) - 영어</sub>
</p>

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-home-after-kor.png" width="100%" alt="홈화면(로그인 후) - 한국어">
  <br>
  <sub>홈 화면(로그인 후) - 한국어</sub>
</p>

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-home1-eng.png" width="100%" alt="홈화면(공통) - 영어">
  <br>
  <sub>홈 화면(공통) - 영어</sub>
</p>

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-home2-eng.png" width="100%" alt="홈화면(공통) - 영어">
  <br>
  <sub>홈 화면(공통) - 영어</sub>
</p>

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-home3-eng.png" width="100%" alt="홈화면(공통) - 영어">
  <br>
  <sub>홈 화면(공통) - 영어</sub>
</p>

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-home1-kor.png" width="100%" alt="홈화면(공통) - 한국어">
  <br>
  <sub>홈 화면(공통) - 한국어</sub>
</p>

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-home2-kor.png" width="100%" alt="홈화면(공통) - 한국어">
  <br>
  <sub>홈 화면(공통) - 한국어</sub>
</p>

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-home3-kor.png" width="100%" alt="홈화면(공통) - 한국어">
  <br>
  <sub>홈 화면(공통) - 한국어</sub>
</p>

> 위 그림은 로그인 전, 후의 영어/한국어 언어 변환 화면이다.  
> 로그인 전에는 로그인과 회원가입을 할 수 있는 버튼이 있다.
> 로그인 후에는 홈 화면의 4가지 버튼을 통해 해당 페이지로 이동할 수 있다.
> 상단의 언어 변경 탭을 통해 한국어/영어로 전환이 가능하다.

---

## 6.5. 사이드바

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-sidebar-before.png" width="100%" alt="사이드바(로그인 전)">
  <br>
  <sub>사이드바(로그인 전)</sub>
</p>

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-sidebar-after-eng.png" width="100%" alt="사이드바(로그인 후) - 영어">
  <br>
  <sub>사이드바(로그인 후) - 영어</sub>
</p>

<p align="center">
  <img src="./User%20interface%20prototype%20image/image-sidebar-after-kor.png" width="100%" alt="사이드바(로그인 후) - 한국어">
  <br>
  <sub>사이드바(로그인 후) - 한국어</sub>
</p>

> 위 그림은 사이드바 화면이다.  
> 로그인 전에는 사이드바에 아무것도 나타나지 않는다.
> 로그인 후에는 사이드바를 통해 각 화면으로 이동하거나 로그아웃할 수 있다.

---

## 6.6. 나의 일기

### 6.6.1 달력

![그림: 달력](./User%20interface%20prototype%20image/image-calendar.png)

> 위 그림은 달력 화면이다.  
> ‘<’, ‘>’ 버튼으로 전월/다음 달로 이동하며 작성된 일기를 확인할 수 있다.

---

### 6.6.2 감정 및 태그 선택

![그림: 감정 및 태그 선택](./User%20interface%20prototype%20image/image-emotion-tag.png)

> 달력에서 별이 없는 빈 날짜를 클릭하면 나타난다.  
> 하나의 감정과 1개 이상의 태그를 선택할 수 있다.

---

### 6.6.3 일기 작성

![그림: 일기 작성](./User%20interface%20prototype%20image/image-diary-write.png)

> 감정 및 태그 선택 화면에서 ‘다음’ 버튼을 누르면 나타난다.  
> 선택한 감정과 태그가 표시되며, 일기는 최소 15자 이상으로 작성해야 한다.

---

### 6.6.4 일기 작성 완료 모달

![그림: 일기 작성 완료 모달](./User%20interface%20prototype%20image/image-diary-confirm-modal.png)

> 일기 작성 후 ‘완료’ 버튼을 누르면 나타난다.  
> ‘예’를 누르면 밤하늘 화면으로 이동, ‘아니요’를 누르면 달력으로 돌아간다.

---

### 6.6.5 작성한 일기

![그림: 작성한 일기](./User%20interface%20prototype%20image/image-diary-view.png)

> 달력에서 별이 생성되어 있는 날짜를 클릭하면 작성된 일기를 확인할 수 있다.  
> 수정 후 ‘완료’를 누르면 수정이 완료된다.

---

### 한 달 일기 요약

![그림: 한 달 일기 요약](./User%20interface%20prototype%20image/image-diary-summary.png)

> 오른쪽 상단의 아이콘을 누르면 해당 달의 일기 요약을 해서 보여준다.

---

## 6.7. 밤하늘 화면

### 6.7.1 밤하늘 화면(별자리 생성 전)

![그림: 밤하늘 화면(별자리 생성 전)](./User%20interface%20prototype%20image/image-starsky-before.png)

> 달력에서 작성한 일기를 기반으로 별과 별자리가 두 달 단위로 표시된다.  
> ‘<’, ‘>’ 버튼으로 전/후 두 달을 이동하며 확인할 수 있다.  
> 별을 원하는 위치로 드래그하여 옮길 수 있다.

---

### 6.7.2 별자리 생성 모달
### 밤하늘 모달 1

![그림: 밤하늘 모달 1)](./User%20interface%20prototype%20image/image-starsky-apply-modal.png)

> 밤하늘 페이지에서 별을 선택할 때 7~14개의 별을 선택하지 않으면 해당 모달이 나타난다.

---

### 별자리 생성 모달

![그림: 별자리 선 잇기 모달](./User%20interface%20prototype%20image/image-constellaion-line-modal.png)

> 밤하늘에서 최소 7개 이상 최대 14개 이하의 별을 선택해야 별자리 생성 모달이 열린다.  
> 선택한 별들의 위치 그대로 화면에 나타나게 되며, 별을 이동하거나 선을 이어 별자리를 만들 수 있다.  
> 마지막 선 지우기 버튼과 전체 삭제 버튼을 통해 선 이은 것을 삭제할 수 있다.
> 바탕 화면을 누르면 모달창이 닫힌다.

---

![그림: 별자리 이름 및 설명 생성 모달](./User%20interface%20prototype%20image/image-constellation-modal.png)

> 오른쪽 입력란에서 별자리 이름과 간단한 설명을 작성 후 ‘완료’ 버튼을 누르면 생성이 완료된다.  
> 별자리 이름은 10자 이내, 설명은 30자 이내로 작성하도록 제한한다.
> 상단 좌측의 '<' 버튼으로 별자리 선 잇기 모달로 돌아갈 수 있다.
> ? 튤팁을 호버하면 AI 추천 기능에 대한 설명을 볼 수 있다.
> 추천받기 버튼을 누르면 입력칸에 이름과 설명을 추천해서 보여준다.

---

### 6.7.3 밤하늘 화면(별자리 생성 후)

![그림: 밤하늘 화면(별자리 생성 후)](./User%20interface%20prototype%20image/image-starsky-after.png)

> 생성된 별자리의 모양 그대로 정해진 일정한 크기로 나타난다..  
> 별자리 간선 또는 별 호버 시 별자리 이름과 생성일자가 적혀있는 라벨이 나타난다.

---

### 6.7.4 별자리 선택(드래그 및 크기 조절)

![그림: 별자리 선택(드래그 및 크기 조절)](./User%20interface%20prototype%20image/image-constellation-resize.png)

> 별자리 선택 시 별자리 이름, 생성일자 라벨과 크기 조절 슬라이드이 나타난다.  
> 슬라이드 위의 원을 위로 올리면 별자리 크기를 키우고 내리면 크기를 줄이며 슬라이드 하단의 체크 아이콘을 누르면 적용된다.
> 드래그 시에도 드래그 후 체크 아이콘을 누르면 저장된다.
> 드래그 이동 후 또는 크기 조절 후 체크 아이콘을 누르지 않고 바탕화면 클릭 시 원래 위치로 돌아간다.

---

### 밤하늘 모달 2

![그림: 밤하늘 모달 2)](./User%20interface%20prototype%20image/image-constellation-confirm-modal.png)

> 별자리 이동 및 크기 조절 후 체크 아이콘을 누르면 모달이 나타난다.

---

## 6.8. 별자리 아카이브

### 6.8.1 별자리 아카이브

![그림: 별자리 아카이브](./User%20interface%20prototype%20image/image-archive.png)

> 지금까지 생성된 별자리 목록이 나타나며 해당 별자리에 따라 별자리 생성일자, 이름, 설명이 표시된다.
> 한 화면에 4개의 별자리를 보여준다.

---

### 6.8.2 별자리 아카이브 상세

![그림: 별자리 아카이브 상세](./User%20interface%20prototype%20image/image-archive-detail.png)

> 보고자 하는 별자리를 클릭하면 상세 페이지로 이동한다.  
> 생성일자, 이름, 설명, 감정 구성을 기본적으로 확인할 수 있다.  
> 내가 남긴 기록보기에서 생성 날짜를 클릭하면 해당 일기가 해당 날짜의 일기를 보여주는 페이지로 이동한다.
> 별자리 아카이브 상세 페이지에서 연필 아이콘을 누르면 수정 페이지로 이동한다.

---

### 별자리 아카이브 수정

![그림: 별자리 아카이브 수정](./User%20interface%20prototype%20image/image-archive-edit.png)

> 별자리 이름과 설명을 수정할 수 있고 '완료'버튼을 누르면 저장된다.

---

### 6.8.3 대표 별자리 설정

![그림: 대표 별자리 설정](./User%20interface%20prototype%20image/image-archive-represent.png)

> 별자리 아카이브의 상단 우측 별 모양을 클릭하면 대표 별자리 설정 모달이 열린다.  
> ‘예’ 버튼을 누르면 대표 별자리로 지정된다.

---

## 6.9. 마이 페이지

### 6.9.1 마이 페이지

![그림: 마이 페이지](./User%20interface%20prototype%20image/image-mypage.png)

> 대표 별자리가 상단 우측에 나타난다.  
> 생성한 별의 수에 따라 레벨이 오르며 호칭을 획득할 수 있다.  
> 하단 그래프에서 감정별 일기 수와 생성된 별자리 수를 한눈에 확인 가능하다.

---

### 6.9.2 프로필 수정

![그림: 프로필 수정](./User%20interface%20prototype%20image/image-profile-edit.png)

> ‘프로필 편집’ 버튼을 누르면 프로필 수정 모달이 나타난다.  
> 프로필 이미지와 닉네임을 변경할 수 있고, 닉네임은 중복 확인을 통해 검증된다.  
> ‘완료’ 버튼을 누르면 수정이 저장된다.

## 6.9. 친구

### 친구 리스트

![그림: 친구 리스트](./User%20interface%20prototype%20image/image-friendlist.png)

> 나와 친구로 맺어진 친구 리스트가 하단에 나타난다.
> 친구 리스트의 우측에 있는 쓰레기통 아이콘을 누르면 친구가 삭제된다.
> '친구 추가'버튼을 누르면 친구 검색 모달이 열린다.
> '친구 요청 확인하기'버튼을 누르면 친구 요청 모달이 열린다.
> 기록된 별과 생성한 별자리 수를 확인할 수 있다.

---

### 친구 검색

![그림: 친구 검색(신청)](./User%20interface%20prototype%20image/image-friend-search.png)

> 이름을 입력 후 돋보기 아이콘을 누르면 하단에 해당 유저가 나타난다.
> 친구 신청을 누르면 친구 신청이 완료된다.

---

![그림: 친구 검색(신청 완료)](./User%20interface%20prototype%20image/image-friend-search.png)

> 친구 신청이 완료되어 '친구 신청'버튼이 신청 완료로 바뀌며 버튼이 비활성화된다.

---

![그림: 친구 검색(이미 친구입니다)](./User%20interface%20prototype%20image/image-friend-search.png)

> 이미 친구인 친구의 이름을 입력 후 돋보기 버튼을 누르면 "이미 친구입니다"라는 문구가 나타나며 버튼이 비활성화된다.

---

### 친구 요청

![그림: 친구 요청](./User%20interface%20prototype%20image/image-friend-request.png)

> 친구 요청이 온 유저들의 리스트를 보여주며 친구 요청을 3일 이내로 받지 않으면 사라진다.
> '수락'버튼을 누르면 친구가 맺어지며 '거절'버튼을 누르면 친구 요청이 거부된다.

---

### 친구 추가 완료

![그림: 친구 추가 완료](./User%20interface%20prototype%20image/image-friendlist-after.png)

> 친구가 맺어진 후 친구 리스트 목록을 나타낸다.
