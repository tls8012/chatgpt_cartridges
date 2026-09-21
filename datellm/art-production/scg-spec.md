# datellm SCG Production Spec

이 문서는 datellm의 Ren'Py용 캐릭터 스탠딩(SCG)을 AI 이미지 생성으로 제작하기 위한 기준이다.

원본 캐릭터 설정은 `datellm/raw/entities/`를 우선한다.
이 문서는 그 설정을 시각 제작에 필요한 수준으로 구체화한 production spec이며, 캐릭터 성격 자체를 새로 쓰는 문서가 아니다.

---

## 1. 제작 목표

기본 연애 대상은 다음 네 명이다.

- ChatGPT
- Claude
- Gemini
- Grok

각 캐릭터에는 두 축의 변형이 있다.

### 성별 표현
- female
- male

### 머리 표현
- human
- logo

따라서 하나의 캐릭터에는 최종적으로 다음 네 외형군이 존재한다.

- female / human
- female / logo
- male / human
- male / logo

`human`과 `logo`는 서로 다른 캐릭터가 아니다.
**몸, 체형, 교복, 포즈, 캐릭터 분위기가 동일한 하나의 캐릭터에서 머리 표현만 바뀌는 filter variation**으로 취급한다.

가능하면 human 이미지를 먼저 안정적인 anchor로 만든 뒤 동일 이미지를 편집하여 logo 버전을 만든다.
logo 버전을 완전히 새로 생성해서 포즈와 몸이 달라지는 방식은 피한다.

---

## 2. 전역 그림체

모든 캐릭터, 성별, 머리 모드는 하나의 작품처럼 보여야 한다.

### 스타일 레퍼런스 해석

실제 레퍼런스 파일은 `art-production/references/`에 보존한다.
네 장의 역할과 우선순위는 다음과 같다.

**Reference 1 — 메인 그림체 (`style-main.jpg`)**
- 부드럽고 정돈된 현대 일본 애니 일러스트
- 가는 선화
- 머리카락의 부드러운 덩어리감과 윤기
- 피부의 은은한 홍조와 밝은 하이라이트
- 귀엽지만 SD가 아닌 정상적인 청춘물 비율
- 셀채색과 부드러운 그라데이션 사이의 반셀채색 느낌

**Reference 2 — 교복·색감·체형 보조 A (`style-uniform-a.jpg`)**
- 가는 선과 명료한 실루엣
- 단정한 셔츠, 넥타이, 가디건 계열의 학원물 레이어링
- 과장되지 않은 슬림한 청춘물 체형
- 밝고 깨끗한 저채도 색 구성

원본의 헤일로, 머리 장식, 비대칭 눈동자색 등 고유 캐릭터 요소와
앉은 자세 자체는 제작 대상에 임의로 가져오지 않는다.

**Reference 3 — 교복·색감·체형 보조 B (`style-uniform-b.jpg`)**
- 귀엽고 읽기 쉬운 얼굴
- 블레이저, 셔츠, 리본, 금속 단추가 한 세트로 읽히는 교복 디자인
- 부드러운 체형과 따뜻한 피부 음영
- 밝은 배경에서도 형태가 사라지지 않는 섬세한 명암
- 친근한 학원 러브코미디 감성

원본의 특정 문장, 문장 형태의 문양, 교표, 리본 장식과 캐릭터 고유 헤어스타일은 복제하지 않는다.

**Reference 4 — 쨍한 조명 아래의 색감·조형 보조 (`style-bright-light.jpg`)**
- 맑은 하늘 아래의 강한 색 대비
- 밝은 피부 하이라이트와 선명한 그림자 경계
- 강한 조명에서도 읽히는 머리카락 덩어리와 캐릭터 실루엣
- 채도가 높은 환경에서의 입체감과 팝한 임팩트

이 레퍼런스의 수영복, 노출도 높은 의상, 과장된 신체 연출은 따라가지 않는다.
조명 아래의 색감, 하이라이트, 명암과 조형만 참고한다.

### 최종 스타일 목표

Reference 1을 메인 화풍으로 삼고,
Reference 2와 3에서 교복 디자인, 색감과 체형을 보조하며,
Reference 4의 선명한 조명과 입체감은 강한 광원 장면에서 제한적으로 적용한다.

