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

asset path는 manifest에 기록된 실제 raw path를 그대로 사용한다.
이미지 선택 목적으로 파일 자체를 분석하지 않는다.

현재 event CG manifest는 없다.
