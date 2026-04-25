# k-hr-legal-review

Claude 스킬 — 한국 인사노무 문서 법적 검토

## 설명

취업규칙, 사규, 인사규정 등 내부 문서를 한국 노동법령 기준으로 검토하는 Claude 전용 스킬입니다.

## 사전 요건: korean-law MCP 설치

이 스킬은 **[korean-law MCP](https://github.com/chrisryugj/korean-law-mcp)** 가 설치되어 있어야 작동합니다.

**Claude Code (CLI / IDE)**:

```bash
claude mcp add korean-law npx -y korean-law-mcp
```

**Claude Desktop / claude.ai 사용자**: 설치 방법은 [korean-law-mcp GitHub](https://github.com/chrisryugj/korean-law-mcp)를 참고하세요.

## 설치 방법

### Claude Code (CLI / IDE 확장)

```
/plugin install zenajo/hr-legal-review
```

업데이트:

```
/plugin update k-hr-legal-review
```

### Claude Desktop / Claude.ai

1. [`skills/k-hr-legal-review/SKILL.md`](skills/k-hr-legal-review/SKILL.md) 파일 다운로드
2. Claude Desktop → Skills → `+` → **Upload a skill** 선택
3. 다운로드한 `SKILL.md` 파일 업로드

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