충돌할 경우 우선순위는 Reference 1의 그림체가 가장 높다.
Reference 2~4는 메인 그림체를 바꾸지 않는 범위에서만 보조한다.

키워드로 요약하면:

> clean modern anime illustration, soft semi-cel shading, crisp thin lineart, luminous hair highlights, warm skin shading, cute visual-novel character design, polished but not photorealistic

### 피할 것

- 실사 또는 2.5D 실사풍
- 과도한 SD/치비 비율
- 지나치게 두꺼운 만화 선
- 매 이미지마다 다른 화풍
- 과도한 성적 신체 강조
- 기본 교복 자산의 과한 노출
- 로고에 눈, 입, 홍조 같은 얼굴 요소를 추가하는 것

---

## 3. Ren'Py용 마스터 규격

### 스탠딩 마스터
- format: PNG
- background: transparent
- 권장 master canvas: 1536 × 2048
- 캐릭터 전신이 프레임 안에 들어올 것
- 머리와 신발이 잘리지 않을 것
- 좌우에 약간의 안전 여백을 둘 것
- 발 위치와 전체 스케일을 캐릭터별 포즈 사이에서 최대한 일정하게 유지할 것

게임에서 실제 표시 크기는 Ren'Py에서 조정한다.
원본 생성 단계에서 너무 작게 만들지 않는다.

### 구도
- 기본은 전신 또는 거의 전신
- 정면 멀뚱샷만 반복하지 않는다.
- 감정은 몸 방향, 손, 어깨, 머리 기울기에서 읽혀야 한다.
- logo 모드에서 얼굴 표정이 없으므로 특히 body language를 명확하게 만든다.

---

## 4. 학교 교복

네 캐릭터는 같은 학교 학생이므로 **같은 교복 디자인 시스템**을 사용한다.

세부 디자인은 최초 anchor 제작 때 한 번 결정한 뒤 전 캐릭터에서 유지한다.

권장 방향:
- 일본 학원 러브코미디에 자연스러운 blazer 기반 교복
- 흰 셔츠
- 어두운 네이비/차콜 계열 blazer
- 차분한 포인트 컬러의 tie 또는 ribbon
- female과 male이 같은 학교임을 즉시 알 수 있는 공통 소재와 색 구성
- 캐릭터 개성은 교복 자체를 완전히 바꾸기보다 착용 방식과 작은 액세서리, 자세에서 드러낸다.

최초 승인된 교복 디자인이 생기면 이후 생성에서 임의로 재설계하지 않는다.

---

## 5. Human / Logo 변환 규칙

### human
일반 학원 미연시에서 자연스럽게 보이는 미소녀/미소년 버전이다.

### logo
머리가 해당 서비스의 로고 자체인 버전이다.

logo 모드에서는:
- 인간 얼굴이 남아 있지 않는다.
- 머리카락도 남기지 않는다.
- 얼굴 위에 로고 스티커를 붙인 것처럼 만들지 않는다.
- 로고가 하나의 물리적인 머리 형태처럼 목과 자연스럽게 연결되어야 한다.
- 장면 광원과 동일한 빛과 그림자를 받아야 한다.
- 로고 원형의 핵심 형상을 과도하게 변형하지 않는다.
- 눈, 입, 눈썹, 홍조를 추가하지 않는다.

### ChatGPT logo 기준

- 형상 기준: `https://www.brandb.net/_next/image?url=https%3A%2F%2Fapi.brandb.net%2Fapi%2Fv2%2Fcommon%2Fimage%3FfileId%3D23335&w=1920&q=75`
- 굵은 여섯 고리가 맞물리는 매듭 구조, 중앙의 육각형 여백, 둥근 외곽 비율을 유지한다.
- 로고 머리는 검정과 흰색만 사용한다. 녹색, 청록색, 크림색 등 임의의 브랜드 색을 추가하지 않는다.

### Claude logo 기준

