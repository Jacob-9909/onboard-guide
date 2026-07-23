# onboard-guide

레포지토리를 분석해 신규 투입자용 **인터랙티브 온보딩 문서**(`onboarding.html`)를 자동 생성하는 Claude Code 플러그인입니다. 디렉토리 구조, 실행 파이프라인, 핵심 모듈(정독/스킵 가이드·코드 스니펫 포함), 추천 학습 경로를 클릭형 HTML로 시각화합니다.

## 사용법

플러그인 설치 후, 분석할 레포 루트에서 Claude Code를 실행하고:

```
/onboard-guide:onboarding
```

특정 영역만 집중 분석하려면 인자를 넘깁니다:

```
/onboard-guide:onboarding src/core 인증 흐름 위주로
```

실행하면 현재 레포 루트에 `onboarding.html`이 생성됩니다. 브라우저로 바로 열면 됩니다(외부 CDN 의존 없음, 사내망 OK).

## 로컬 테스트

마켓플레이스 없이 바로 테스트하려면:

```bash
claude --plugin-dir ./onboard-guide
```

변경 후에는 `/reload-plugins`로 반영합니다.

## 구조

```
onboard-guide/
├── .claude-plugin/
│   └── plugin.json          # 플러그인 매니페스트
├── skills/
│   └── onboarding/
│       └── SKILL.md         # /onboard-guide:onboarding 정의
└── README.md
```

## 팀 배포

사내 공유는 이 디렉토리를 git 저장소에 올리고 마켓플레이스로 등록하면 됩니다.
자세한 절차: https://code.claude.com/docs/en/plugin-marketplaces

## 짧은 이름(`/onboarding`)으로 쓰고 싶다면

플러그인은 네임스페이스(`/onboard-guide:onboarding`)가 붙습니다. 개인용으로 네임스페이스 없이
`/onboarding`을 쓰려면 `skills/onboarding/SKILL.md`를 `~/.claude/commands/onboarding.md`로
복사하세요. 그러면 모든 레포에서 `/onboarding`으로 실행됩니다.
