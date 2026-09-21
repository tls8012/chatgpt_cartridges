# AGENTS.md — datellm art production

이 디렉터리의 작업은 datellm의 AI 이미지 에셋 제작용이다.

## Scope

주요 문서:

- `scg-spec.md`: 캐릭터 스탠딩(SCG) 제작 규칙
- `eventcg-spec.md`: 이벤트 CG 제작 규칙

원본 설정:

- `../raw/entities/`
- `../raw/story/`
- `../raw/game.md`

이미지 출력:

- `../raw/assets/characters/`
- `../raw/assets/event_cg/`

`../distribution/`은 build 산출물이다.
**이미지 제작 작업에서 distribution을 직접 수정하지 않는다.**

---

## Source of truth

충돌이 있을 때 우선순위:

1. 사용자의 현재 작업 지시
2. `scg-spec.md` / `eventcg-spec.md`
3. `../raw/entities/`와 `../raw/story/`
4. `../distribution/`은 참고용 runtime build이며 원본 설정의 대체물이 아니다.

캐릭터 성격, 관계, 이벤트 의미를 이미지 제작 편의를 위해 새로 창작하지 않는다.

---

## Style references

사용자가 기획 단계에서 제공한 스타일 레퍼런스의 해석은 `scg-spec.md`에 텍스트로 기록되어 있다.

로컬 workspace에 실제 reference image를 둘 경우 권장 경로:

```text
datellm/art-production/references/
  style-main.jpg
  style-color.jpg
  style-school.jpg
```

역할:
- `style-main.jpg`: 메인 화풍
- `style-color.jpg`: 선명함/광택/하이라이트 보조
- `style-school.jpg`: 학원물/교복/따뜻한 무드 보조

실제 파일이 존재하면 이미지 생성 시 적극적으로 reference로 사용한다.
파일이 존재하지 않으면 **사용했다고 주장하지 말고**, spec의 텍스트 스타일 가이드만 따른다.

특정 작가 이름이나 작품명을 추측해 style prompt에 넣지 않는다.

---

## Core visual rules

모든 생성물에서 반드시 유지:

- 하나의 통일된 현대 일본 애니/비주얼노벨 화풍
- 같은 학교의 일관된 교복 디자인
- 캐릭터별 고정된 색감과 body language
- female/male이 같은 캐릭터의 변형처럼 보일 것
- human/logo가 같은 이미지의 head variation처럼 보일 것
- logo 모드에 인간 얼굴, 눈, 입, 머리카락을 남기지 않을 것
- logo에 임의의 표정 요소를 추가하지 않을 것
- 과도한 성적 연출을 기본값으로 사용하지 않을 것

---

## Required workflow — SCG

새 캐릭터 또는 아직 anchor가 없는 캐릭터:

1. `scg-spec.md` 읽기.
2. 해당 캐릭터의 `../raw/entities/<Character>.md` 읽기.
3. 기존 승인 anchor가 있는지 먼저 확인.
4. 없으면 human `uniform_neutral` anchor를 먼저 만든다.
5. 같은 anchor에서 P0 human pose를 파생한다.
6. 가능하면 이미지 편집을 사용해 human 이미지의 머리만 logo로 교체한다.
7. female 세트와 male 세트가 같은 캐릭터 코어를 공유하는지 확인한다.
8. P0 전체가 안정된 뒤에만 P1을 만든다.

**같은 캐릭터의 포즈를 서로 독립적인 fresh generation으로 대량 생성하지 않는다.**

이미지 편집 기능이 없는 환경에서는:
- 승인 anchor를 reference로 사용한다.
- human/logo의 구도 차이를 최소화한다.
- 완벽한 대응쌍을 만들 수 없었다면 작업 결과에 그 제한을 명시한다.

---

## Required workflow — Event CG

1. `eventcg-spec.md` 읽기.
2. 해당 event source in `../raw/story/` 읽기.
3. 해당 캐릭터의 승인된 SCG anchor를 찾는다.
4. anchor 없이 event CG부터 만들지 않는다.
5. human composition master를 먼저 만든다.
6. logo 버전은 가능한 한 같은 composition을 편집해서 만든다.
7. player는 기본적으로 POV/off-screen으로 유지하고 불필요하게 외형을 확정하지 않는다.
8. P0에서는 여러 LLM이 한 CG에 동시에 등장하는 구도를 피한다.

---

## Pilot rule

새로운 전체 production을 처음 시작할 때는 바로 모든 이미지를 생성하지 않는다.

먼저 다음 pilot을 만든다.

```text
ChatGPT / female /
  human / uniform_neutral
  logo  / uniform_neutral
```

가능하면 여기에 `uniform_signature` human/logo pair까지 추가한다.

pilot의:
- 화풍
- 교복
- 체형
- human/logo 대응
이 안정적이면 같은 규칙을 확장한다.

사용자가 이미 anchor를 승인했거나 명시적으로 pilot을 건너뛰라고 하면 반복하지 않는다.

---

## Output paths

SCG:

```text
datellm/raw/assets/characters/{character}/{gender}/{head_mode}/{asset}.png
```

Event CG:

```text
datellm/raw/assets/event_cg/{character}/{gender}/{head_mode}/{event_key}.png
```

경로 규칙:
- character: `chatgpt`, `claude`, `gemini`, `grok`
- gender: `female`, `male`
- head_mode: `human`, `logo`
- filename: lowercase snake_case
- 이미지: PNG

---

## Do not

- `raw/entities`의 캐릭터 설정을 이미지에 맞추려고 수정하지 않는다.
- `raw/story`의 이벤트 내용을 CG에 맞추려고 수정하지 않는다.
- `distribution`에 직접 이미지를 넣지 않는다.
- 없는 캐릭터 취향, 과거사, 연애 관계를 시각 설정으로 확정하지 않는다.
- logo를 단순 얼굴 스티커처럼 처리하지 않는다.
- 승인된 anchor가 있는데 이유 없이 캐릭터 디자인을 리셋하지 않는다.
- group CG 때문에 gender/head-mode 조합 폭증을 일으키지 않는다.
- 깨진 손, 뒤틀린 교복, 얼굴 잔여물이 있는 logo 이미지를 정상 완료로 처리하지 않는다.

---

## Validation

배치 완료 후 최소 확인:

- 요청된 파일 수와 실제 생성 수가 같은가
- 모든 파일이 올바른 경로에 있는가
- PNG인가
- SCG는 투명 배경인가
- 같은 캐릭터의 스케일과 교복이 일관적인가
- human/logo pair가 구도상 대응되는가
- event CG가 원본 이벤트의 핵심을 왜곡하지 않았는가
- logo 모드에 인간 얼굴 요소가 남지 않았는가

문제가 있는 파일만 수정 또는 재생성한다.

---

## Git behavior

이미지 생성 자체와 Git commit은 별개다.

- 사용자가 commit까지 요청했다면 완성된 배치만 commit한다.
- 중간 실패 이미지나 discarded candidate는 commit하지 않는다.
- 기존 승인 asset을 덮어쓸 때는 변경 이유를 확인한다.
- commit message는 생성 범위가 드러나게 작성한다.
