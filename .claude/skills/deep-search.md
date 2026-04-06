---
name: deep-search
description: 특정 주제에 대한 체계적 문헌 조사 스킬. literature-surveyor 에이전트를 사용해 웹 검색 + 로컬 파일 통합 탐색. 연구 동향, 핵심 논문, 연구 공백 파악.
---

주제 키워드를 받아 체계적인 문헌 조사를 수행합니다.

## 실행 순서

**Step 1: 범위 설정**
- 주제 키워드 정제
- 검색 연도 범위 설정 (기본: 최근 5년 + seminal papers)
- 검색 데이터베이스 선택

**Step 2: 문헌 탐색** (`literature-surveyor` 에이전트 실행)
- 로컬 .docx 및 .pdf 파일 탐색
- 웹 검색 (Google Scholar, PubMed, arXiv, Semantic Scholar)
- 결과 통합 및 중복 제거

**Step 3: 결과 정리**
- 핵심 논문 / 최신 논문 목록화
- 연구 동향 타임라인
- 연구 공백 식별

## 사용법

```
/deep-search [주제]
/deep-search [주제] --years 2020-2024
/deep-search [주제] --include-local  # 로컬 docx 파일 포함
/deep-search [주제] --field clinical  # 분야 지정 (clinical/cs/social/basic-science)
```

## 검색 대상 데이터베이스
- Google Scholar: 광범위한 학술 문헌
- PubMed/MEDLINE: 의학/생명과학
- arXiv: 물리학/CS/수학 (preprint 포함)
- Semantic Scholar: AI 기반 추천 및 인용 분석
- 로컬 프로젝트 디렉토리: 기존에 수집된 .docx 및 .pdf 파일

## 출력
- 검색 개요 (키워드, 기간, 데이터베이스)
- 로컬 논문 목록
- 핵심 논문 10편 (seminal papers)
- 최신 논문 20편
- 연구 동향 타임라인
- 주요 연구자 및 그룹
- 연구 공백 분석
- 추천 읽기 순서

## 주의사항
- 실제 존재하는 논문만 포함 (DOI/URL 확인)
- 인용 수 등 수치는 검색 시점 기준
- 한국어 사용자에게는 한국어로 응답
- 로컬 .docx/.pdf 파일은 `paper-reader`로 추가 파싱 가능
