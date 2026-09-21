# datellm Distribution

GAME_NAME: datellm
BUILD_VERSION: 1
FORMAT_VERSION: 1
CONTENT_ROOT: datellm/distribution

## 데이터 폴더

- entities: entities/
  - 공개 세계 설정과 객체 자료.
  - 필요한 객체를 경로별로 조회하며 캐릭터 식별은 character_manifest.md를 먼저 사용한다.
- story: story/
  - 공개 narrative unit과 시작 안내.
  - 장면 파일은 선형 순서가 아니라 각 파일의 조건을 만족할 때 후보로 사용한다.
- flags: flags/
  - 현재 build에는 hidden reveal이 없어 public flag가 없다.
- hidden: hidden/
  - 현재 build에는 hidden reveal 또는 hidden story가 없다.
- assets: assets/
  - 현재 build에는 실제 runtime asset이 없다.
  - raw의 asset 문서는 미래 SCG 경로 예시뿐이므로 존재하지 않는 asset path를 배포 manifest로 만들지 않았다.

## 진입점

character_manifest: character_manifest.md
welcome: story/welcome.md
story_manifest: story/story_manifest.md
start_story: story/전학 첫날.md

## 탐색 규약

- character_manifest.md는 이름 있는 주요 캐릭터를 정확한 entity path로 연결하는 작은 색인이다.
- entities/와 story/는 하위 폴더를 재귀적으로 탐색할 수 있다.
- story unit은 파일 순서가 아니라 현재 조건·인물 동기·세계 상태를 기준으로 사용한다.
- flags/에 항목이 생기는 향후 build에서는 관련 flag가 해금된 뒤에만 대응 hidden payload를 조회한다.
- assets/에 manifest가 생기는 향후 build에서는 확인된 manifest path만 사용한다.