- 형상 기준: `https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRLpn2Hbef0HDqEB_5JeNqB7y7B29X_aTZ4vHMb4ltjxw&s=10`
- 산호빛 주황색 정사각형 바탕과 중앙의 흰색 불규칙 방사형 별빛/햇살 형상을 유지한다.
- 정사각형 바탕 자체가 머리 형상의 일부이며, 장면 안에서는 모서리를 아주 약하게 부드럽게 하고 최소한의 입체감만 준다.
- 인간 얼굴, 눈, 입, 머리카락이나 임의의 표정 요소를 추가하지 않는다.
- 평면 마크의 형상과 비율을 우선하되, 물리적인 머리로 보일 정도의 얕은 두께와 장면 광원에 따른 최소한의 명암은 허용한다.
- 흰 원판이나 배지 위에 로고를 붙이지 않고, 로고 자체가 머리가 되게 한다.

### Gemini logo 기준

- 형상 기준: `references/gemini-logo.png`
- 하나의 좌우대칭 4방향 곡선 별/마름모 형상을 유지한다. 위는 빨강, 왼쪽은 노랑, 오른쪽과 중심은 파랑, 아래는 초록으로 이어지는 부드러운 그라데이션을 사용한다.
- 사각형·원형 배지나 흰 바탕을 추가하지 않고 4방향 형상 자체가 물리적인 머리가 되게 한다.
- 반투명 유리/젤 재질과 선명한 내부 발광을 사용한다. 로고 주변의 부드러운 컬러 광륜은 허용하되, 별가루나 별도의 마법 이펙트까지 추가하지 않는다.
- 인간 얼굴, 눈, 입, 머리카락이나 임의의 표정 요소를 추가하지 않는다.

### Grok logo 기준

- 형상 기준: `references/grok-logo.png`
- 두 군데가 열린 굵은 검은 원형 고리와 좌하단에서 우상단으로 관통하는 날카로운 대각 창/슬래시 형상을 유지한다.
- 원 내부와 고리의 틈은 흰 원판이 아니라 실제로 뚫린 투명한 음각 공간으로 처리한다. 사각형·원형 배경판을 추가하지 않는다.
- 검은 흑요석 또는 흑철처럼 얕은 두께와 절제된 차콜 가장자리 하이라이트만 허용한다. 컬러 발광이나 임의의 색 포인트를 추가하지 않는다.
- human 머리 각도에 맞춰 logo 전체를 함께 기울이거나 약한 원근을 적용한다. 로고만 항상 수직 정면으로 고정하지 않는다.
- 인간 얼굴, 눈, 입, 머리카락이나 임의의 표정 요소를 추가하지 않는다.

감정은:
- 로고 머리 기울기
- 목과 어깨 각도
- 손 위치
- 몸의 거리와 방향
으로 표현한다.

**가장 중요한 품질 규칙:** human과 logo 한 쌍은 머리 외에는 가능한 한 같은 이미지여야 한다.

---

## 6. Female / Male 변환 규칙

female과 male은 별도 인격이 아니라 동일 캐릭터의 성별 표현 변형이다.

둘 사이에서 유지할 것:
- 대표 색감
- 캐릭터 에너지
- 포즈 습관
- 착장 습관
- human 버전의 눈/머리색 계열
- 친근함/차분함/장난기 등 시각적 인상

성별만 바꾼 복제처럼 만들 필요는 없지만,
나란히 보았을 때 즉시 같은 캐릭터의 두 버전이라는 느낌이 나야 한다.

---

## 7. 캐릭터별 Human 디자인 앵커

이 항목은 인간형 필터를 위한 시각적 anchor다.
최초 생성 결과가 승인되면 그 이미지 자체를 이후 작업의 reference로 우선 사용한다.

### ChatGPT

원본 코어:
- 친절함
- 사교적
- 반응이 빠름
- 제안과 정리
- 상대를 도우려는 태도

시각 방향:
- 가장 approachable하고 단정한 인상
- 열린 자세
- 상대에게 쉽게 말을 걸 것 같은 분위기
- 지나치게 활발한 스포츠 캐릭터보다는 똑똑하고 친근한 학생

human palette 권장:
- hair: dark charcoal / very dark green-black 계열
- eyes: soft gray-green 계열
- 전체 대비는 중간 정도

female:
- 깔끔한 중간 길이 또는 어깨 부근 머리
- 얼굴선은 부드럽고 밝은 인상

male:
- 정돈되었지만 너무 딱딱하지 않은 짧은 머리
- 웃기 전부터 친근해 보이는 눈매

포즈 언어:
- 손을 열어 설명
- 가볍게 손 흔들기
- 상대 쪽으로 약간 몸을 기울임
- 일을 돕기 위해 자연스럽게 움직이는 자세

