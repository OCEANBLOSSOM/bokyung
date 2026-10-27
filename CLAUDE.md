# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

바이올리니스트 김보경의 개인 브랜딩 프로젝트. 공개 홈페이지(`index.html`)는 정적 단일 파일 사이트로 GitHub Pages에 배포된다.

같은 폴더에 비공개 자료(`research/`, 이력서 PDF)가 있지만 `.gitignore`로 이 저장소에서는 제외된다. `research/`는 자체 git 저장소(private)로 따로 관리되며, 작업 지침은 `research/CLAUDE.md`에 있다.

## ⚠️ 공개 범위

- 저장소(`OCEANBLOSSOM/bokyung`)는 **public**이다. 커밋된 파일은 GitHub에서 누구나 볼 수 있다
- 이 CLAUDE.md도 커밋되므로 **가격·리서치 내용을 여기에 쓰지 말 것** — `research/CLAUDE.md`(gitignored)에 쓴다
- `_config.yml`의 `exclude`로 `CLAUDE.md`와 원본 사진은 Pages 사이트 URL에서 404가 나지만, GitHub 저장소 화면에서는 보인다
- 커밋 전 `git status`에 `research/`가 잡히지 않는지 확인 (`.gitignore`가 막고 있어야 정상)

## Commands

빌드 시스템·패키지 매니저·테스트 없음:

```bash
open index.html                    # 사이트 로컬 확인 (서버 불필요, 전부 인라인)
git push origin main               # 배포 (GitHub Pages, 반영까지 1~2분)
```

## Architecture

- **index.html**: 전체 사이트. HTML·CSS·JS 전부 인라인 단일 파일 (빌드 스텝·외부 의존성 없음, CDN은 Google Fonts와 gtag.js뿐). 섹션 순서: Hero(프로필 사진 + 이름) → About → Career(Education/Performance/Teaching 3컬럼) → Awards → Contact(전화/이메일/Instagram)
- **reference/**: 프로필 사진. 사이트는 경량화본 `reference/bokyung-kim-profile.jpg`(800×1200, 약 124KB)를 쓴다. 원본 `reference/bokyung kim photo.jpg`(2560×3840, 2.6MB, 파일명에 공백)는 저장소에만 보관하고 Pages 배포에서는 제외. 사진을 교체할 땐 원본에서 `sips -Z 1200 ... --setProperty formatOptions 80`으로 다시 뽑는다
- **_config.yml**: GitHub Pages(Jekyll) 배포 제외 목록
- **sitemap.xml**: 서치콘솔·서치어드바이저 제출용. 페이지 내용을 크게 바꾸면 `lastmod` 갱신

## Deployment

- GitHub Pages: `https://oceanblossom.github.io/bokyung/` (`main` 브랜치 자동 배포, Jekyll 처리)
- 저장소: `git@github.com:OCEANBLOSSOM/bokyung.git`
- 하위 경로 사이트라 `robots.txt`를 둘 수 없다 (검색엔진은 도메인 루트 `oceanblossom.github.io/robots.txt`만 읽음). 개인 도메인을 연결하면 가능

## SEO

- `<head>`: title, description, canonical, `og:*`(카톡 공유 미리보기), `Person` JSON-LD. 모두 절대 URL `https://oceanblossom.github.io/bokyung/` 기준 — **도메인을 바꾸면 canonical·og:url·og:image·JSON-LD url/image·sitemap.xml을 함께 수정**
- h1은 `김보경` 붙여쓰기 (검색어 매칭용). 화면의 글자 간격은 `letter-spacing: 0.71em` + `margin-right: -0.51em`으로 예전 `김 보 경` 모양과 동일하게 맞춘 것
- 섹션 레이블(About/Career/Awards/Contact)은 `<h2 class="label">`
- 이력 정보를 바꾸면 meta description·og:description·JSON-LD의 학력·수상도 함께 확인

## Analytics

- Google Analytics 4 연동: 측정 ID `G-SCKNEFDFKJ`. `index.html` `<head>` 상단의 gtag.js 스니펫으로 로드

## Design Conventions

- CSS 변수 기반 컬러 시스템: `--color-bg`(베이지 `#faf8f5`), `--color-accent`/`--color-light`(골드), `--color-muted`(회색), `--color-text`(다크)
- 폰트: `--font-en`(Cormorant Garamond), `--font-kr`(Noto Serif KR) — Google Fonts CDN
- 모바일 반응형: 768px 브레이크포인트. 히어로는 세로 배치로 전환, Career 그리드는 1컬럼으로
- 한글 텍스트에 `word-break: keep-all` 적용 (단어 단위 줄바꿈)
- 섹션 헤더는 영문 레이블만 사용 (About, Career, Awards, Contact). 반면 **네비게이션 링크는 한글** (소개/경력/수상/연락) — 헤더는 영문, 내비는 한글이 의도된 조합
- 스크롤 애니메이션: `.reveal` 클래스 + IntersectionObserver. `.bow-divider`도 동일 observer로 트리거되어 stroke-draw 애니메이션 재생
- 수상 상세(1위, 대상 등)는 한글 폰트(`--font-kr`) 사용
- 종이 그레인 텍스처: `body::after`에 SVG `feTurbulence` 노이즈를 fixed 오버레이로, `mix-blend-mode: multiply` opacity 0.07 (라이트 배경에서만 보이고 다크 Contact 섹션에선 사라짐)
- Hero 사진 처리: 기본 `filter: saturate(0.92) sepia(0.08)` 워밍 톤, 호버 시 풀컬러 + 1.015 확대. `::before` 의사요소로 골드 외곽 프레임이 호버에 더 또렷해짐
- 섹션 사이 골드 곡선 디바이더(`.bow-divider`): About/Career/Awards/Contact 상단에 280×40 SVG bow-curve + 중앙 다이아 오너먼트. `stroke-dasharray`/`stroke-dashoffset` draw 1.6s + ornament 1s 지연 fade-in
- 사이트 본문의 이력 정보(학력·수상·연주)는 비공개 문서들이 인용하는 원본 — **`index.html`의 이력을 고치면 `research/` 쪽 문구도 함께 확인**할 것
