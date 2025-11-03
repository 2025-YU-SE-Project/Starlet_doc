# 6. 사용자 인터페이스 프로토타입 (User Interface Prototype)

---

## 6.1. 로그인

![그림: 로그인](./User%20interface%20prototype%20image/image-login.png)

> 위 그림은 로그인 화면이다.  
> 이메일과 비밀번호를 입력하여 로그인을 할 수 있다.  
> ‘비밀번호 찾기’, ‘HOME’ 버튼을 클릭하여 각각 비밀번호 찾기 화면과 홈 화면으로 이동할 수 있다.

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

<figure>
  <img src="./User%20interface%20prototype%20image/image-home-before.png" width="80%" alt="홈화면(로그인 전)">
  <figcaption align="center"><sub>홈화면(로그인 전)</sub></figcaption>
</figure>

<figure>
  <img src="./User%20interface%20prototype%20image/image-home-after.png" width="80%" alt="홈화면(로그인 후)">
  <figcaption align="center"><sub>홈화면(로그인 후)</sub></figcaption>
</figure>

> 위 그림은 로그인 전, 후의 홈화면이다.  
> 로그인 전에는 상단 오른쪽에 로그인/회원가입 버튼이 있고, 하단의 3가지 버튼을 클릭하면 로그인 페이지로 자동 이동한다.  
> 로그인 후에는 하단의 3가지 버튼이 해당 페이지로 연결된다.
> 상단의 언어 변경 탭을 통해 한국어/영어로 전환이 가능하다.

---

## 6.5. 사이드바

<figure>
  <img src="./User%20interface%20prototype%20image/image-sidebar-before.png" width="80%" alt="사이드바(로그인 전)">
  <figcaption align="center"><sub>사이드바(로그인 전)</sub></figcaption>
</figure>

<figure>
  <img src="./User%20interface%20prototype%20image/image-sidebar-after.png" width="80%" alt="사이드바(로그인 후)">
  <figcaption align="center"><sub>사이드바(로그인 후)</sub></figcaption>
</figure>

> 위 그림은 사이드바 화면이다.  
> 로그인 전에는 미등록 사용자임을 나타낸다.
> 로그인 후에는 각 화면으로 이동하거나 로그아웃할 수 있다.

---

## 6.6. 나의 일기

### 달력

![그림: 달력](./User%20interface%20prototype%20image/image-calendar.png)

> 위 그림은 달력 화면이다.  
> ‘<’, ‘>’ 버튼으로 전월/다음 달로 이동하며 작성된 일기를 확인할 수 있다.  
> ‘< Back’ 버튼을 누르면 이전 페이지로 돌아간다.

---

### 감정 및 태그 선택

![그림: 감정 및 태그 선택](./User%20interface%20prototype%20image/image-emotion-tag.png)

> 달력에서 별이 없는 빈 날짜를 클릭하면 나타난다.  
> 하나의 감정과 1개 이상의 태그를 선택할 수 있다.

---

### 일기 작성

![그림: 일기 작성](./User%20interface%20prototype%20image/image-diary-write.png)

> 감정 및 태그 선택 화면에서 ‘다음’ 버튼을 누르면 나타난다.  
> 선택한 감정과 태그가 표시되며, 일기는 최소 15자 이상으로 작성해야 한다.

---

### 일기 작성 완료 모달

![그림: 일기 작성 완료 모달](./User%20interface%20prototype%20image/image-diary-finish.png)

> 일기 작성 후 ‘완료’ 버튼을 누르면 나타난다.  
> ‘예’를 누르면 밤하늘 화면으로 이동, ‘아니요’를 누르면 달력으로 돌아간다.

---

### 작성한 일기

![그림: 작성한 일기](./User%20interface%20prototype%20image/image-diary-view.png)

> 달력에서 별이 생성되어 있는 날짜를 클릭하면 작성된 일기를 확인할 수 있다.  
> 수정 후 ‘완료’를 누르면 수정이 완료된다.

---

## 6.7. 밤하늘 화면

### 밤하늘 화면(별자리 생성 전)

![그림: 밤하늘 화면(별자리 생성 전)](./User%20interface%20prototype%20image/image-starsky-before.png)

