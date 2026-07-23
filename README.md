# jacob-plugins — Claude Code 플러그인 마켓플레이스

레포지토리를 분석해 **신규 투입자용 인터랙티브 온보딩 문서**를 자동 생성하는 Claude Code 플러그인을 배포하는 마켓플레이스 저장소입니다.

> Repo: https://github.com/Jacob-9909/onboard-guide · Marketplace 이름: `jacob-plugins`

---

## 어떤 건가요?

낯선 코드베이스에 처음 투입됐을 때, "어디부터 어떻게 읽어야 하는지"를 알려주는 **단일 파일 HTML 온보딩 문서**를 만들어 줍니다.

`onboard-guide` 플러그인의 `onboarding` 스킬을 실행하면, Claude Code가 **현재 열려 있는 레포(cwd)를 실제로 분석**해서 레포 루트에 `onboarding.html` 한 개를 생성합니다. 추측이 아니라 실제 파일·함수·행 번호를 근거로 작성되며, 외부 CDN 없이 vanilla HTML/CSS/JS로만 만들어져 **사내망에서도 그대로 열립니다**.

### 생성되는 문서에 담기는 것

| 구성 | 내용 |
| --- | --- |
| **KPI 스트립** | 파일 수, 코드 라인, 주요 언어, 계층 수, 의존성 수, 예상 학습 소요 |
| **프로젝트 개요** | 아키텍처/계층 구조·설계 철학, 핵심 데이터 흐름, 공식 확장 지점, 외부 의존성과 역할 |
| **워크플로우 그래프 (SVG)** | 사용자 → API → 코어 → 전송 → 외부 라이브러리 계층 배치. 노드 클릭 시 해당 모듈로 스크롤·하이라이트 |
| **디렉토리 트리** | 접고 펼치는 사이드바. 각 항목 역할 설명, 핵심 파일 클릭 연동 |
| **파이프라인 다이어그램** | 실행 흐름을 단계별 노드로. 클릭 시 파일 경로·핵심 함수·읽기 포인트·다음 단계 코드 표시 |
| **모듈 카드** | 최우선으로 볼 함수, 실제 코드 스니펫(주석 설명), 정독/스킵 가이드, 난이도·코드량, 내부/외부 의존 구분 |
| **읽기 순서 가이드** | 번호 매겨진 학습 경로 + "왜 이 순서인지" 이유 |
| **검색** | 키워드로 트리·모듈 카드 필터링 |

모든 파일 경로·함수명·행 번호는 실제 코드에서 확인된 것만 사용하며(환각 금지), 생성 후 `ls`/`grep`으로 자가 검증합니다.

---

## 설치

Claude Code에서:

```
/plugin marketplace add Jacob-9909/onboard-guide
/plugin install onboard-guide@jacob-plugins
```

설치 후 Claude Code를 재시작하면 플러그인이 로드됩니다.

> 로컬 개발 중이라면 GitHub 대신 로컬 경로로도 등록할 수 있습니다:
> `/plugin marketplace add /path/to/onboard-guide`

## 사용법

1. **분석할 레포 루트**에서 Claude Code를 실행합니다.
2. `onboarding` 스킬을 실행합니다 (`onboard-guide:onboarding`).
3. 그 레포 루트에 `onboarding.html`이 생성됩니다. 브라우저로 열면 됩니다.

특정 디렉토리나 관점에 집중하고 싶으면 인자로 지정할 수 있습니다 (예: 특정 하위 모듈 경로).

---

## 저장소 구조

```
onboard-guide/                      # 마켓플레이스 저장소 루트
├── .claude-plugin/
│   └── marketplace.json            # 마켓플레이스 카탈로그
├── README.md                       # 이 파일
└── plugins/
    └── onboard-guide/              # 플러그인 본체
        ├── .claude-plugin/plugin.json
        ├── skills/onboarding/SKILL.md
        └── README.md
```

## 업데이트

플러그인을 수정한 뒤 저장소에 push 하면, 사용자는 `/plugin marketplace update`로 최신본을 받습니다.
사용자에게 업데이트로 인식되게 하려면 `plugins/onboard-guide/.claude-plugin/plugin.json`의 `version`을 올려야 합니다.

```
# 예: 1.0.0 → 1.1.0 으로 version 수정 후
git add -A && git commit -m "feat: ..." && git push
```
