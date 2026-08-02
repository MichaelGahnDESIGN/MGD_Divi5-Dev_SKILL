# WordPress- und Divi-5-Wiki Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Eine ausführliche GitHub-Wiki für WordPress 7, sichere Plugin-Entwicklung, Divi 5 und KI-Agenten erstellen.

**Architecture:** Die Wiki trennt Themen in eigenständige Seiten. Jede Seite beginnt mit einer verständlichen Einführung, enthält dann technische Referenzabschnitte und endet mit einer klaren Prüfliste. Die GitHub-Wiki bleibt die veröffentlichte Quelle; die Skill-Datei verlinkt auf die wichtigsten Arbeitsabläufe.

**Tech Stack:** GitHub Wiki Markdown, WordPress 7, Divi 5, PHP, WordPress Coding Standards.

---

### Task 1: Wiki-Navigation und Quellenbasis

**Files:**
- Modify: Wiki `Home.md`
- Create: Wiki `Quellen-und-Pflege.md`

- [ ] **Step 1: Navigation vollständig machen**

Home verlinkt diese Themen:

```text
WordPress 7 Grundlagen und Betrieb
WordPress Plugin Entwicklung sicher
Divi 5 Visual Builder und Designsystem
Divi 5 Module und Erweiterungen
Divi 5 Presets und Designvarianten
Divi AI sicher einsetzen
KI-Agenten Playbook für WordPress und Divi
Quellen und Pflege
```

- [ ] **Step 2: Quellen- und Pflegepage schreiben**

Die Seite enthält offizielle WordPress-, WordPress-Developer- und Elegant-Themes-Links, Versionsprüfregeln, Änderungsdatum und die Vorgabe, unbestätigte Aussagen sichtbar als Annahme zu kennzeichnen.

- [ ] **Step 3: Prüfung**

```bash
git diff --check
```

Erwartung: keine Leerzeichen- oder Markdown-Fehler.

### Task 2: WordPress-7-Grundlagen und Betrieb

**Files:**
- Create: Wiki `WordPress-7-Grundlagen-und-Betrieb.md`

- [ ] **Step 1: Nutzerabschnitt schreiben**

Erkläre verständlich Inhalte, Medien, Rollen, Updates, Backups, Wartungsmodus sowie wann Hilfe nötig ist.

- [ ] **Step 2: Entwickler- und KI-Agentenabschnitt schreiben**

Beschreibe Datenmodell, REST API, Cron, Caching, WP-CLI, sichere Betriebsreihenfolge und Abnahmeliste.

- [ ] **Step 3: Prüfung**

```bash
rg -n 'Passwort|Secret|API-Key' WordPress-7-Grundlagen-und-Betrieb.md
```

Erwartung: keine realen Zugangsdaten; nur erklärende Sicherheitsregeln.

### Task 3: Sichere WordPress-Plugin-Entwicklung

**Files:**
- Create: Wiki `WordPress-Plugin-Entwicklung-sicher.md`

- [ ] **Step 1: Architektur und Sicherheitsmodell schreiben**

Erkläre Dateistruktur, Hooks, Optionen, Capability-Checks, Nonces, Sanitization, Validierung, Escaping, Datenschutz und Tests.

- [ ] **Step 2: Settings-API-Beispiel schreiben**

Das Beispiel verwendet `register_setting`, eine Sanitization-Callback-Funktion, `current_user_can`, `wp_nonce_field` und korrektes Escaping in einem Admin-Formular.

- [ ] **Step 3: REST/AJAX-Beispiel schreiben**

Das Beispiel zeigt einen klar begrenzten Endpunkt mit Permission Callback, Eingabevalidierung und datensparsamem Fehlertext.

- [ ] **Step 4: Prüfung**

```bash
rg -n 'check_admin_referer|current_user_can|sanitize_|esc_' WordPress-Plugin-Entwicklung-sicher.md
```

Erwartung: beide Beispiele belegen die Sicherheitsbausteine nachvollziehbar.

### Task 4: Divi-5-Visual-Builder und Designsystem