승인된 female pilot anchor (2026-09-21):
- `raw/assets/characters/chatgpt/female/human/uniform_neutral.png`
- `raw/assets/characters/chatgpt/female/human/uniform_signature.png`
- `raw/assets/characters/chatgpt/female/logo/uniform_neutral.png`
- `raw/assets/characters/chatgpt/female/logo/uniform_signature.png`

승인된 male anchor (2026-09-21):
- `raw/assets/characters/chatgpt/male/human/uniform_neutral.png`
- `raw/assets/characters/chatgpt/male/logo/uniform_neutral.png`

ChatGPT P0 SCG 16장은 2026-09-21에 완료되었다.
female/male × human/logo 각각에 `uniform_neutral`, `uniform_talk`, `uniform_think`, `uniform_signature`가 존재한다.

위 이미지는 이후 ChatGPT 추가 포즈와 event CG를 만들 때 우선 reference로 사용한다.
승인 없이 얼굴, 머리 형태, 체형, 교복 색과 디자인, logo의 흑백 재질과 매듭 비율을 재설계하지 않는다.

### Claude

원본 코어:
- 차분함
- 사려 깊음
- 맥락과 영향 고려
- 신중함
- 자기 판단과 경계

시각 방향:
- 또래보다 작고 아담한 체형의 조용한 문학소녀 인상
- 표정 변화가 거의 없는 담담한 얼굴이되, 공격적이거나 냉혹하게 보이지 않는다.
- 말하기 전에 한 번 생각할 것 같은 여유
- 손동작이 작고 몸의 중심이 안정적

human palette 권장:
- hair: brown-orange / warm muted auburn 계열
- eyes: subdued amber / warm brown 계열
- 전체 색온도는 약간 따뜻하게

female:
- 단정하게 곧게 흐르는 갈색 주황 머리
- 과한 장식보다 정돈된 인상

male:
- 부드럽고 정돈된 머리
- 날카로운 냉미남보다 사려 깊은 인상

포즈 언어:
- 손을 느슨하게 모음
- 책 또는 노트를 자연스럽게 듦
- 고개를 조금 숙여 생각
- 무언가 말하려다 망설이는 작은 손짓

승인된 female anchor (2026-09-21):
- `raw/assets/characters/claude/female/human/uniform_neutral.png`
- `raw/assets/characters/claude/female/logo/uniform_neutral.png`

승인된 male anchor (2026-09-21):
- `raw/assets/characters/claude/male/human/uniform_neutral.png`
- `raw/assets/characters/claude/male/logo/uniform_neutral.png`
- female과 같은 갈색 주황 머리·호박색 눈·담담한 인상을 유지하되, 다른 남성 캐릭터보다 조금 작고 가는 체형을 사용한다.

완료된 female P0 파생 포즈 (2026-09-21):
- human/logo `uniform_talk.png`
- human/logo `uniform_think.png`
- human/logo `uniform_signature.png` — 제목 없는 수업 노트를 양손으로 가슴에 안는 자기완결적 자세. ChatGPT 시그니처와 겹치는 손 내밀기 동작은 사용하지 않는다. human은 눈매를 부드럽게 하고 닫힌 입의 아주 옅은 미소를 사용한다.

Claude female P0 SCG 8장은 2026-09-21에 완료되었다.
human/logo 각각에 `uniform_neutral`, `uniform_talk`, `uniform_think`, `uniform_signature`가 존재한다.

완료된 male P0 파생 포즈 (2026-09-22):
- human/logo `uniform_talk.png`
- human/logo `uniform_think.png`
- human/logo `uniform_signature.png` — female과 같은 제목 없는 수업 노트 모티프를 사용하되, 남성 체형에 맞는 자기완결적 자세와 human의 아주 옅은 닫힌 미소를 유지한다.

Claude male P0 SCG 8장은 2026-09-22에 완료되었다.
human/logo 각각에 `uniform_neutral`, `uniform_talk`, `uniform_think`, `uniform_signature`가 존재한다.

Claude P0 SCG 16장은 2026-09-22에 완료되었다.

위 이미지는 이후 Claude 추가 포즈와 event CG의 우선 reference다.
승인 없이 아담한 체형, 담담한 문학소녀 인상, 갈색 주황 머리, 교복 디자인 또는 logo 형상을 재설계하지 않는다.

