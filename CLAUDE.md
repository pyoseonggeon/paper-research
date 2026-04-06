# Paper Research Harness

학술 논문(.docx) 분석/요약/비교를 위한 Claude Code harness.

## 에이전트 구성

| 에이전트 | 역할 | 주요 도구 |
|---------|------|---------|
| `paper-reader` | .docx → 구조화 텍스트 (pandoc) | Bash, Read, Write |
| `paper-analyst` | 7섹션 심층 분석 | Read |
| `paper-comparator` | 다중 논문 비교 (비교축 자동도출) | Read |
| `literature-surveyor` | 웹+로컬 문헌 탐색 | WebSearch, WebFetch, Read |
| `qa-reviewer` | 분석 품질 검증 | Read |

## 스킬 (슬래시 명령)

| 스킬 | 사용법 | 설명 |
|------|--------|------|
| `/analyze-paper` | `/analyze-paper 논문.docx` | 단일 논문 완전 분석 |
| `/compare-papers` | `/compare-papers A.docx B.docx` | 다중 논문 비교 |
| `/deep-search` | `/deep-search [주제]` | 문헌 조사 |
| `/research-orchestrator` | `/research-orchestrator [요청]` | 복잡한 작업 자동 조율 |

## 핵심 규칙
- **수치/통계/Figure는 절대 생략 금지** — p값, CI, n수, OR 등 모두 원문 그대로
- **비교 축은 논문 내용에서 자동 도출** — 고정 템플릿 사용 금지
- **한국어 사용자에게는 한국어로 응답**
- **QA 검증 없이 최종 보고서 발행 금지**

## 전제 도구
- pandoc 3.x 이상 (.docx 처리): 설치됨 (`pandoc --version`)
- pdftotext (.pdf 텍스트 추출): 설치됨 (`pdftotext -v`)
- pymupdf 1.27+ (.pdf 이미지 추출): 설치됨 (`python -c "import fitz; print(fitz.__version__)"`)
- python-docx (pandoc fallback용): `pip install python-docx`

## 디렉토리 구조
```
paper-research/
├── CLAUDE.md           # 이 파일
├── .claude/
│   ├── agents/
│   │   ├── paper-reader.md
│   │   ├── paper-analyst.md
│   │   ├── paper-comparator.md
│   │   ├── literature-surveyor.md
│   │   └── qa-reviewer.md
│   └── skills/
│       ├── research-orchestrator.md
│       ├── analyze-paper.md
│       ├── compare-papers.md
│       └── deep-search.md
└── papers/             # 분석할 논문 .docx 파일 보관 권장
```
