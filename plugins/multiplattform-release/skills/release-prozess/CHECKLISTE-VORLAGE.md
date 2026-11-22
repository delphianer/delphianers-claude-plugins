# Checkliste lokale Testsession (Vorlage)

In `docs/RELEASE-PROZESS.md` des Projekts übernehmen und um projektspezifische
Punkte ergänzen. Jeden Punkt einzeln ausführen und bestätigen lassen; nicht
Geprüftes bleibt „nicht geprüft“.

## A. Vorbereitung
- [ ] Richtiger Tag ausgecheckt, SHA notiert, Arbeitsverzeichnis sauber
- [ ] Betriebssystem mit allen verfügbaren Updates (Hauptversion notieren)
- [ ] Gepinnte SDK-/Werkzeugversion aktiv (z. B. `flutter --version`)
- [ ] Abhängigkeiten aus Lockfile, keine Änderung an Lockfile

## B. Automatisch (Prüfskript des Projekts)
- [ ] Formatierung
- [ ] Statische Analyse
- [ ] Unit-/Widget-/Integrationstests
- [ ] Release-Build für dieses Betriebssystem

## C. Start und Grundfunktion (manuell)
- [ ] App startet aus dem Release-Build ohne Fehlermeldung
- [ ] Hauptablauf einmal vollständig (projektspezifisch beschreiben)
- [ ] Sprache DE und EN umschaltbar, Texte vollständig
- [ ] Fenstergröße klein/groß bzw. Hoch-/Querformat
- [ ] Daten bleiben nach Neustart erhalten (sofern vorgesehen)
- [ ] Keine Geheimnisse im Log/Konsolenausgabe

## D. Plattformfunktionen (nur zutreffende)
- [ ] Berechtigungsdialoge (Mikrofon, Netzwerk, Dateien) mit Projekttexten
- [ ] Berechtigung verweigert → verständliche Meldung, kein Absturz
- [ ] Netzwerk weg/zurück → App erholt sich
- [ ] App in Hintergrund/Vordergrund → Zustand korrekt
- [ ] Firewall-/Netzwerkfreigabe (z. B. Windows-Dialog beim ersten Port)

## E. Mobil (nur Release-Stufe, laut Projekt)
- [ ] Installation auf echtem Gerät (iPhone über Mac/Xcode, Android per APK)
- [ ] Punkte C und D auf dem Gerät

## F. Abschluss
- [ ] Nachweis ausgefüllt, Ergebnis „bestanden“ / „nicht bestanden“ / „teilweise“
- [ ] Fehler als Issue mit Reproduktionsschritten (ohne Geheimnisse)
