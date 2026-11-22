# delphianers-claude-plugins

Persönlicher [Claude-Code-Plugin-Marketplace](https://code.claude.com/docs/en/plugin-marketplaces)
mit geprüften Skills und Plugins für eigene Projekte.

Vorschläge gern per Issue. **Externe Pull Requests werden nicht übernommen**
(siehe [SECURITY.md](SECURITY.md)).

## Inhalt

| Plugin | Skill | Zweck |
|---|---|---|
| `multiplattform-release` | `release-prozess` | Branch-Modell (`main`, `dev/m<N>`, `release/x.y.z`, `hotfix/x.y.z`), Release-Candidates, lokale Testnachweise je Betriebssystem, sparsame und gehärtete CI |

## Installation (lokal, einmal je Rechner)

In einer Claude-Code-Session:

```text
/plugin marketplace add delphianer/delphianers-claude-plugins#v1.0.0
/plugin install multiplattform-release@delphianers-claude-plugins
```

Der Zusatz `#v1.0.0` legt den Marketplace auf einen geprüften Stand fest.
Aktualisieren erst nach Lesen des Diffs zum neuen Tag.

Aufruf: `/multiplattform-release:release-prozess` (optional mit `planen`,
`rc 0.6.0`, `test v0.6.0-rc.1`, `release 0.6.0`, `hotfix 0.6.1`, `ci`).
Claude lädt den Skill auch selbst, wenn es um Branches, RCs oder Releases geht.

## Cloud-Sessions (claude.ai/code)

Plugins werden dort nicht geladen. Den Skill-Ordner ins Projekt kopieren:
`plugins/multiplattform-release/skills/release-prozess` → `.claude/skills/release-prozess`.
Details: [PROJEKT-EINRICHTUNG.md](plugins/multiplattform-release/skills/release-prozess/PROJEKT-EINRICHTUNG.md).

## Pflege

- Änderungen nur per PR auf `main`; danach Tag `vX.Y.Z` und Version in
  `plugin.json` + Skill-Versionszeile + [CHANGELOG.md](CHANGELOG.md) anheben.
- Prüfen: `claude plugin validate .`
- Kopien in Projekten danach ersetzen, nie dort direkt ändern.

## Repo-Einstellungen (Checkliste, auch für weitere öffentliche Repos)

- [ ] 2FA mit Passkey oder Authenticator-App (kein SMS)
- [ ] Settings → General → Features: Wiki, Discussions, Projects aus; Issues an
- [ ] Pull Requests auf Mitwirkende beschränken, falls die Einstellung angeboten wird
- [ ] Ruleset `main`: nur per PR, kein Force-Push, kein Löschen (keine Pflicht-Freigabe – allein nicht erfüllbar)
- [ ] Tag-Ruleset `v*`: Anlegen/Löschen nur durch Inhaber
- [ ] Settings → Actions: deaktiviert, solange keine Workflows nötig sind
- [ ] Private Vulnerability Reporting aktivieren (Settings → Security)
- [ ] Bei Spam: Interaction limits ([Doku](https://docs.github.com/en/communities/moderating-comments-and-conversations/limiting-interactions-in-your-repository))

## Lizenz

[MIT](LICENSE)
