# onboard-guide

[English](README.md) | **한국어**

현재 열려 있는 레포지토리를 분석해 신규 투입자용 **인터랙티브 온보딩 문서**를 만들어 주는 Claude Code 플러그인입니다. "어디부터 어떤 순서로 읽어야 하는지"를 담은 `onboarding.html` 파일 하나를 생성합니다.

이 저장소는 플러그인을 배포하는 `jacob-plugins` 마켓플레이스이기도 합니다.

## 설치

Claude Code에서:

```
/plugin marketplace add Jacob-9909/onboard-guide
/plugin install onboard-guide@jacob-plugins
```

설치 후 Claude Code를 재시작하면 플러그인이 로드됩니다.

## 사용법

1. 문서를 만들 **레포 루트**에서 Claude Code를 실행합니다.
2. `onboarding` 스킬(`onboard-guide:onboarding`)을 실행합니다.
3. 레포 루트에 생성된 `onboarding.html`을 브라우저로 엽니다.

특정 부분에 집중하려면 하위 디렉토리 경로나 관점을 인자로 넘기면 됩니다.

## 생성되는 문서 구성

| 구성 | 내용 |
|---|---|
| KPI 스트립 | 파일 수, 코드 라인, 주요 언어, 계층 수, 의존성 수, 예상 학습 소요 |
| 프로젝트 개요 | 아키텍처·계층 구조, 설계 철학, 핵심 데이터 흐름, 확장 지점, 외부 의존성 |
| 워크플로우 그래프 (SVG) | 사용자 → API → 코어 → 전송 → 외부 라이브러리. 노드를 누르면 해당 모듈로 이동 |
| 디렉토리 트리 | 접고 펼치는 사이드바. 항목별 역할 설명, 핵심 파일 연동 |
| 파이프라인 다이어그램 | 실행 흐름을 단계별로 표시. 단계를 누르면 파일 경로·핵심 함수·읽기 포인트·다음 단계 코드 표시 |
| 모듈 카드 | 먼저 볼 함수, 주석 달린 실제 코드 스니펫, 정독/스킵 가이드, 난이도, 내부/외부 의존 구분 |
| 읽기 순서 가이드 | 번호 매긴 학습 경로와 각 순서의 이유 |
| 검색 | 키워드로 트리·모듈 카드 필터링 |

모든 파일 경로·함수명·행 번호는 실제 코드에서 확인한 것만 쓰며, 생성 후 `ls`/`grep`으로 자가 검증합니다. 외부 CDN 없이 순수 HTML/CSS/JS로 만들어져 사내망에서도 그대로 열립니다.

## 저장소 구조

```
onboard-guide/                    # 마켓플레이스 저장소 루트
├── .claude-plugin/
│   └── marketplace.json          # 마켓플레이스 카탈로그
└── plugins/
    └── onboard-guide/            # 플러그인 본체
        ├── .claude-plugin/plugin.json
        ├── skills/onboarding/SKILL.md
        └── README.md
```

## 업데이트 배포

`plugins/onboard-guide/.claude-plugin/plugin.json`의 `version`을 올린 뒤 push하면, 사용자는 `/plugin marketplace update`로 최신본을 받습니다.

로컬 개발 중이라면 폴더를 직접 등록할 수 있습니다: `/plugin marketplace add /path/to/onboard-guide`
