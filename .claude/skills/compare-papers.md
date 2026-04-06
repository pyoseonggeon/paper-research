---
name: compare-papers
description: 2편 이상의 .docx 또는 .pdf 논문을 받아 비교 분석 보고서를 생성. 형식 혼합(docx+pdf) 가능. 비교 축을 논문 내용에서 자동 도출. paper-reader → paper-analyst(병렬) → paper-comparator → qa-reviewer 파이프라인.
---

여러 논문 파일을 받아 심층 비교 분석 보고서를 생성합니다. .docx와 .pdf 혼합 입력 지원.

## 실행 순서

**Step 1: 각 논문 파싱** (`paper-reader` 병렬 실행)
- .docx: pandoc 변환
- .pdf: pdftotext 텍스트 추출 + pymupdf Figure 이미지 추출
- 각각의 구조화된 텍스트 생성

**Step 2: 각 논문 개별 분석** (`paper-analyst` 병렬 실행)
- 각 논문의 7섹션 분석
- 특히 연구방법, 주요결과, 통계량에 집중

**Step 3: 비교 분석** (`paper-comparator` 실행)
- Step 2 결과를 모두 입력
- 논문 내용에서 비교 축 자동 도출
- 비교 매트릭스 생성
- 합의점/쟁점 분석
- 종합 평가

**Step 4: 품질 검증** (`qa-reviewer` 실행)
- 비교 결과 교차 검증
- 수치 정확성 확인
- 균형성 평가

## 사용법

```
/compare-papers 논문1.docx 논문2.docx
/compare-papers 논문1.pdf 논문2.pdf
/compare-papers 논문1.docx 논문2.pdf 논문3.docx  # 형식 혼합 가능
/compare-papers "path/to/*.pdf"   # 폴더 내 전체 pdf 비교
/compare-papers "path/to/*.docx"  # 폴더 내 전체 docx 비교
```

## 출력
- 각 논문 개별 요약 (1페이지씩)
- 비교 매트릭스 (표 형식)
- 합의점 / 쟁점 분석
- 종합 평가 및 근거 수준
- QA 검증 점수

## 비교 축 자동 도출 규칙
- 모든 논문이 다루는 공통 요소 → 필수 비교 축
- 논문 간 가장 큰 차이가 있는 요소 → 핵심 비교 축
- 고정된 비교 축 사용 금지 — 항상 내용 기반으로 도출

## 주의사항
- 최소 2편, 최대 10편 권장 (그 이상은 요약 비교로 전환)
- .docx와 .pdf 혼합 입력 가능
- 스캔 PDF는 텍스트 추출 불가 — 해당 논문만 제외하고 진행하거나 사용자에게 알림
- 모든 수치 원문 그대로 유지
- 한국어 사용자에게는 한국어로 응답
