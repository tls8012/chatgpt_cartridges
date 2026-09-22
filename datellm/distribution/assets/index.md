# Asset Index

## Character SCG
manifest: characters.md

현재 캐릭터 SCG:
- ChatGPT
- Claude
- Gemini
- Grok

선택 축:
- gender: `female` | `male`
- head_mode: `human` | `logo`
- outfit: `uniform`
- pose: `neutral` | `signature` | `talk` | `think`

현재 인스턴스의 `gender`와 `head_mode`를 먼저 적용한 뒤,
장면에 맞는 pose를 선택한다.

## Backgrounds
manifest: backgrounds.md

현재 배경은 5개다.

- school_gate / spring_cherry_blossom
- classroom / spring_day
- classroom / sunset_after_school
- hallway / spring_day
- library / sunny_afternoon

장면의 현재 장소와 시간대/계절 정보가 manifest의 variant와 맞을 때 해당 배경을 사용한다.
정확히 맞는 배경이 없으면 manifest에 없는 경로나 variant를 추측해서 만들지 않는다.

## 공통 규칙

asset path는 각 manifest에 기록된 실제 raw path를 그대로 사용한다.
이미지 선택 목적으로 이미지 파일 자체를 분석하지 않는다.

현재 event CG manifest는 없다.
