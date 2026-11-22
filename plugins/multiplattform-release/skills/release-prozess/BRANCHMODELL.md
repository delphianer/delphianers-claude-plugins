# Branch-Modell im Detail

Angelehnt an Git-Flow ([Original von Vincent Driessen](https://nvie.com/posts/a-successful-git-branching-model/)),
vereinfacht: kein dauerhafter `develop`-Branch, sondern ein Integrationsbranch je
Meilenstein.

```text
main ────●──────────────────────────────●── v0.6.0 ──●── v0.6.1
          \                            / \           /
dev/m6     ●──●──●──●──────●──●───────/   \  hotfix/0.6.1
              \     \      ↑   \     /     \
dev/m6-xyz     ●──●──●     │    \   /       └─→ zurück nach dev/m6
                           │  release/0.6.0 ●──rc.1──●──rc.2──●(Nachweise)
                     Korrektur aus Test rc.1
```

## Befehle

Meilenstein beginnen:

```bash
git fetch origin main
git switch -c dev/m6 origin/main
git push -u origin dev/m6
git switch -c dev/m6-protokoll
```

RC schneiden (erster Kandidat):

```bash
git fetch origin dev/m6
git switch -c release/0.6.0 origin/dev/m6
# Version und Changelog anpassen, committen
git tag -a v0.6.0-rc.1 -m "Release-Candidate 0.6.0-rc.1"
git push -u origin release/0.6.0 v0.6.0-rc.1
```

Korrektur nach fehlgeschlagenem Test:

```bash
# Fix auf dev/m6 (über Arbeitsbranch + PR), dann:
git switch release/0.6.0
git merge --no-ff origin/dev/m6
git tag -a v0.6.0-rc.2 -m "Release-Candidate 0.6.0-rc.2"
git push origin release/0.6.0 v0.6.0-rc.2
```

Prüfen, dass seit dem RC-Tag nur Nachweise dazukamen:

```bash
git diff --name-only v0.6.0-rc.2 HEAD   # darf nur docs/evidence/** zeigen
```

Nach dem Merge der Release-PR (durch den Inhaber):

```bash
git fetch origin main
git tag -a v0.6.0 -m "Release 0.6.0" origin/main
git push origin v0.6.0
git switch dev/m6 && git merge --no-ff origin/main && git push
```

## Versionsnummern

[Semantic Versioning](https://semver.org/lang/de/): `MAJOR.MINOR.PATCH`,
Release-Candidates als `-rc.N`. Plattformen mit Build-Nummer (Android
`versionCode`, iOS `CFBundleVersion`, Flutter `+N`) zählen streng aufsteigend
über alle RCs, damit Testinstallationen sich überschreiben lassen.

## Cloud-Sessions

Cloud-Sessions dürfen oft nur auf einen vorgegebenen `claude/…`-Branch pushen.
Dieser Branch ist dann der Arbeitsbranch; Übernahme nach `dev/m<N>` per PR oder
nach ausdrücklicher Freigabe. Release- und Hotfix-Branches sowie Tags legt in
diesem Fall der Inhaber oder eine lokale Session an.

## Schutz auf GitHub

- Ruleset für `main`: Änderungen nur per PR, kein Force-Push, kein Löschen;
  erforderliche Statuschecks = Linux-Jobs.
- Ruleset für `release/*`: kein Force-Push, kein Löschen.
- Tag-Ruleset für `v*`: nur Inhaber darf anlegen/löschen.

Doku: [Rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets).
