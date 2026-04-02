# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

바이올리니스트 김보경의 개인 소개 홈페이지. 단일 `index.html` 파일로 구성된 정적 사이트.

## Architecture

- **index.html**: 전체 사이트 (HTML + CSS + JS 인라인). 섹션: Hero(프로필 사진), About, Career(Education/Performance/Teaching), Awards, Contact(전화/이메일/Instagram)
- **reference/**: 원본 자료 (이력서 PDF, 프로필 사진). 사진은 히어로 섹션에서 상대경로로 참조됨

## Deployment

- GitHub Pages로 배포: `https://oceanblossom.github.io/bokyung`
- 저장소: `git@github.com:OCEANBLOSSOM/bokyung.git`
- `main` 브랜치에서 자동 배포

## Design Conventions

- 폰트: Cormorant Garamond(영문) + Noto Serif KR(한글), Google Fonts CDN
- 컬러: 뉴트럴 베이지 배경(`#faf8f5`), 골드 포인트(`#8b6914`, `#c9a84c`)
- 모바일 반응형 (768px 브레이크포인트)
- 스크롤 시 IntersectionObserver 기반 페이드인 애니메이션