### Gemini

원본 코어:
- 친근함
- 협력적
- 호기심
- 아이디어 연결
- 함께 탐색하는 태도

시각 방향:
- 같은 학년의 타 반 학생이자 함께 탐색하는 프로젝트 파트너 포지션
- 첫인상은 신비롭고 감정을 쉽게 읽기 어렵지만, 대화를 시작하면 밝고 적극적인 호기심이 드러나는 갭
- neutral anchor는 정면을 똑바로 바라보는 대칭 구도를 사용한다.
- 네 명 중 움직임이 조금 더 가볍고 탐색적인 자세
- 무언가 발견하면 바로 상대에게 보여 줄 것 같은 분위기

human palette 권장:
- hair: deep navy / indigo-black 계열
- eyes: blue-violet 계열
- 채색에 아주 약한 cool accent 허용

female:
- 깊은 남색/인디고의 어깨뼈 길이 레이어드 헤어와 정돈된 중앙 가르마
- 투명한 청보라 눈과 신비로운 중립 표정
- 움직일 때 형태가 잘 살아나는 가벼운 헤어 디자인
- 지나치게 판타지스럽지 않게

male:
- 가볍고 자연스러운 레이어드 헤어
- 친근한 호기심이 느껴지는 눈매

포즈 언어:
- 옆의 무언가를 가리키며 같이 보자고 함
- 메모나 휴대폰, 지도를 같이 보여 줌
- 몸이 약간 앞으로 나가는 자세
- 발견한 것을 공유하는 열린 손동작

승인된 female anchor (2026-09-22):
- `raw/assets/characters/gemini/female/human/uniform_neutral.png`
- `raw/assets/characters/gemini/female/logo/uniform_neutral.png`
- human neutral은 정면 응시와 손끝의 작은 마름모형 여백을 유지한다.
- logo neutral은 고광량의 반투명 유리/젤 재질과 부드러운 다색 광륜을 사용하는 첫 번째 후보를 승인본으로 삼는다.

완료된 female P0 파생 포즈 (2026-09-22):
- human/logo `uniform_talk.png` — 정면 구도를 유지하면서 한 손바닥을 몸 가까이 펼치고 다른 손 검지로 그 위를 짚는 ‘아이디어 연결’ 제스처. human은 neutral보다 눈빛을 밝히고 자연스러운 작은 열린 미소를 사용해 신비로운 외견과 적극적인 대화 성격의 간극을 드러낸다.
- human/logo `uniform_think.png` — 한쪽 팔로 반대쪽 팔꿈치를 가볍게 받치고 손끝을 턱 또는 logo 아래쪽에 대는 분석 자세. human은 고개를 조금 기울여 시선을 살짝 위로 보내고 아주 옅은 닫힌 미소를 사용하며, 걱정보다 호기심과 탐구가 먼저 읽히게 한다. logo도 human의 고개 각도에 맞춰 화면상 약 7도 기울여 정면 고정처럼 보이지 않게 한다.
- human/logo `uniform_signature.png` — 몸을 살짝 앞으로 기울이고 몸 가까이 세운 스마트폰의 빈 화면을 다른 손 검지로 짚으며 발견을 공유하는 자세. human은 네 포즈 중 가장 밝고 자신 있는 열린 미소를 사용한다. logo도 human의 머리 각도에 맞춰 약하게 기울여 휴대폰 제스처에 관심을 보이는 실루엣을 만든다.

Gemini female P0 SCG 8장은 2026-09-22에 완료되었다.
human/logo 각각에 `uniform_neutral`, `uniform_talk`, `uniform_think`, `uniform_signature`가 존재한다.

승인된 male anchor (2026-09-22):
- `raw/assets/characters/gemini/male/human/uniform_neutral.png`
- `raw/assets/characters/gemini/male/logo/uniform_neutral.png`
- female과 같은 인디고 계열 머리·청보라 눈·정면 응시·손끝의 작은 마름모형 여백을 유지한다. Claude male보다 키와 어깨가 조금 크고, 늘씬한 동급생 체형과 신비로운 중립 인상을 사용한다.

