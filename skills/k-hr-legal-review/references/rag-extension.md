# RAG 확장 가이드 — 벡터 DB 소스 추가

이 문서는 korean-law MCP만으로 운영 중인 스킬에
고용노동부 PDF 등 추가 자료를 벡터 DB로 연동하는 절차를 설명한다.

---

## 언제 이 확장이 필요한가

korean-law MCP 단독 운영 중 아래 상황이 반복될 때 도입을 검토한다.

- 법령 조문은 있지만 "어떻게 적용하는지" 실무 기준이 없을 때
- 고용노동부 행정해석·지침이 판단에 필요할 때
- 특정 업종(제조업, IT, 의료 등) 특화 자료가 필요할 때

---

## 추가 권장 PDF 자료

| 자료명 | 출처 | 우선순위 |
|--------|------|---------|
| 취업규칙 작성 매뉴얼 | 고용노동부 | 높음 |
| 표준 취업규칙 | 고용노동부 | 높음 |
| 근로기준법 해설서 | 고용노동부 | 높음 |
| 직장 내 괴롭힘 판단·예방·대응 매뉴얼 | 고용노동부 | 중간 |
| 포괄임금제 가이드라인 | 고용노동부 | 중간 |
| 재택근무 가이드 | 고용노동부 | 중간 |
| 개인정보보호 실무 안내서 | 개인정보보호위원회 | 중간 |

---

## 구축 절차 요약

### 1단계 — PDF 파이프라인
```bash
pip install pdfplumber sentence-transformers
```
- pdfplumber로 텍스트 추출
- 500~800 토큰 단위로 청킹
- 각 청크에 메타데이터 추가: source, page, category

### 2단계 — 임베딩 & 저장
- 임베딩 모델: `voyage-multilingual-2` (한국어 특화 권장)
- 벡터 DB: Supabase pgvector 또는 Pinecone
- 청크 저장 시 메타데이터 함께 인덱싱

### 3단계 — MCP 서버로 래핑
검색 엔드포인트를 MCP 서버로 노출한다.

```python
# 검색 함수 예시
def search_hr_docs(query: str, top_k: int = 5):
    embedding = embed(query)
    results = vector_db.similarity_search(embedding, top_k)
    return [{"text": r.text, "source": r.metadata["source"],
             "page": r.metadata["page"]} for r in results]
```

### 4단계 — SKILL.md 업데이트
SKILL.md의 **검색 소스 우선순위** 섹션을 아래로 교체한다.

```
[확장 후] 0순위: hr-rag-search MCP → 고용노동부 PDF, 행정해석 사례집
          1순위: korean-law MCP    → 법령 조문, 판례, 행정해석
          2순위: Claude 학습 지식   → 일반적인 노동법 해석
```

compatibility 섹션의 optional_tools에서
`hr-rag-search MCP` 앞의 주석을 제거하고 URL을 추가한다.

---

## 소스 충돌 시 처리 원칙

RAG 결과와 MCP 결과가 다를 경우:
1. 법령 조문(MCP)이 항상 우선
2. RAG 결과는 "실무 적용 기준" 보조 자료로 활용
3. 충돌 내용은 사용자에게 명시: "법령과 행정지침 간 해석 차이가 있습니다"
