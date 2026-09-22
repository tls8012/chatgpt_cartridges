# datellm assets

현재 실제 SCG 이미지 에셋이 존재한다.

## 캐릭터 SCG

경로:

```text
raw/assets/characters/
  chatgpt/
  claude/
  gemini/
  grok/
```

각 캐릭터는 다음 축으로 구성된다.

- gender: `female` | `male`
- head_mode: `human` | `logo`
- pose:
  - `uniform_neutral`
  - `uniform_signature`
  - `uniform_talk`
  - `uniform_think`

현재 기본 SCG는 총 64개다.

```text
4 characters × 2 genders × 2 head modes × 4 poses = 64
```

## 런타임 선택

작품별 추가 컨트롤과 연결한다.

- `gender`
  - 기본값: `female`
  - 허용값: `female`, `male`
- `head_mode`
  - 기본값: `logo`
  - 허용값: `logo`, `human`

`gender`는 네 연애 대상의 성별 표현을 함께 결정한다.
`head_mode`는 동일 인물의 시각 표현 필터이며 세계 설정, 관계, 기억을 변경하지 않는다.

## Logo 모드

logo 모드에서 캐릭터 머리는 얼굴 위에 붙인 표식이 아니라 각 서비스 로고 자체다.
인간 얼굴, 눈, 입, 머리카락을 별도로 더하지 않는다.

## Human 모드

human 모드는 과도하게 슈르한 시각 표현을 완화하기 위한 일반 미소녀/미소년 표현이다.
동일 캐릭터의 filter variation이므로 logo 모드와 같은 정체와 캐릭터 코어를 유지한다.

## Event CG

이벤트 CG는 아직 필수 runtime asset으로 포함하지 않는다.
추가 제작 후 별도 asset build에서 manifest에 반영한다.