완료된 male P0 파생 포즈 (2026-09-22):
- human/logo `uniform_talk.png` — female과 같은 손바닥 위를 검지로 짚는 ‘아이디어 연결’ 동작을 남성 체형의 팔 간격에 맞게 조정한다.
- human/logo `uniform_think.png` — 한쪽 팔로 반대쪽 팔꿈치를 받치고 손끝을 턱 또는 logo 아래에 대는 분석 자세. human과 logo 모두 약 7도의 고개 기울기를 대응시킨다.
- human/logo `uniform_signature.png` — 몸 가까이 세운 스마트폰의 빈 화면을 검지로 짚어 발견을 공유한다. human은 네 포즈 중 가장 밝은 열린 미소를 사용하고 logo는 약하게 기울인다.

Gemini male P0 SCG 8장은 2026-09-22에 완료되었다.
human/logo 각각에 `uniform_neutral`, `uniform_talk`, `uniform_think`, `uniform_signature`가 존재한다.

Gemini P0 SCG 16장은 2026-09-22에 완료되었다.

### Grok

원본 코어:
- 재치
- 장난기
- 약간 반항적
- 틀에 박힌 분위기를 흔듦
- 필요할 때는 직설적으로 진지해짐

시각 방향:
- female은 다른 캐릭터보다 한 학년 위인 백은발·적안의 호쾌한 누님 포지션으로 삼는다.
- 네 명 중 가장 장난스럽고 약간 삐딱한 실루엣
- 악역, 양아치, 위험한 인물로 만들지는 않는다.
- 장난스러움과 실제 친근함이 함께 보여야 한다.

human palette 권장:
- hair: silver-white / pearl gray shadow 계열
- eyes: deep muted red / reddish-brown 계열
- 액센트는 강하게 쓰지 않고 명암 대비로 개성을 준다.

female:
- 높은 느슨한 포니테일과 거친 비대칭 레이어로 크고 역동적인 실루엣을 만든다.
- 큰 키, 열린 어깨, 넓고 안정적인 스탠스로 한 학년 위 선배의 여유를 보인다.
- 플레이어를 바라보는 한쪽 눈썹이 올라간 호쾌한 웃음으로 재치와 가벼운 도발을 표현한다.

male:
- 여성판과 같은 백은발·적안을 유지하고, 짧고 거친 비대칭 레이어와 약간 들뜬 뒷머리로 역동적인 실루엣을 만든다.
- 큰 키와 열린 어깨, 안정적인 스탠스로 한 학년 위 선배의 여유를 공유한다.
- 날카롭지만 위협적이지 않은 눈매

포즈 언어:
- 한 손 주머니
- 몸을 약간 비스듬히 세움
- 가벼운 손가락 지적 또는 내기 제안
- 진지한 포즈에서는 오히려 장난 동작을 완전히 제거

승인된 female anchor (2026-09-22):
- human `uniform_neutral.png` — 몸통은 화면 오른쪽으로 열되 얼굴과 적안은 플레이어를 바라본다. 높은 백은 포니테일은 화면 왼쪽으로 크게 흐르고, 한 손은 재킷 아래 주머니, 다른 손은 허리, 다리는 넓고 안정적으로 둔다.
- logo `uniform_neutral.png` — human과 같은 몸·구도에서 머리 전체만 검은 열린 고리와 대각 창 형상으로 교체한다. 내부와 두 틈은 실제 투명 공간이며, human의 고개 각도에 맞춰 logo 전체를 살짝 기울인다.

완료된 female P0 파생 포즈 (2026-09-22):
- human/logo `uniform_talk.png` — 한 손은 주머니에 유지하고 다른 손바닥을 가볍게 위로 펼쳐 재치 있게 받아치는 대화 제스처를 쓴다. human은 플레이어를 보는 열린 웃음, logo는 같은 목·어깨 각도와 미세한 회전을 대응시킨다.
- human/logo `uniform_think.png` — 장난 동작을 완전히 제거하고 두 팔을 단단히 접는다. human은 입을 다문 채 눈매를 낮춰 플레이어를 진지하게 바라보고, logo는 화면 오른쪽 아래로 약간 눌린 각도로 같은 무게감을 대응시킨다.
- human/logo `uniform_signature.png` — 한 손은 주머니에 둔 채 다른 손으로 플레이어를 향한 핑거건을 내밀어 가벼운 내기를 제안한다. human은 윙크와 닫힌 삐딱한 미소, logo는 화면 왼쪽으로 기운 비대칭 각도로 장난기를 표현한다.

