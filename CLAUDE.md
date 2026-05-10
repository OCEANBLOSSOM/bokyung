# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

바이올리니스트 김보경의 개인 소개 홈페이지. 단일 `index.html` 파일로 구성된 정적 사이트 (HTML + CSS + JS 모두 인라인).

## Architecture

- **index.html**: 전체 사이트. 섹션 순서: Hero(프로필 사진 + 이름) → About → Career(Education/Performance/Teaching 3컬럼) → Awards → Contact(전화/이메일/Instagram)
- **reference/**: 원본 자료 (이력서 PDF, 프로필 사진). 프로필 사진은 히어로에서 `reference/bokyung kim photo.jpg` 상대경로로 참조

## Deployment

- GitHub Pages: `https://oceanblossom.github.io/bokyung`
- 저장소: `git@github.com:OCEANBLOSSOM/bokyung.git` (`main` 브랜치 자동 배포)
- 변경 후 `git push origin main`으로 배포. 반영까지 1~2분 소요

## Analytics

- Google Analytics 4 연동: 측정 ID `G-SCKNEFDFKJ`. `index.html` `<head>` 상단의 gtag.js 스니펫으로 로드

## Design Conventions

- CSS 변수 기반 컬러 시스템: `--color-bg`(베이지 `#faf8f5`), `--color-accent`/`--color-light`(골드), `--color-muted`(회색), `--color-text`(다크)
- 폰트: `--font-en`(Cormorant Garamond), `--font-kr`(Noto Serif KR) — Google Fonts CDN
- 모바일 반응형: 768px 브레이크포인트. 히어로는 세로 배치로 전환, Career 그리드는 1컬럼으로
- 한글 텍스트에 `word-break: keep-all` 적용 (단어 단위 줄바꿈)
- 섹션 헤더는 영문 레이블만 사용 (About, Career, Awards, Contact)
- 스크롤 애니메이션: `.reveal` 클래스 + IntersectionObserver
- 수상 상세(1위, 대상 등)는 한글 폰트(`--font-kr`) 사용
