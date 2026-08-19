<div align="center">

# 🗺️ Metric Atlas

### Make analytics implementation visible, verifiable, and trustworthy.

이미 존재하는 React·Vite 코드에서 분석 이벤트를 발견하고, 화면 요소와 연결한 뒤, GA4 실측·설정과 대조하여 Analytics Health를 보여주는 도구입니다.

[Main Repository](https://github.com/Metric-Atlas/Metric-Atlas) · [Documentation](https://github.com/Metric-Atlas/Metric-Atlas/tree/main/docs) · [Contributing](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/CONTRIBUTING.md)

<img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-Node.js-3178C6?style=flat-square&logo=typescript&logoColor=white"> <img alt="React and Vite" src="https://img.shields.io/badge/React%20%2B%20Vite-first-646CFF?style=flat-square&logo=vite&logoColor=white"> <img alt="GA4" src="https://img.shields.io/badge/GA4-first-E37400?style=flat-square&logo=googleanalytics&logoColor=white">

</div>

---

## Analytics 코드와 실제 데이터를 하나의 지도로

이벤트 정보는 코드, 문서, 화면, 분석 도구에 흩어지고 시간이 지나면서 서로 어긋납니다. Metric Atlas는 이미 존재하는 코드를 출발점으로 이 흐름을 연결합니다.

~~~text
Existing React + Vite Code
        ↓
Event Detection & JSX Binding
        ↓
Live Event Overlay & Manifest
        ↓
GA4 Observation & Configuration
        ↓
Analytics Health, Search & Query
~~~

## 핵심 기능

- **Event Overlay** — 화면 요소를 호버하여 원본 이벤트명, Emitter, Provider, 파라미터, 코드 위치를 확인합니다.
- **Analytics Health** — Code detected / GA4 observed / GA4 managed / Custom Dimension gap 상태를 서로 대조합니다.
- **PR Analytics Change Report** — Base와 Head Git tree를 스캔하여 이벤트 추가·삭제·Provider·파라미터·warning 변화를 PR에 전달합니다.
- **Search & Query** — 원본 이벤트를 검색하고 GA4 결과를 조회합니다. 자연어 기능은 Core MVP를 막지 않는 선택 기능입니다.

## 설계 원칙

- 사용자 소스파일은 수정하지 않고 빌드 결과에만 overlay metadata를 주입합니다.
- GA4와 GTM을 같은 개념으로 취급하지 않습니다. dataLayer.push는 GTM Emitter이며 목적 Provider를 임의 추론하지 않습니다.
- 지원하지 않는 wrapper, dynamic event, Custom Component binding을 조용히 누락하지 않고 review-needed warning으로 남깁니다.
- GA4 Result Status와 Data Quality Flag를 분리합니다.
- Secret은 브라우저 bundle, localStorage, Git, Manifest에 저장하지 않습니다.
- Database 없이 Single Node Runtime과 인메모리 cache를 사용합니다.

## Local Demo

Node.js 22.18 이상이 필요합니다.

~~~bash
git clone https://github.com/Metric-Atlas/Metric-Atlas.git
cd Metric-Atlas
corepack enable
pnpm install --frozen-lockfile
pnpm demo
~~~

브라우저에서 [http://127.0.0.1:5180](http://127.0.0.1:5180)을 엽니다.

Demo의 Detector, Manifest, DOM binding, Overlay는 현재 소스를 대상으로 실제 동작합니다. GA4 Health와 Query 수치는 안전한 fixture를 사용하므로 API key나 실제 Analytics credential 없이 체험할 수 있습니다.

전체 검증:

~~~bash
pnpm verify
~~~

## 현재 MVP 범위

현재 공식 탐지 기준은 정적 이벤트명의 GA4/GTM 직접 호출, 같은 파일 handler, 네이티브 JSX 요소입니다. Wrapper 호출, 파일 간 호출 그래프, Custom Component 자동 overlay 주입은 아직 공식 지원 범위 밖이며 결과와 warning은 가능한 한 보존합니다.

GA4를 첫 Connector로 개발 중이며, 여러 Provider의 수치를 자동으로 합산하지 않습니다.

## Repository

| Repository | Description |
| --- | --- |
| [Metric-Atlas](https://github.com/Metric-Atlas/Metric-Atlas) | Detector, contracts, Vite plugin, overlay, GA4 connector, runtime, dashboard, CLI가 포함된 main monorepo |

## 함께 만들기

프로젝트는 Core MVP를 개발 중입니다. 이슈를 열기 전에 [Source of Truth](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/docs/00-project-source-of-truth.md), [Architecture](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/docs/04-system-architecture.md), [Contributing Guide](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/CONTRIBUTING.md)를 확인해 주세요.
