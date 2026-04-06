---
name: analyze-paper
description: 단일 .docx 논문 파일을 받아 완전한 분석 보고서를 생성하는 원스톱 스킬. paper-reader → paper-analyst → qa-reviewer 파이프라인을 자동 실행.
---

단일 논문 파일의 경로를 받아 완전한 분석 보고서를 생성합니다.

## 실행 순서

**Step 1: 파일 파싱** (`paper-reader` 에이전트 사용)
- pandoc으로 .docx → markdown 변환
- 섹션 구조, Figure/Table, 통계량 추출

**Step 2: 심층 분석** (`paper-analyst` 에이전트 사용)
Step 1 결과를 입력으로 다음 7섹션 분석:
1. 논문 개요
2. 핵심 요약
3. 연구 방법
4. 주요 결과 (수치 전체 포함)
5. Figure & Table 분석
6. 인사이트 및 한계
7. 놓치면 안 될 포인트

**Step 3: 품질 검증** (`qa-reviewer` 에이전트 사용)
- 수치 정확성 교차 검증
- 완결성 확인
- 품질 점수 산출

## 사용법

```
/analyze-paper 논문파일.docx
/analyze-paper "C:/path/to/paper.docx"
```

## 출력
- 7섹션 완전 분석 보고서
- QA 점수 및 검증 결과
- 분석 결과를 `[파일명]_analysis.md`로 저장 (선택)

## 주의사항
- pandoc이 설치되어 있어야 함 (`pandoc --version`으로 확인)
- .docx 파일만 지원 (PDF는 별도 변환 필요)
- 수치/통계/Figure는 절대 생략하지 않음
- 한국어 사용자에게는 한국어로 응답