> 달력에서 작성한 일기를 기반으로 별과 별자리가 두 달 단위로 표시된다.  
> ‘<’, ‘>’ 버튼으로 전/후 두 달을 이동하며 확인할 수 있다.  
> 별을 원하는 위치로 드래그하여 옮길 수 있다.

---

### 별자리 생성 모달

![그림: 별자리 생성 모달](./User%20interface%20prototype%20image/image-constellation-modal.png)

> 밤하늘에서 최소 7개 이상 최대 14개 이하의 별을 선택해야 별자리 생성 모달이 열린다.  
> 선택한 별들의 위치 그대로 왼쪽에 나타나게 되며, 별을 이동하거나 선을 이어 별자리를 만들 수 있다.  
> 오른쪽 입력란에서 별자리 이름과 간단한 설명을 작성 후 ‘설정’ 버튼을 누르면 생성이 완료된다.  
> 상단의 '<-' 버튼으로 밤하늘 화면으로 돌아갈 수 있다.

---

### 밤하늘 화면(별자리 생성 후)

![그림: 밤하늘 화면(별자리 생성 후)](./User%20interface%20prototype%20image/image-starsky-after.png)

> 생성된 별자리의 별과 간선이 그대로 나타난다.  
> 별자리 선 위에 마우스를 올리면 별자리 이름과 생성일자가 라벨로 표시된다.

---

### 별자리 선택(드래그 및 크기 조절)

![그림: 별자리 선택(드래그 및 크기 조절)](./User%20interface%20prototype%20image/image-constellation-resize.png)

> 별자리 선택 시 별자리 이름, 생성일자 라벨과 크기 조절 탭이 나타난다.  
> 조절은 0.05 단위로 가능하며 ‘적용’을 버튼을 누르면 저장된다.
> 드래그 시에도 드래그 후 '적용'을 버튼을 누르면 저장된다.
> 드래그 이동 후 또는 크기 조절 후 ‘적용’을 누르지 않고 바탕화면 클릭 시 원래 위치로 돌아간다.

---

## 6.8. 별자리 아카이브

### 별자리 아카이브

![그림: 별자리 아카이브](./User%20interface%20prototype%20image/image-archive.png)

> 지금까지 생성된 별자리 목록이 나타나며 해당 목록에 따라 별자리 생성일자, 이름, 설명이 표시된다.

---

### 별자리 아카이브 상세

![그림: 별자리 아카이브 상세](./User%20interface%20prototype%20image/image-archive-detail.png)

> 원하는 목록을 클릭하면 상세 페이지로 이동한다.  
> 생성일자, 이름, 설명, 감정 구성을 기본적으로 확인할 수 있다.  
> ‘수정’ 버튼을 누르면 이름/설명을 변경할 수 있다.  
> 내가 남긴 기록보기에서 기록을 클릭하면 해당 일기가 생성된 달의 달력으로 이동한다.

---

### 대표 별자리 설정

![그림: 대표 별자리 설정](./User%20interface%20prototype%20image/image-archive-represent.png)

> 별자리 아카이브의 상단 우측 별 모양을 클릭하면 대표 별자리 설정 모달이 열린다.  
> ‘대표 별자리로 설정’ 버튼을 누르면 대표 별자리로 지정된다.

---

## 6.9. 마이 페이지

### 마이 페이지

![그림: 마이 페이지](./User%20interface%20prototype%20image/image-mypage.png)

> 대표 별자리가 상단 우측에 나타난다.  
> 생성한 별의 수에 따라 레벨이 오르며 호칭을 획득할 수 있다.  
> 하단 그래프에서 감정별 일기 수와 별자리 수를 한눈에 확인 가능하다.

---

### 프로필 수정

![그림: 프로필 수정](./User%20interface%20prototype%20image/image-profile-edit.png)

> ‘프로필 편집’ 버튼을 누르면 프로필 수정 모달이 나타난다.  
> 프로필 이미지와 닉네임을 변경할 수 있고, 닉네임은 중복 확인을 통해 검증된다.  
> ‘완료’ 버튼을 누르면 수정이 저장된다.
