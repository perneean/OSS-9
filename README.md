# OSS-9
![레베이스](https://user-images.githubusercontent.com/113653315/201718177-dd8b8565-cb9b-421b-ac38-68f4ad5dcb5f.png)


브랜치를 합치는 방법
- 병합
- **리베이스** : 커밋의 **트리 구조를 재배열**. 커밋을 재배열하는 변경 결과가 병합과 유사.

> 실무에서는 merge 명령어보다 리베이스를 더 선호함

<br>

---

<br>
<img src="https://user-images.githubusercontent.com/113653315/201719788-533442bf-8cd3-4a9d-b3d4-b11d3f4a86df.png" width="500">


- master 브랜치를 제외한 **모든 브랜치에는 뿌리가 있음**.


- 브랜치는 특정 커밋을 가리키는 포인터.


- 가리키는 특정 커밋은 브랜치가 파생된 **기준**이 됨. 

<img src="https://user-images.githubusercontent.com/107173046/201600202-c75b6403-e324-4e98-ab7f-152d27273b4b.png" width="330">

<br>

---

<br>
<img src="https://user-images.githubusercontent.com/113653315/201719860-2c1b77b0-f475-446c-9292-34acea4afab6.png" width="300">


- 리베이스는 파생된 브랜치의 기준이 되는 베이스 커밋을 변경하는 것.

- 변경 이유 : 커밋의 진행 모습을 **단순화** 하기 위해.

- 리베이스는 코드의 **베이스 분기점을 변경**하여 마치 하나의 기찻길처럼 만듦

- 장점 : 여러 갈래로 갈라지지 않아 **커밋의 진행 사항을 좀 더 쉽게 파악**할 수 있음.

<img src="https://user-images.githubusercontent.com/107173046/201601276-dbddcda1-34f9-4c78-9c45-3b0741d26cda.png" width="330">

<br>

---

<br>
<img src="https://user-images.githubusercontent.com/113653315/201719940-4cffec1d-7f93-41d7-8490-ee394fa4d90f.png" width="500">


**병합** : 파생된 두 브랜치를 하나로 합치는 과정. 

병합을 위해선 두 브랜치의 공통 조상 커밋(두 브랜치를 병합하는 베이스 커밋)을 찾아야 함. 

공통 조상 커밋을 찾으면 서로 다르게 커밋이 진행된 두 브랜치를 3-way 방식으로 병합.

<img src="https://user-images.githubusercontent.com/107173046/201601502-214a6f3a-e54e-4dc9-bd52-dac91bb7f88e.png" width="500">

**리베이스** : 두 브랜치를 서로 비교하지 않고 **순차적으로 커밋 병합** 시도.

##### 결합 순서

1. 공통 조상 커밋 찾기 


3. 베이스 커밋을 변경하여 두 브랜치 커밋 위치를 바꾸기
4. 파생된 브랜치의 diff를 임시 공간에 잠시 보관하기
5. master 브랜치의 커밋 1 ~ 커밋 6 까지 진행
6. 기존 베이스 커밋 2 에서 커밋 6 으로 베이스 기준점 변경
7. 마지막 커밋에서 차례로 임시 공간에 저장한 diff를 하나씩 적용
8. 새로운 베이스 기준점을 기반으로 한 브랜치에서 커밋 3 , 커밋 4 를 커밋 6 에서 연장하여 수정 재배치

<img src="https://user-images.githubusercontent.com/107173046/201601979-aa1280be-552d-4185-9866-6f34d31c1070.png" width="500">

<br>

#### 리베이스의 결과물과 기존 병합의 차이점

- 3-way 병합은 병합 커밋이 있지만 리베이스를 하면 **병합 커밋은 없음**.

- 브랜치의 **마지막을 가리키는 커밋 위치가 다름**.(브랜치 A는 커밋 4를 가리키지만 master 브랜치는 아직 커밋 6을 가리킴)

<br>

---

<br>
<img src="https://user-images.githubusercontent.com/113653315/201720018-0e898dab-8ca9-417c-9446-ae7de5d5aba2.png" width="500">


**rebase** 명령어 사용

<img src="https://user-images.githubusercontent.com/107173046/201603510-21c5f245-4c95-4628-902c-791b37cb713f.png" width="500">

#### 리베이스 실습 전 셋팅

1.	index.html 파일 수정, 커밋. 먼저 브랜치 생성

<img src="https://user-images.githubusercontent.com/107173046/201603869-6ddfde39-aeba-4647-bd11-1154fb6475fa.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201603890-b2d96a8e-e4d4-4bb3-969a-d62a0d897fab.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201603903-6b17d2bc-a880-4f95-9ea6-e4c7e6cef8db.png" width="500">


2.	main 브랜치에서도 index.html 수정 후 두 번 커밋

<img src="https://user-images.githubusercontent.com/107173046/201603950-878edbd4-115b-4018-a663-f5226126f4d0.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201604007-abf4acf3-89c6-4bed-a2db-ee8c671b5645.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201604024-abac90c6-ff02-4d8d-a8af-e206c711bd6e.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201604042-309fc54a-1934-49ae-b5a8-7f3cf8254abf.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201604048-3e323a90-9887-4f10-a82c-0e7c20ff294f.png" width="500">


3.	베이스 커밋 하나를 기준으로 서로 다른 브랜치에 각각의 커밋이 추가 됨. 소스트리에서 확인

<img src="https://user-images.githubusercontent.com/107173046/201604068-113d3951-fc5f-4d04-8442-a931b38b4ea9.png" width="500">


<br>

---

<br>
<img src="https://user-images.githubusercontent.com/113653315/201720042-7f6e3750-1ca4-4872-bd5d-9f958cd6d3b9.png" width="500">


리베이스는 병합 기준 브랜치가 merge 명령어와 반대임.

<img src="https://user-images.githubusercontent.com/107173046/201604147-0abc2eb6-82de-4bf6-ab22-4bbdb5aac2fb.png" width="500">



1.	리베이스를 하기 위해 description 브랜치로 체크아웃.

<img src="https://user-images.githubusercontent.com/107173046/201604275-94e93f26-2f0c-47c1-ae22-65ba92169e5f.png" width="500">


2.	description 브랜치에서 원본 main 브랜치를 리베이스.

<img src="https://user-images.githubusercontent.com/107173046/201604289-21aad05d-2045-43ea-ab9e-0a3fe3f1dbff.png" width="500">

> 리베이스 명령 시 **파생 브랜치의 커밋들은 기준 브랜치의 마지막 커밋으로 재정렬**

3.	소스 트리를 통해 마지막 커밋인 ‘add menu6’ 뒤에 파생 브랜치의 커밋이 연결된 것을 볼 수 있음.

<img src="https://user-images.githubusercontent.com/107173046/201604317-4bcb7d43-24d7-46f0-9339-c7ac3e2dcaa4.png" width="500">


<br>

---

<br>
<img src="https://user-images.githubusercontent.com/113653315/201721106-89a29173-ddbe-4504-9c1a-81efcfebac49.png" width="500">


- 리베이스는 베이스 커밋을 변경하여 병합. 
- 베이스 커밋을 변경하는 과정에서 재배치 작업을 하며 이 과정에서 **커밋의 해시 값이 변경**됨.

#### 리베이스 후 로그 확인

1.	리베이스 이전 커밋 해시 값 : de764e8

<img src="https://user-images.githubusercontent.com/107173046/201605561-21cbb059-3ed2-4e9a-883d-9b40cee73aeb.png" width="500">


2.	리베이스 이후 커밋 해시 값 : a9d50fe

<img src="https://user-images.githubusercontent.com/107173046/201605579-4c262421-932c-48d8-80b1-019ea670d2bc.png" width="500">


<br>

---

<br>
<img src="https://user-images.githubusercontent.com/113653315/201720068-fc93431b-dce6-4b1f-b216-5e0163efe34a.png" width="500">


- 리베이스는 커밋 위치를 재조정만 하며 브랜치의 HEAD 포인터까지는 옮겨 주지 않음
> 리베이스 한 후에는 **병합 브랜치의 HEAD를 맞추어야** 함


<img src="https://user-images.githubusercontent.com/107173046/201605985-01865ab1-bc94-45ac-982b-f79364283dd0.png" width="500">

1.	병합을 위해 main 브랜치로 체크아웃, merge 명령어 실행

<img src="https://user-images.githubusercontent.com/107173046/201606089-0f95841d-41ff-41ec-b750-ac903984d552.png" width="500">

2.	소스트리 다시 확인

<img src="https://user-images.githubusercontent.com/107173046/201606119-fcf3093b-fb6f-45e7-b3d9-53127512b3c2.png" width="500">

> 두 브랜치 HEAD가 동일한 커밋 위치를 가리키고 있음. 
> 
> **리베이스는 커밋을 재배치만 할 뿐**이지 실제 병합과 같은 최종 상태는 가지지 않기 때문에 
> **리베이스 후에는 HEAD 포인터를 일치하기 위해 Fast-Forward 병합을 실행시켜야 최종 병합을 완성할 수 있음**.

<br>

---

<br>
<img src="https://user-images.githubusercontent.com/113653315/201720095-3abef735-75ba-468c-8c66-0ff591677829.png" width="500">


- 리베이스는 기준점을 변경함. 병합 과정에서 충돌이 발생할 수 있음.
- 리베이스 충돌 : 사용자가 수동으로 해결해야 함.

1.	menu 브랜치 생성, 이동

<img src="https://user-images.githubusercontent.com/107173046/201606695-0e3466ab-dfe7-4fcd-a5c6-9f515ca57c01.png" width="500">

2. index.html 변경, 두 번 커밋

<img src="https://user-images.githubusercontent.com/107173046/201606755-b255eabd-ed10-4312-a5b1-1d24e6c9aa08.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201606774-4dafc3ad-fa75-4ed8-81c3-dc3018842356.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201606785-91d62ba5-8e35-48b9-bb32-64c253771723.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201606797-268f1a19-399b-4705-a4af-7138cfe75baa.png" width="500">

3.	master 브랜치에서도 동일한 위치의 내용 수정해 충돌 만듦.

<img src="https://user-images.githubusercontent.com/107173046/201606872-738aaba0-eda7-4a3b-b950-1e302fef6fbe.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201606884-2c409f04-3f74-4bef-9386-afe579e1c646.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201606897-dc2c29b0-868c-4088-8632-bdc18a5c20d7.png" width="500">

4.	소스트리 확인

<img src="https://user-images.githubusercontent.com/107173046/201606929-538ab8a5-c535-486c-a23b-f5e37e157ffb.png" width="500">

> 서로 다른 브랜치 모양으로 분기 됨.

5.	menu 브랜치로 체크아웃. 리베이스 명령 실행, 충돌 발생 부분 수정.

<img src="https://user-images.githubusercontent.com/107173046/201607060-cbc0b5ad-b00c-436e-9c72-d60996dd6d77.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201607079-fba73d79-d82b-4068-8d68-ef517715de77.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201607093-05d53893-5daa-49cc-aff2-f23c7088eb13.png" width="500">

6.	충돌 수정 후 rebase 명령어와 –continue 옵션 사용. 수정한 파일을 다시 스테이지 상태로 변경. 오류뜨는 부분은 스킵(--skip은 특정 커밋의 충돌을 제외할 수 있음)

<img src="https://user-images.githubusercontent.com/107173046/201607134-f72fd150-90e3-4e85-a1bc-74881bf7d0bb.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201607142-c9842f3f-d1b4-4942-8f28-2ba3c4d47d2f.png" width="500">

7.	master 브랜치로 체크아웃. menu 병합, 삭제

<img src="https://user-images.githubusercontent.com/107173046/201607176-96cb23cf-191b-46b2-b9d8-a70efd42c393.png" width="500">

> 브랜치 HEAD 일치

<br>

---

<br>
<img src="https://user-images.githubusercontent.com/113653315/201720180-35026679-24f7-4b00-834a-b0375a774049.png" width="500">


- 마지막 커밋은 –-amend 옵션으로 수정 가능. 
- 리베이스는 여러 커밋을 한 커밋으로 묶을 수 있음. 이때 -i 옵션 사용

<img src="https://user-images.githubusercontent.com/107173046/201607388-618de8b8-b7a9-4ed5-969c-9299fdc7b49e.png" width="500">
<img src="https://user-images.githubusercontent.com/107173046/201607418-20de088c-1a4c-4a06-a207-3a13de4324e9.png" width="500">

> 리베이스 한 3개의 커밋을 하나의 커밋으로 묶음. 이때 **합쳐진 커밋은 새 해시 값이 부여**됨

<br>

---

<br>

<img src="https://user-images.githubusercontent.com/113653315/201720215-460b3908-2e8b-4d82-b390-0faecb54c6f7.png" width="500">

1.	리베이스는 커밋 위치와 해시값을 변경함

3.	저장소를 외부에 공개했다면 공개된 순간부터 커밋은 리베이스를 사용하지 않는 것이 원칙

5.	리베이스는 외부에서 동작하기 전엔 로컬에서만 실행하는 것이 좋음

7.	공개된 커밋을 리베이스하면 커밋 위치와 해시값이 변경되어 혼란스러움

9.	공개된 커밋을 변경할 때는 revert 명령어를 사용


<br>

---

<br>
<img src="https://user-images.githubusercontent.com/113653315/201720252-328ec6e7-1381-4a47-98b1-53322b07a1fd.png" width="500">

- 다수의 개발자와 협업할 때 병합과 충돌이 매우 자주 발생. 개발 과정에서 병합/충돌을 최소화 하고 예방하려면 master 브랜치 내용을 자주 반영하여 병합해야 함
- 원격 저장소의 master 브랜치를 모니터링 하고, 변화된 부분을 즉시 반영하면서 작업하면 충돌을 최소화 하거나 예방할 수 있음