**Files:**
- Create: Wiki `Divi-5-Visual-Builder-und-Designsystem.md`

- [ ] **Step 1: Nutzerabschnitt schreiben**

Erkläre Sektionen, Zeilen, Spalten, Gruppen, Module, Theme Builder, Presets, Variablen sowie die Wahl zwischen nativen Einstellungen und Custom Code.

- [ ] **Step 2: Visual-Builder-Workflow schreiben**

Beschreibe Drahtgitteransicht, Kommandozentrale, Elementbeschriftungen, geschützte globale Layouts, lokale Medien, Responsive-Prüfung und Speichern.

- [ ] **Step 3: Designsystem-Checkliste ergänzen**

Beschreibe Global Colors, Schriften, Abstände, Radius, Schatten und barrierefreie Kontraste als wiederverwendbares System.

### Task 5: Divi-5-Module, Presets, Divi AI und KI-Agenten

**Files:**
- Create: Wiki `Divi-5-Module-und-Erweiterungen.md`
- Create: Wiki `Divi-5-Presets-und-Designvarianten.md`
- Create: Wiki `Divi-AI-sicher-einsetzen.md`
- Create: Wiki `KI-Agenten-Playbook-für-WordPress-und-Divi.md`

- [ ] **Step 1: Module und Erweiterungen schreiben**

Erkläre native Module, Bild- und Icon-Entscheidungen, Custom Modules, Plugin-Grenzen, Builder-Kompatibilität und Tests.

- [ ] **Step 2: Divi-5-Presets-Seite schreiben**

Erkläre Default-, Element- und Option-Group-Presets als wiederverwendbare Bausteine eines Designsystems. Dokumentiere gestapelte und verschachtelte Presets mit klarer Prioritätsregel: Bei derselben Eigenschaft gewinnt die zuletzt aufgetragene Preset-Ebene. Zeige eine kleine, wartbare Startbibliothek und einen sicheren Änderungs- sowie Prüfprozess.

- [ ] **Step 3: Divi-AI-Seite schreiben**

Beschreibe die offiziell dokumentierten Einsatzfelder für Layouts, Texte, Bilder und Code. Trenne Ideenfindung und Veröffentlichung. Dokumentiere, dass keine sensiblen Kunden-, Zugangs- oder personenbezogenen Daten ohne geklärte Freigabe in Prompts oder Bildreferenzen gehören. Ergänze einen Qualitätscheck für Inhalt, Rechte, Barrierefreiheit, Responsive Design und SEO.

- [ ] **Step 4: Agenten-Playbook schreiben**

Definiere eine sichere Reihenfolge: Auftrag verstehen, Schutzbereiche feststellen, Backup prüfen, Struktur lesen, native Umsetzung, Medien/Alt-Texte, Responsive-/SEO-Prüfung, Speichern und dokumentieren.

- [ ] **Step 5: Verbote und Freigabepunkte schreiben**

Klar nennen: keine Secrets ausgeben, keine globalen Layouts ohne Auftrag ändern, keine externen Fonts/Assets ohne Freigabe, keine ungesicherten Leistungsbehauptungen und keine produktiven Änderungen ohne Rückfallweg.

### Task 6: Abnahme und Veröffentlichung

**Files:**
- Modify: `README.md`
- Modify: `CHANGELOG.md`
- Modify: Wiki `Home.md`

- [ ] **Step 1: README verlinken**

README verlinkt die Wiki deutlich und erklärt die beiden Leseebenen „Nutzer“ und „Entwickler/KI-Agenten“.

- [ ] **Step 2: Qualitätsprüfung**

```bash
git diff --check
rg -n -i 'TODO|TBD|Passwort=.*|API[_ -]?KEY=.*' .
```

Erwartung: keine Platzhalter, keine echten Zugangsdaten.

- [ ] **Step 3: Commit und Push**

```bash
git add .
git commit -m "docs: WordPress- und Divi-5-Wiki ausbauen"
git push origin main
```

Im separaten Wiki-Repository auf dessen Standardbranch committen und pushen.
