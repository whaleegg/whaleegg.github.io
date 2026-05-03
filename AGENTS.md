# Repository Guidelines

## Project Scope & Structure
이 저장소는 Chirpy Jekyll 테마를 기반으로 운영하는 개인 기술 블로그이며, 범용 테마 패키지 저장소로 다루지 않습니다. `_posts/`는 핵심 콘텐츠 영역, `_tabs/`는 상단 고정 페이지, `_layouts/`와 `_includes/`는 테마 오버라이드, `_javascript/`와 `_sass/`는 소스 에셋, `assets/`는 배포되거나 생성된 정적 파일로 취급합니다. 공통 설정과 메타데이터는 `_config.yml` 및 `_data/`에 있습니다.

Codex는 테마 자체의 추상적인 개선보다 실제 블로그 운영에 필요한 콘텐츠 품질, 렌더링 안정성, SEO 메타데이터, 배포 안전성을 우선합니다. 사용자가 명시하지 않은 대규모 디자인 리뉴얼이나 구조 개편은 기본값으로 수행하지 않습니다.

## Build, Test, and Development Commands
- `npm install`: lint 및 asset build에 필요한 JS 도구를 설치합니다.
- `npm run build`: 번들된 JS와 CSS를 다시 생성합니다.
- `npm test`: `eslint`와 `stylelint`를 실행합니다.
- `bash tools/run.sh`: 로컬 Jekyll 미리보기 서버를 실행합니다.
- `bash tools/run.sh -p`: `JEKYLL_ENV=production`으로 미리보기합니다.
- `bash tools/test.sh`: 전체 사이트를 빌드하고 `htmlproofer`까지 실행합니다. 레이아웃, 설정, 내비게이션, 링크가 많이 바뀐 경우 머지 전에 사용합니다.

## Post Writing Workflow
새 글은 `_posts/` 아래에 `YYYY-MM-DD-title.md` 형식으로 작성합니다. 예: `_posts/2026-04-23-embedded-ai-notes.md`. 기본 `front matter`는 아래 형식을 권장합니다.

```yaml
---
title: Embedded AI Notes
date: 2026-04-23 09:00:00 +0900
categories: [Study, AI]
tags: [llm, edge-ai]
description: Short summary for feed and post header.
---
```

`tags`는 소문자로 유지합니다. `categories`는 보통 1~2단계 이내로 제한합니다. 이 블로그의 기본 카테고리 체계는 "기술 분야"보다 "글의 성격"을 먼저 잡는 방식을 우선합니다.

- 상위 카테고리 기본값: `Project`, `Study`, `Career`
- 하위 카테고리 예시: `Embedded`, `AI`, `Robotics`, `Control`, `SLAM`, `Simulation`, `Portfolio`, `Program`, `Jekyll`

카테고리는 "이 글을 어떤 관점으로 찾게 할 것인가"를 기준으로 고릅니다. 한 글이 임베디드, AI, 로보틱스 주제를 모두 포함하더라도 상위 카테고리는 하나의 대표 성격만 선택하고, 나머지 기술 요소는 태그로 풀어냅니다.

예시:

- 구현 중심 로봇 프로젝트: `categories: [Project, Robotics]`
- SLAM/제어 공부 정리: `categories: [Study, SLAM]` 또는 `categories: [Study, Control]`
- 포트폴리오용 프로젝트 회고: `categories: [Career, Portfolio]`
- 교육 과정/취업 활동 기록: `categories: [Career, Program]`

회사명, 과정명, 프레임워크명, 플랫폼명은 가능하면 카테고리보다 태그에 둡니다. 예: `hyundai-autoever`, `h-mobility-class`, `isaac-sim`, `isaac-lab`, `ros2`, `jetson`.

블로그/Jekyll 운영 관련 글은 기존 Chirpy 샘플 계열 카테고리를 유지합니다. 즉 블로그 자체를 다루는 글은 새 체계의 `Blog` 상위 카테고리로 통합하지 않고, 필요하면 기존처럼 `categories: [Blogging, Tutorial]`, `categories: [Blogging, Demo]` 등을 사용합니다.

`toc: false`, `comments: false`, `pin: true`, `math: true` 같은 옵션은 필요한 글에서만 사용합니다. 이미지는 `assets/img/...` 아래에 두고 root-relative path로 참조합니다. 가능하면 `width`와 `height`도 함께 지정해 레이아웃 흔들림을 줄입니다.

이미지 자산은 아래 구조를 기본값으로 사용합니다.

- 글별 이미지: `assets/img/posts/YYYYMMDD-slug/`
- 사이트 공통 이미지: `assets/img/site/`
- 여러 글에서 재사용하는 공용 이미지: `assets/img/commons/`

포스트 본문과 `front matter.image`는 가능한 한 `/assets/img/...` 절대경로를 사용합니다. 테마 데모용 외부 CDN 경로나 저장소 밖 자산에 의존하는 링크는 장기 운영 시 깨질 수 있으므로 기본값으로 사용하지 않습니다.

