# datellm Distribution

GAME_NAME: datellm
BUILD_VERSION: 2
FORMAT_VERSION: 1
CONTENT_ROOT: datellm/distribution

control.gender: female
control.head_mode: logo

## 데이터 폴더

- entities: entities/
  - 공개 세계 설정과 객체 자료.
  - 필요한 객체를 경로별로 조회하며 캐릭터 식별은 character_manifest.md를 먼저 사용한다.
  - 작품별 추가 컨트롤의 의미와 허용값은 entities/concepts/표현 컨트롤.md를 따른다.
- story: story/
  - 공개 narrative unit과 시작 안내.
  - 장면 파일은 선형 순서가 아니라 각 파일의 조건을 만족할 때 후보로 사용한다.
- flags: flags/
  - 현재 build에는 hidden reveal이 없어 public flag가 없다.
- hidden: hidden/
  - 현재 build에는 hidden reveal 또는 hidden story가 없다.
- assets: assets/
  - 현재 build에는 ChatGPT, Claude, Gemini, Grok의 캐릭터 SCG manifest가 있다.
  - 실제 이미지 선택은 assets/index.md와 그 하위 manifest를 우선한다.
  - 이미지를 선택하기 위해 이미지 파일 자체를 분석하지 않는다.

## 작품별 추가 컨트롤

- `gender`
  - default: `female`
  - allowed: `female` | `male`
  - 네 연애 대상의 성별 표현을 함께 결정한다.
  - 플레이어 캐릭터의 성별을 뜻하지 않는다.
- `head_mode`
  - default: `logo`
  - allowed: `logo` | `human`
  - 동일 연애 대상의 머리 표현 필터다.
  - 세계 설정, 정체, 관계, 기억, 사건 결과를 바꾸지 않는다.

현재 인스턴스의 실제 값은 init/runtime 규약에 따라 Save의 `init완료.md` 동명 필드가 이 기본값보다 우선한다.

## 진입점

character_manifest: character_manifest.md
welcome: story/welcome.md
story_manifest: story/story_manifest.md
start_story: story/전학 첫날.md
control_spec: entities/concepts/표현 컨트롤.md
asset_manifest: assets/index.md

## 탐색 규약

- character_manifest.md는 이름 있는 주요 캐릭터를 정확한 entity path로 연결하는 작은 색인이다.
- entities/와 story/는 하위 폴더를 재귀적으로 탐색할 수 있다.
- story unit은 파일 순서가 아니라 현재 조건·인물 동기·세계 상태를 기준으로 사용한다.
- flags/에 항목이 생기는 향후 build에서는 관련 flag가 해금된 뒤에만 대응 hidden payload를 조회한다.
- 캐릭터 이미지는 assets/index.md → characters.md 순으로 조회한다.
- asset 선택 시 현재 `gender`와 `head_mode`를 먼저 적용하고 장면에 맞는 pose를 고른다.
- manifest에 없는 asset 경로나 variant를 추측해서 만들지 않는다.
