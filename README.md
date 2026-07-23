# jacob-plugins — Claude Code 플러그인 마켓플레이스

Claude Code 플러그인을 배포하는 마켓플레이스 저장소입니다.

## 포함된 플러그인

| 플러그인 | 설명 | 명령어 |
| --- | --- | --- |
| **onboard-guide** | 레포를 분석해 인터랙티브 온보딩 문서(`onboarding.html`) 자동 생성 | `/onboard-guide:onboarding` |

## 설치

```
/plugin marketplace add <your-github-id>/onboard-guide-marketplace
/plugin install onboard-guide@jacob-plugins
```

설치 후, 분석할 레포 루트에서 Claude Code를 실행하고 `/onboard-guide:onboarding` 을 입력하면
그 레포 루트에 `onboarding.html` 이 생성됩니다.

## 구조

```
onboard-guide-marketplace/
├── .claude-plugin/
│   └── marketplace.json          # 마켓플레이스 카탈로그
└── plugins/
    └── onboard-guide/            # 플러그인 본체
        ├── .claude-plugin/plugin.json
        ├── skills/onboarding/SKILL.md
        └── README.md
```

## 업데이트

플러그인을 수정한 뒤 저장소에 push 하면, 사용자는 `/plugin marketplace update` 로 최신본을 받습니다.
`plugins/onboard-guide/.claude-plugin/plugin.json` 의 `version` 을 올려야 사용자에게 업데이트로 인식됩니다.