새 글이나 기존 글을 다듬을 때는 아래 기준을 우선합니다.

- `description`은 가능한 한 비워 두지 않고, 피드와 SEO에 맞게 1~2문장으로 명확하게 작성합니다.
- 제목은 검색 가능한 표현을 우선하며, 지나치게 모호하거나 감상문 같은 제목은 피합니다.
- 한국어 본문은 번역투를 줄이고 기술 블로그 문체로 자연스럽게 다듬습니다.
- 코드 블록에는 가능한 한 언어 식별자를 명시합니다.
- 카테고리와 태그는 기존 글들과 충돌하지 않도록 일관성을 확인합니다.
- 외부 서비스명, 라이브러리명, 모델명, 버전은 사용자가 최신성을 기대할 수 있으므로 단정하지 말고 확인 가능한 범위에서만 서술합니다.

초안 작성이나 교정 요청을 받을 때 Codex는 단순 문장 생성에 그치지 말고 `front matter`, 본문 구조, 요약, 제목, 태그까지 함께 점검합니다.

## Coding Style & Naming Conventions
`.editorconfig` 규칙을 따릅니다. 기본은 UTF-8, LF, 들여쓰기 2칸입니다. JavaScript, CSS, SCSS는 single quote를 사용하고, YAML은 double quote를 우선합니다. 수정은 먼저 `_javascript/`와 `_sass/`의 소스 파일에서 하고, 필요할 때만 `assets/js/dist/` 또는 `assets/css/` 결과물을 다시 생성합니다. 작업과 무관한 대규모 포맷 변경은 피합니다.

HTML/Liquid, YAML, Markdown을 수정할 때도 기존 저장소의 스타일을 우선 따릅니다. 사용자가 요청하지 않은 파일 이동, permalink 변경, slug 변경은 기존 링크를 깨뜨릴 수 있으므로 신중하게 다룹니다.

## Testing Guidelines
새 포스트 추가나 단순 오타 수정처럼 콘텐츠만 바뀌는 경우에는 `bash tools/run.sh`로 로컬 미리보기만 확인해도 충분한 경우가 많습니다. JS, SCSS, 또는 lint 대상 파일을 수정했다면 `npm test`를 실행합니다. `_config.yml`, `layout/include`, permalink 동작, 링크 구조처럼 생성 결과에 영향을 주는 변경은 `bash tools/test.sh`까지 실행합니다.

가능하면 아래 우선순위로 검증합니다.

- 콘텐츠만 변경: front matter, 링크, 이미지 경로, Markdown 렌더링을 우선 확인합니다.
- `_config.yml`, `_tabs/`, `_layouts/`, `_includes/` 변경: 내비게이션, permalink, 메타 태그, 댓글, analytics 동작에 영향이 없는지 확인합니다.
- `_javascript/`, `_sass/` 변경: `npm test`와 필요한 asset build를 실행합니다.
- 링크 구조나 템플릿 변경: `bash tools/test.sh`까지 실행해 생성 결과를 확인합니다.

테스트를 실행하지 못했거나 환경상 생략했다면 최종 응답에서 그 사실을 명확히 밝힙니다.

## Review Priorities
Codex가 리뷰를 수행할 때는 아래 순서로 봅니다.

1. 배포를 깨뜨릴 수 있는 설정 오류, Liquid/Jekyll 오류, 잘못된 경로
2. permalink, navigation, includes/layouts 변경으로 인한 렌더링 회귀
3. 누락된 `front matter`, 잘못된 날짜/타임존, 분류 체계 불일치
4. SEO 관련 누락: `description`, 제목 품질, 대표 이미지, 소셜 메타
5. 오탈자, 문체, 표현 품질

단순 요약보다 실제 문제와 리스크를 먼저 보고합니다.

## Commit & Pull Request Guidelines
커밋 메시지는 `feat:`, `fix:`, `chore:` 같은 Conventional Commits 형식을 사용합니다. 한 커밋에는 한 가지 주제만 담고, 명령문 형태로 짧게 작성합니다. PR에는 사용자 관점에서 무엇이 바뀌는지 요약하고, 관련 이슈나 메모가 있으면 연결합니다. UI 또는 렌더링 결과가 바뀌면 스크린샷을 첨부합니다. 생성된 asset이 함께 바뀌었다면 어떤 소스 파일을 수정했고 어떤 build 명령을 실행했는지 PR 설명에 적습니다.

콘텐츠 중심 변경이라면 PR 설명에 아래 항목을 포함하면 좋습니다.

- 어떤 글이 추가 또는 수정되었는지
- SEO 메타나 카테고리/태그 체계에 변화가 있는지
- 이미지나 외부 링크가 추가되었는지
- 어떤 검증 명령을 실행했는지, 또는 실행하지 못했다면 그 이유
