<div align="center">

<img src="./assets/metric_atlas_logo.png" width="210" alt="Metric Atlas logo" />

# Metric Atlas

### Make analytics implementation visible, verifiable, and trustworthy.

**English** · [한국어](https://github.com/Metric-Atlas/.github/blob/main/profile/README.ko.md)

Metric Atlas is a source-first analytics observability toolkit for React and Vite applications. It discovers tracking events in existing frontend code, connects them to real interface elements, and compares the implementation with GA4 data and configuration.

[Repository](https://github.com/Metric-Atlas/Metric-Atlas) · [Documentation](https://github.com/Metric-Atlas/Metric-Atlas/tree/main/docs) · [Contributing](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/CONTRIBUTING.md)

![TypeScript](https://img.shields.io/badge/TypeScript-Node.js-3178C6?style=flat-square&logo=typescript&logoColor=white)
![React and Vite](https://img.shields.io/badge/React%20%2B%20Vite-first-646CFF?style=flat-square&logo=vite&logoColor=white)
![GA4](https://img.shields.io/badge/GA4-analytics%20health-E37400?style=flat-square&logo=googleanalytics&logoColor=white)
![Self-hosted](https://img.shields.io/badge/deployment-self--hosted-0F766E?style=flat-square)
![No database](https://img.shields.io/badge/database-none-334155?style=flat-square)
![Contributions welcome](https://img.shields.io/badge/contributions-welcome-14B8A6?style=flat-square)

</div>

---

## Analytics instrumentation should not be a guessing game

Tracking knowledge is often scattered across source code, spreadsheets, dashboards, and the people who remember how everything was wired. As applications evolve, those sources drift apart.

Metric Atlas starts with the implementation that already exists and turns it into a living analytics map.

```text
Existing frontend code
        ↓
Discover event calls and bind them to UI elements
        ↓
Generate a structured event manifest
        ↓
Compare code with GA4 observation and configuration
        ↓
Surface analytics health in the product and in pull requests
```

<table>
  <tr>
    <td width="33%" valign="top"><h3>Discover</h3>Find event calls, parameters, emitters, providers, source locations, and UI bindings directly from frontend code.</td>
    <td width="33%" valign="top"><h3>Verify</h3>Compare code with GA4 observations, managed events, quality signals, and Custom Dimension registration.</td>
    <td width="33%" valign="top"><h3>Deliver</h3>Bring analytics context into a live overlay, a health dashboard, search, and pull-request reports.</td>
  </tr>
</table>

## What Metric Atlas connects

Metric Atlas is not another analytics dashboard. Its value comes from connecting evidence that normally lives in different tools:

| Evidence | What Metric Atlas adds |
|---|---|
| Frontend implementation | Original event name, parameters, emitter, provider, and source location |
| Product interface | The native UI element associated with a detected event |
| Analytics platform | GA4 observation, reporting timezone, managed-event state, and data-quality flags |
| Analytics configuration | Built-in and registered Custom Dimension status for event parameters |
| Code review | Semantic event changes between base and head Git revisions |

## Core capabilities

### Event detection and live overlay

Metric Atlas detects supported direct analytics calls during the build, generates an event manifest, and binds events to native JSX elements. Turn on the overlay and hover a tracked element to inspect its event name, emitter, provider, parameters, binding confidence, and source location.

Source files remain untouched. `data-atlas-id` metadata is injected only into build output.

### Code ↔ GA4 Analytics Health

The dashboard begins with implementation health—not a raw event-count table. It helps teams review:

- events detected in code and observed in GA4;
- code events with no recent GA4 rows, without automatically calling them broken;
- GA4 events with no matching detected implementation;
- GA4-managed and Enhanced Measurement events;
- event parameters that are not registered as Custom Dimensions; and
- thresholding, data-loss, and recent-data quality signals.

Result status and data-quality flags stay separate so uncertainty remains visible.

### Analytics changes in pull requests

The CLI can scan base and head Git trees without modifying a checkout. A PR report can surface added and removed events, provider or emitter changes, parameter changes, unresolved bindings, dynamic names, and unsupported patterns where developers already review code.

### Search and optional natural-language query

Events remain searchable by their original names, providers, source locations, and health status. Optional natural-language querying builds on the same validated event catalog; it does not invent or permanently rename events.

## See the system

<p align="center">
  <img src="./assets/overview.png" width="100%" alt="Metric Atlas analytics health overview" />
</p>

<table>
  <tr>
    <td width="50%"><img src="./assets/events.png" alt="Metric Atlas event explorer" /></td>
    <td width="50%"><img src="./assets/query.png" alt="Metric Atlas query view" /></td>
  </tr>
</table>

## Why it is different

| Typical question | Metric Atlas approach |
|---|---|
| “Is the tracking document still current?” | Rebuild the manifest from the current implementation |
| “Which button sends this event?” | Connect the event call, source location, and rendered UI element |
| “The event exists in code—does GA4 see it?” | Compare code state with normalized GA4 observation |
| “Can we use this custom parameter in reports?” | Check built-in metadata and Custom Dimension registration |
| “What analytics changed in this PR?” | Produce a semantic base/head event diff |

Metric Atlas complements tracking plans and BI tools; it does not replace them. Its job is to make the implementation-to-measurement boundary observable.

## Built around explicit boundaries

- GA4 and GTM remain distinct. A `dataLayer.push(...)` call is a GTM emitter, not automatically a GA4 event.
- Unsupported wrappers, dynamic names, custom-component overlays, and unresolved bindings become visible warnings instead of silent omissions.
- Original event names are preserved rather than translated or redefined.
- Browser code never receives GA4 or LLM credentials. Secrets are resolved by the local Node runtime.
- Provider-specific responses are normalized behind shared contracts.
- No database is required; manifests are rebuilt and analytics responses use in-memory caching.

## Architecture at a glance

| Layer | Responsibility |
|---|---|
| Detector and Vite plugin | AST analysis, same-file JSX binding, manifest generation, and build-output instrumentation |
| Overlay | Live event metadata inside the running product |
| GA4 connector and health engine | Observation, managed-event classification, registration gaps, comparisons, and quality signals |
| Node runtime | Static assets, manifests, analytics APIs, credentials, guards, and in-memory caching |
| Dashboard and query tools | Health exploration, event search, detail views, and optional natural-language workflows |
| CLI and GitHub Actions | Repository scans, semantic manifest diffs, artifacts, and PR reports |

Shared Zod schemas keep producers and consumers aligned while detector and connector adapters remain independently extensible.

## Try it locally

Requirements: Node.js 22.18 or later. The demo does not require GA4 credentials.

```bash
git clone https://github.com/Metric-Atlas/Metric-Atlas.git
cd Metric-Atlas
corepack pnpm install --frozen-lockfile
corepack pnpm demo
```

Open [http://127.0.0.1:5180](http://127.0.0.1:5180).

The demo runs detection, manifest generation, DOM binding, and the overlay against real local source code. GA4 health and query views use safe fixtures, making the end-to-end product flow easy to evaluate without analytics credentials.

Run the complete verification suite:

```bash
corepack pnpm verify
```

## Built to be extended

Metric Atlas begins with React, Vite, GA4, and GTM while keeping domain boundaries explicit. Contributors can extend the project through:

- detector adapters for additional SDK call patterns;
- analytics connectors that implement the shared connector contract;
- fixtures for real-world supported and unsupported patterns;
- dashboard, overlay, search, and accessibility improvements;
- documentation, examples, and translations; and
- contract, integration, end-to-end, security, and performance tests.

## Contributing

Thoughtful issues, discussions, bug reproductions, documentation improvements, detector fixtures, connector work, and pull requests are welcome.

Before changing shared contracts, read the [project source of truth](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/docs/00-project-source-of-truth.md) and follow the ADR workflow described in the [Contributing Guide](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/CONTRIBUTING.md).

<div align="center">

### Map what the product sends. Verify what analytics receives.

[Explore the repository](https://github.com/Metric-Atlas/Metric-Atlas) · [Read the docs](https://github.com/Metric-Atlas/Metric-Atlas/tree/main/docs) · [Contribute](https://github.com/Metric-Atlas/Metric-Atlas/blob/main/CONTRIBUTING.md)

</div>
