# CI-Regeln: sparsam und gehärtet

GitHub-Actions-Minuten kosten je Runner unterschiedlich viel (Linux 1×,
Windows 2×, macOS 10× bei privaten Repos;
[Abrechnung](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions/about-billing-for-github-actions)).
Die lokale Testsession ist der Hauptnachweis, CI das Sicherheitsnetz.

## Wann welcher Runner

| Auslöser | Linux (Format, Analyse, Tests, Linux-/Android-Build) | Windows-Build | macOS-/iOS-Build |
|---|---|---|---|
| PR auf `dev/*` oder Arbeitsbranch | ja | nein | nein |
| PR `release/*` oder `hotfix/*` → `main` | ja | ja (Kür) | nein, lokal |
| Push auf `main` | ja | nein | nein |
| manuell (`workflow_dispatch`) | ja | ja | nur wenn ausdrücklich gewünscht |

Beispiel für einen Windows-Job nur bei Release-PRs:

```yaml
on:
  pull_request:
    branches: [main]
  workflow_dispatch:

jobs:
  windows:
    if: >-
      github.event_name == 'workflow_dispatch' ||
      startsWith(github.head_ref, 'release/') ||
      startsWith(github.head_ref, 'hotfix/')
    runs-on: windows-2022
```

## Härtung (Pflicht)

Doku: [Security hardening for GitHub Actions](https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions).

- Auslöser `pull_request`, **nie** `pull_request_target` für Code aus PRs.
- `permissions: contents: read` auf Workflow-Ebene; mehr nur je Job und begründet.
- Keine Secrets in PR-Workflows. Signierschlüssel nur in manuellen Release-Workflows
  mit Environment-Schutz.
- Fremde Actions auf vollständigen Commit-SHA pinnen, Version als Kommentar:
  `uses: actions/checkout@<sha> # v4.x.y`.
- Repo-Einstellung: Workflows aus Fork-PRs nur nach Freigabe ausführen.
- Keine Tokens oder Rechner-Details in Logs/Artefakten; Testberichte nur mit
  synthetischen Daten.
- SDK- und Werkzeugversionen fest pinnen (wie lokal), damit CI und Testsession
  dasselbe bauen.
