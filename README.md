# k-hr-legal-review

Claude 스킬 — 한국 인사노무 노무 리스크 사전 검토

## 설명

인사담당자가 채용·계약·성과평가·징계 등 인사 기획·운영 전반에서 노무 리스크를 사전에 인지할 수 있도록 돕는 Claude 전용 스킬입니다. 완성된 문서뿐 아니라 기획 단계의 아이디어·제도 초안도 검토합니다.

## 사전 요건: korean-law MCP 설치

이 스킬은 **[korean-law MCP](https://github.com/chrisryugj/korean-law-mcp)** 가 설치되어 있어야 작동합니다.

**Claude Code (CLI / IDE)**:

```bash
claude mcp add korean-law npx -y korean-law-mcp
```

**Claude Desktop / claude.ai 사용자**: 설치 방법은 [korean-law-mcp GitHub](https://github.com/chrisryugj/korean-law-mcp)를 참고하세요.

## 설치 방법

### Claude Code (CLI / IDE 확장)

**1. 마켓플레이스 등록** (최초 1회):

```bash
claude plugin marketplace add zenajo/hr-legal-review
```

**2. 플러그인 설치**:

```bash
claude plugin install k-hr-legal-review
```

**3. Claude Code 재시작** — 재시작 후 인사 문서를 붙여넣으면 스킬이 자동으로 트리거됩니다.

업데이트:

```bash
claude plugin update k-hr-legal-review
```

### Claude Desktop / Claude.ai

1. [`skills/k-hr-legal-review/SKILL.md`](skills/k-hr-legal-review/SKILL.md) 파일 다운로드
2. Claude Desktop → Settings → Skills → `+` → **Upload a skill** 선택
3. 다운로드한 `SKILL.md` 파일 업로드

## 파일 구조

```
hr-legal-review/
├── .claude-plugin/
│   ├── plugin.json              # 플러그인 메타데이터
│   └── marketplace.json         # 마켓플레이스 등록 정보
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
| v1.1.1 | 2026-04-29 | marketplace.json 추가 — CLI 2단계 설치 지원 |
