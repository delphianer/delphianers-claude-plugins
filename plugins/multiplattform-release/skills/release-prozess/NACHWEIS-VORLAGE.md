# Nachweis-Vorlage

Ablage im Projekt: `docs/evidence/<version>-rc.<N>-<plattform>.md`,
z. B. `docs/evidence/0.6.0-rc.1-windows.md`.

Nicht eintragen: Tokens, Passwörter, Rechner-/Benutzernamen, IP-Adressen,
Seriennummern, Build-/Patchnummern des Betriebssystems.

```markdown
# Nachweis 0.6.0-rc.1 – Windows

| Feld | Wert |
|---|---|
| Tag | v0.6.0-rc.1 |
| Commit (SHA) | <vollständiger SHA aus `git rev-parse HEAD`> |
| Datum | JJJJ-MM-TT |
| Betriebssystem | Windows 10 (Hauptversion) |
| Gerätetyp | Desktop / Laptop / iPhone / Android-Telefon |
| SDK | Flutter x.y.z (gepinnt) |
| Teststufe | Release |
| Ergebnis | bestanden / nicht bestanden / teilweise |

## Automatisch
| Prüfung | Ergebnis |
|---|---|
| Prüfskript | ✓ / ✗ (Anzahl Tests) |
| Release-Build | ✓ / ✗ |

## Manuell
| Punkt | Ergebnis | Bemerkung |
|---|---|---|
| C1 App startet | ✓ | |
| … | nicht geprüft | Grund |

## Abweichungen und Issues
- keine / #123 …

## Bekannte Ausnahmen
- z. B. Windows 10 ohne Herstellersupport (siehe RELEASE-PROZESS.md)
```
