# Skill in einem Projekt einrichten

## 1. Projektdatei `docs/RELEASE-PROZESS.md`

Mindestinhalt:

```markdown
# Release-Prozess

Grundlage: Skill `multiplattform-release:release-prozess` Version 1.0.0
(https://github.com/delphianer/delphianers-claude-plugins).

## Zielsysteme
| System | Rolle | Gerät vorhanden | Ausnahme |
|---|---|---|---|
| Windows | Desktop | ja (Windows 10) | ohne Herstellersupport, To-do: Windows 11 |
| macOS | Desktop + iOS-Build | ja | – |
| Linux | Desktop | ja (Ubuntu) | – |
| iOS | Mobil | iPhone über Mac | Personal Team, 7 Tage |
| Android | Mobil | … | … |

## Prüfskripte
- Linux/macOS: `sh scripts/check.sh`
- Windows: `powershell -File scripts/check.ps1`
- Release-Build je System: …

## Projektspezifische Checklistenpunkte
- C2 Hauptablauf: …

## CI
- Linux-Jobs bei jeder PR: …
- Windows-Kür: `…yml`
```

## 2. Kopie des Skills für Cloud-Sessions

Plugins werden in Claude-Code-Cloud-Sessions nicht geladen, Projekt-Skills unter
`.claude/skills/` schon ([Doku](https://code.claude.com/docs/en/skills)). Deshalb:

```bash
mkdir -p .claude/skills
cp -r <plugins-repo>/plugins/multiplattform-release/skills/release-prozess .claude/skills/
```

Die Kopie trägt die Skill-Version in `SKILL.md`. Änderungen immer zuerst im
Plugin-Repo machen, dann die Kopie ersetzen – nie die Kopie direkt bearbeiten.

## 3. Verweis in den Projektregeln

In `AGENTS.md` bzw. `CLAUDE.md`:

```markdown
Release, RCs, Testnachweise und CI folgen `docs/RELEASE-PROZESS.md`
(Skill `release-prozess`).
```

## 4. GitHub-Einstellungen

Rulesets laut [BRANCHMODELL.md](BRANCHMODELL.md), Workflows laut
[CI-REGELN.md](CI-REGELN.md).