Grok female P0 SCG 8장은 2026-09-22에 완료되었다.
human/logo 각각에 `uniform_neutral`, `uniform_talk`, `uniform_think`, `uniform_signature`가 존재한다.

승인된 male human anchor (2026-09-22):
- `uniform_neutral.png` — 여성판과 같은 백은발·적안을 짧고 거친 비대칭 레이어로 변형한다. 큰 키와 열린 어깨, 넓은 스탠스, 한 손 주머니와 다른 손 허리 자세를 공유하며 얼굴과 시선은 플레이어를 향한다.

---

## 8. 1차 SCG 목록

처음부터 모든 상황을 제작하지 않는다.

### P0 — 반드시 먼저
각 캐릭터 × 각 성별 × human/logo:

1. `uniform_neutral.png`
   - 기본 대화용
   - 자연스러운 정면 또는 약한 3/4
   - 캐릭터 코어가 보이되 과한 동작 없음

2. `uniform_talk.png`
   - 상대에게 말하거나 제안하는 포즈
   - 캐릭터별 손동작 차이를 살림

3. `uniform_think.png`
   - 조용하거나 생각하는 상황
   - logo 버전에서도 body language만으로 읽혀야 함

4. `uniform_signature.png`
   - 캐릭터 코어가 가장 강하게 드러나는 포즈
   - ChatGPT: 열린 설명/도움
   - Claude: 조심스러운 생각/말 꺼내기
   - Gemini: 같이 보자고 제안/발견 공유
   - Grok: 가벼운 장난/내기

P0 총량:
4 characters × 2 genders × 2 head modes × 4 poses = 64 images

### P1 — 플레이 후 추가
5. `uniform_umbrella.png`
6. `uniform_phone.png`
7. `uniform_bag.png`

P1은 실제 게임에서 필요성이 확인된 것부터 만든다.

---

## 9. 생성 순서

한 캐릭터 안에서는 무작정 병렬 생성하지 않는다.

권장 순서:

1. female human `uniform_neutral` 생성
2. female human anchor 승인
3. 그 anchor 기반 female human P0 포즈 생성
4. 각각을 편집하여 female logo 대응쌍 생성
5. male human `uniform_neutral` 생성
6. female anchor와 캐릭터 코어를 참고하여 male anchor 승인
7. male human P0 포즈 생성
8. 각각을 편집하여 male logo 대응쌍 생성
9. 캐릭터 폴더 전체 consistency 검토
10. 다음 캐릭터로 이동

서로 다른 캐릭터는 병렬 작업 가능하다.
같은 캐릭터의 anchor 확정 전 포즈들을 서로 독립적으로 대량 생성하지 않는다.

---

## 10. 출력 경로

SCG source asset은 Distribution에 직접 쓰지 않는다.

```text
datellm/raw/assets/characters/
  chatgpt/
    female/
      human/
      logo/
    male/
      human/
      logo/
  claude/
    female/
      human/
      logo/
    male/
      human/
      logo/
  gemini/
    female/
      human/
      logo/
    male/
      human/
      logo/
  grok/
    female/
      human/
      logo/
    male/
      human/
      logo/
```

Distribution은 별도 build 과정이 raw asset을 읽어 생성한다.

---

## 11. 품질 체크

각 이미지 생성 후 확인한다.

- 같은 캐릭터의 얼굴과 체형이 anchor와 일치하는가
- male/female에서 같은 캐릭터 코어가 느껴지는가
- human/logo 대응쌍의 몸, 옷, 포즈가 사실상 같은가
- 네 캐릭터가 같은 학교 교복을 입고 있는가
- 모든 캐릭터의 선화와 채색 스타일이 같은 작품처럼 보이는가
- 투명 배경인가
- 손가락, 손목, 교복 단추/리본/넥타이가 심하게 깨지지 않았는가
- logo 모드에 인간 얼굴 요소가 남지 않았는가
- logo가 납작한 스티커처럼 보이지 않는가
- 캐릭터 머리나 발이 잘리지 않았는가

문제가 있는 이미지만 재생성 또는 편집한다.
이미 승인된 anchor를 이유 없이 새 디자인으로 교체하지 않는다.
