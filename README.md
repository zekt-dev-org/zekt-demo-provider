# zekt-demo-provider

**Ship It Demo — Provider Repository**

Part of the [Zekt](https://zekt.io) "Ship It 🚀" live deploy demo (Spec 030).

## Purpose

This repository acts as the **Provider** in the Zekt demo pipeline. When a visitor clicks "Ship It" on the Zekt demo page, this workflow:

1. **Receives** build configuration (template, name, message, color theme) via `workflow_dispatch`
2. **Validates** and sanitizes all inputs
3. **Generates** a self-contained HTML page from the selected template
4. **Dispatches** the generated page to the Consumer repository via `zekt-action`

The Consumer repository then deploys the page to GitHub Pages, producing a live URL the visitor can share.

## Architecture

```
Visitor → Zekt Backend → [THIS REPO] → zekt-action → Zekt Mesh → zekt-demo-consumer → GitHub Pages
```

## Workflow

- **File:** `.github/workflows/zekt-ship-it-provider.yml`
- **Trigger:** `workflow_dispatch` from Zekt backend
- **Inputs:** `zektDemoTemplate`, `zektDemoUserName`, `zektDemoMessage`, `zektDemoTheme`, `zektCorrelationId`

## Templates

Three page templates are generated:

| Template | Description |
|----------|-------------|
| `landing-page` | Hero section with name, message, gradient background |
| `status-badge` | Service status card with uptime bar |
| `team-card` | Profile card with avatar initial and themed border |

## Setup

### Repository Variable

Set `ZEKT_DEMO_API` under **Settings → Secrets and variables → Actions → Variables**:

| Name | Value |
|------|-------|
| `ZEKT_DEMO_API` | `https://<your-zekt-backend-url>` |

### Requirements

- Repository must be **public** (free GitHub Actions)
- `zekt-action` must be accessible (public action at `zekt-dev-org/zekt-action@v1`)

## Related

- **Consumer repo:** [zekt-dev-org/zekt-demo-consumer](https://github.com/zekt-dev-org/zekt-demo-consumer)
- **Main platform:** [zekt-dev-org/zektMainWeb](https://github.com/zekt-dev-org/zektMainWeb)
- **Spec plan:** `specs/030-chess-ai-demo/` in `zektMainWeb`
