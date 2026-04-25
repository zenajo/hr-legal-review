# k-hr-legal-review

Claude 스킬 — 한국 인사노무 문서 법적 검토

## 설명

취업규칙, 사규, 인사규정 등 내부 문서를 한국 노동법령 기준으로 검토하는 Claude 전용 스킬입니다.

## 필수 도구

- `korean-law` MCP 연결 필요

## 설치 방법

이 저장소를 GitHub에 올린 후:

```
/plugin install {github-username}/hr-legal-review
```

## 파일 구조

```
hr-legal-review/
├── .claude-plugin/
│   └── plugin.json              # 플러그인 메타데이터
├── skills/
│   └── k-hr-legal-review/
│       ├── SKILL.md             # 스킬 메인 파일
│       └── references/
│           └── rag-extension.md # 추후 RAG 확장 가이드
└── README.md
```

## 버전 히스토리

| 버전 | 날짜 | 변경사항 |
|------|------|---------|
| v1.0.0 | 2026-04-24 | 초기 릴리즈 |
| v1.1.0 | 2026-04-25 | 플러그인 구조로 변환, 스킬명 k-hr-legal-review로 변경 |
