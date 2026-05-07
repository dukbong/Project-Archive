# affiliate-link-generator — 어필리에이트 코드 자동 생성 크롬 확장

플랫폼마다 다른 어필리에이트 링크 포맷을 페이지에서 자동으로 생성해주는 크롬 확장 프로그램입니다.

**Install**: [https://buly.kr/6141yax](https://buly.kr/6141yax)

![시연 GIF](./assets/demo.gif)

---

## 만든 이유

- 플랫폼별로 어필리에이트 코드 생성 방식이 달라 매번 수동으로 변환하는 작업이 반복됨
- 단순 반복 작업이라 자동화 가치가 크다고 판단해 확장 프로그램으로 구현

## 기술 스택

<!-- TODO: 실제 사용 기술로 교체 -->
- JavaScript / TypeScript
- Chrome Extension Manifest V3

## 핵심 기능

<!-- TODO: 실제 기능 1~3개 -->

- 현재 페이지 URL을 감지해 플랫폼별 어필리에이트 포맷으로 자동 변환
- 변환된 링크 클립보드 자동 복사
- 플랫폼별 변환 규칙을 코드 분리로 확장 가능하게 설계

## 화면

| 팝업 UI | 변환 결과 |
|---|---|
| ![팝업](./assets/popup.png) | ![결과](./assets/result.png) |

## 개발 노트

<!-- TODO: 트러블슈팅, 결정 사항 1~2개 -->

- **플랫폼별 URL 패턴 인식** — 어떤 방식으로 분기 처리했는가
- **Manifest V3 마이그레이션** — Service Worker 전환 시 고려한 점
