<div align="center">

<img src="./assets/metric_atlas_logo.png" width="210" alt="Metric Atlas 로고" />

# Metric Atlas

### 분석 이벤트 구현을 눈에 보이고, 검증 가능하며, 신뢰할 수 있게.

[English](https://github.com/Metric-Atlas/.github/blob/main/profile/README.md) · **한국어**

Metric Atlas는 React·Vite 애플리케이션을 위한 소스 코드 중심의 Analytics Observability 도구입니다. 기존 프론트엔드 코드에서 분석 이벤트를 발견하고, 실제 화면 요소와 연결하며, 구현 상태를 GA4 실측 데이터 및 설정과 대조합니다.

[저장소](https://github.com/Metric-Atlas/Metric-Atlas) · [문서](https://github.com/Metric-Atlas/Metric-Atlas/tree/main/docs) · [기여 안내](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/CONTRIBUTING.md)

![TypeScript](https://img.shields.io/badge/TypeScript-Node.js-3178C6?style=flat-square&logo=typescript&logoColor=white)
![React and Vite](https://img.shields.io/badge/React%20%2B%20Vite-first-646CFF?style=flat-square&logo=vite&logoColor=white)
![GA4](https://img.shields.io/badge/GA4-analytics%20health-E37400?style=flat-square&logo=googleanalytics&logoColor=white)
![Self-hosted](https://img.shields.io/badge/deployment-self--hosted-0F766E?style=flat-square)
![No database](https://img.shields.io/badge/database-none-334155?style=flat-square)
![Contributions welcome](https://img.shields.io/badge/contributions-welcome-14B8A6?style=flat-square)

</div>

---

## 분석 이벤트 구현은 추측에 의존해서는 안 됩니다

이벤트 정보는 보통 소스 코드, 스프레드시트, 분석 대시보드, 그리고 구현을 기억하는 사람들에게 흩어져 있습니다. 애플리케이션이 바뀌면 이 정보들은 서로 다른 상태가 됩니다.

Metric Atlas는 이미 존재하는 구현에서 출발해 살아 있는 Analytics Map을 만듭니다.

```text
기존 프론트엔드 코드
        ↓
이벤트 호출 탐지 및 UI 요소 연결
        ↓
구조화된 Event Manifest 생성
        ↓
코드와 GA4 실측·설정 대조
        ↓
제품 화면과 Pull Request에서 Analytics Health 제공
```

<table>
  <tr>
    <td width="33%" valign="top"><h3>탐지</h3>프론트엔드 코드에서 이벤트 호출, 파라미터, Emitter, Provider, 코드 위치와 UI 연결을 찾습니다.</td>
    <td width="33%" valign="top"><h3>검증</h3>코드 구현을 GA4 실측, 관리 이벤트, 품질 신호, Custom Dimension 등록 상태와 대조합니다.</td>
    <td width="33%" valign="top"><h3>전달</h3>라이브 오버레이, Health Dashboard, 검색과 Pull Request Report로 분석 정보를 전달합니다.</td>
  </tr>
</table>

## Metric Atlas가 연결하는 정보

Metric Atlas는 또 하나의 분석 대시보드가 아닙니다. 서로 다른 도구에 흩어진 근거를 연결하는 것이 핵심입니다.

| 근거 | Metric Atlas가 연결하는 정보 |
|---|---|
| 프론트엔드 구현 | 원본 이벤트명, 파라미터, Emitter, Provider와 코드 위치 |
| 제품 인터페이스 | 탐지된 이벤트와 연결된 실제 네이티브 UI 요소 |
| Analytics Provider | GA4 관측 결과, Reporting Time Zone, 관리 이벤트와 데이터 품질 플래그 |
| Analytics 설정 | 이벤트 파라미터의 Built-in 및 Custom Dimension 등록 상태 |
| 코드 리뷰 | Base와 Head Git Revision 사이의 의미 있는 이벤트 변경 |

## 핵심 기능

### 이벤트 탐지와 라이브 오버레이

빌드 과정에서 지원하는 분석 호출을 탐지하고 Event Manifest를 생성한 뒤, 이벤트를 네이티브 JSX 요소에 연결합니다. 오버레이를 켜고 추적된 요소에 마우스를 올리면 이벤트명, Emitter, Provider, 파라미터, Binding Confidence와 코드 위치를 확인할 수 있습니다.

사용자 소스파일은 수정하지 않습니다. `data-atlas-id` 메타데이터는 빌드 결과에만 주입됩니다.

### Code ↔ GA4 Analytics Health

대시보드는 단순 Event Count가 아니라 구현 상태에서 시작합니다. 다음 항목을 검토할 수 있습니다.

- 코드에서 탐지되고 GA4에서도 관측된 이벤트
- 코드에는 있지만 최근 GA4 조회 결과가 없는 이벤트
- GA4에는 있지만 현재 코드에서 탐지되지 않은 이벤트
- GA4 자동 수집 및 Enhanced Measurement 관리 이벤트
- Custom Dimension으로 등록되지 않은 이벤트 파라미터
- Thresholding, 데이터 손실 및 최근 데이터 변동 가능성

최근 GA4 결과가 없다는 이유만으로 구현 오류라고 단정하지 않으며, Result Status와 Data Quality Flag를 분리해 불확실성을 그대로 보여줍니다.

### Pull Request Analytics Change Report

CLI는 현재 Checkout을 수정하지 않고 Base와 Head Git Tree를 스캔할 수 있습니다. PR Report는 추가·삭제된 이벤트, Provider 또는 Emitter 변경, 파라미터 변경, 해결되지 않은 바인딩, 동적 이벤트명과 미지원 패턴을 코드 리뷰 흐름에 전달합니다.

### 검색과 선택적 자연어 질의

원본 이벤트명, Provider, 코드 위치와 Health 상태로 이벤트를 검색할 수 있습니다. 선택적 자연어 질의는 같은 검증된 Event Catalog를 사용하며, 존재하지 않는 이벤트를 만들거나 원본 이벤트명을 영구적으로 바꾸지 않습니다.

## 화면 살펴보기

<p align="center">
  <img src="./assets/overview.png" width="100%" alt="Metric Atlas Analytics Health 화면" />
</p>

<table>
  <tr>
    <td width="50%"><img src="./assets/events.png" alt="Metric Atlas Event Explorer" /></td>
    <td width="50%"><img src="./assets/query.png" alt="Metric Atlas Query 화면" /></td>
  </tr>
</table>

## 무엇이 다른가요?

| 일반적인 질문 | Metric Atlas의 접근 방식 |
|---|---|
| “Tracking 문서가 아직 최신 상태인가?” | 현재 구현을 다시 분석해 Manifest 생성 |
| “이 이벤트는 어느 버튼에서 전송되는가?” | 이벤트 호출, 코드 위치와 실제 화면 요소 연결 |
| “코드에 있는 이벤트가 GA4에서도 보이는가?” | 코드 상태와 정규화된 GA4 관측 결과 대조 |
| “이 커스텀 파라미터를 리포트에서 사용할 수 있는가?” | Built-in Metadata와 Custom Dimension 등록 확인 |
| “이번 PR에서 분석 이벤트가 어떻게 바뀌었는가?” | Base와 Head 사이의 의미 기반 Event Diff 생성 |

Metric Atlas는 Tracking Plan과 BI 도구를 대체하지 않고 보완합니다. 구현과 실제 측정 사이의 경계를 관측 가능하게 만드는 것이 역할입니다.

## 명확한 경계를 지킵니다

- GA4와 GTM을 같은 개념으로 취급하지 않습니다. `dataLayer.push(...)`는 GTM Emitter이며 자동으로 GA4 이벤트가 되지 않습니다.
- 래퍼 호출, 동적 이벤트명, Custom Component Overlay와 해결되지 않은 바인딩을 조용히 무시하지 않고 경고로 표시합니다.
- 원본 이벤트명을 자동 번역하거나 새로운 의미로 재정의하지 않습니다.
- 브라우저 코드는 GA4 또는 LLM Credential을 받지 않습니다. Secret은 로컬 Node Runtime에서만 처리합니다.
- Provider별 응답은 공유 계약 뒤에서 정규화합니다.
- Database 없이 Manifest를 다시 생성하고 Analytics 응답은 인메모리로 캐시합니다.

## 아키텍처

| 계층 | 책임 |
|---|---|
| Detector와 Vite Plugin | AST 분석, 같은 파일 JSX Binding, Manifest 생성과 빌드 결과 주입 |
| Overlay | 실행 중인 제품 화면에서 라이브 이벤트 메타데이터 표시 |
| GA4 Connector와 Health Engine | 이벤트 관측, 관리 이벤트 분류, 등록 누락, 기간 비교와 품질 신호 |
| Node Runtime | 정적 파일, Manifest, Analytics API, Credential, Guard와 인메모리 캐시 |
| Dashboard와 Query | Health 탐색, 이벤트 검색, 상세 화면과 선택적 자연어 기능 |
| CLI와 GitHub Actions | 저장소 스캔, 의미 기반 Manifest Diff, Artifact와 PR Report |

공유 Zod Schema가 Producer와 Consumer의 계약을 맞추며, Detector와 Connector Adapter는 독립적으로 확장할 수 있습니다.

## 로컬에서 체험하기

Node.js 22.18 이상이 필요합니다. Demo 실행에는 GA4 Credential이 필요하지 않습니다.

```bash
git clone https://github.com/Metric-Atlas/Metric-Atlas.git
cd Metric-Atlas
corepack pnpm install --frozen-lockfile
corepack pnpm demo
```

[http://127.0.0.1:5180](http://127.0.0.1:5180)을 엽니다.

Demo는 실제 로컬 소스 코드를 대상으로 탐지, Manifest 생성, DOM Binding과 Overlay를 실행합니다. GA4 Health와 Query 화면은 안전한 Fixture를 사용하므로 Analytics Credential 없이 전체 제품 흐름을 확인할 수 있습니다.

전체 검증 실행:

```bash
corepack pnpm verify
```

## 확장 가능한 구조

Metric Atlas는 React, Vite, GA4와 GTM에서 시작하지만 각 영역의 경계를 명확하게 유지합니다. 다음 영역에 기여할 수 있습니다.

- 새로운 SDK 호출 패턴을 위한 Detector Adapter
- 공유 Connector Contract를 구현하는 Analytics Connector
- 실제 지원·미지원 패턴을 재현하는 Fixture
- Dashboard, Overlay, 검색 및 접근성 개선
- 문서, 예제와 번역
- Contract, 통합, E2E, 보안과 성능 테스트

## 기여하기

Issue, Discussion, 버그 재현, 문서 개선, Detector Fixture, Connector 구현과 Pull Request를 환영합니다.

공유 계약을 변경하기 전 [Project Source of Truth](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/docs/00-project-source-of-truth.md)를 읽고 [기여 안내](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/CONTRIBUTING.md)의 ADR Workflow를 따라 주세요.

<div align="center">

### 제품이 무엇을 보내는지 연결하고, Analytics가 무엇을 받는지 검증하세요.

[저장소 살펴보기](https://github.com/Metric-Atlas/Metric-Atlas) · [문서 읽기](https://github.com/Metric-Atlas/Metric-Atlas/tree/main/docs) · [기여하기](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/CONTRIBUTING.md)

</div>
