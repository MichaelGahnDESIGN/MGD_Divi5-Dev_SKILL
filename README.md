# MGD Divi 5 Dev Skill

Ein umfangreicher Skill für Claude Code und ChatGPT Codex, der KI-Agenten dazu befähigt,
professionell mit WordPress und Divi 5 zu entwickeln und zu designen. Animationen,
Scroll-Effekte, Three.js, eigene Plugins, Child-Themes — alles nach MGD-Standard: sauber,
sicher, DSGVO-konform und kommerziell nutzbar.

Dieser Skill ist kein Schnellschuss. Er entstand aus echter Arbeit mit WordPress, Divi und
KI-Agenten im Agentur-Alltag von Michael Gahn DESIGN — und soll genau das widerspiegeln.

## Wissensstand und Pflege

Der Skill, die GitHub-Wiki und die ausführliche interne Wissensbasis werden gemeinsam gepflegt.
Die GitHub-Wiki ist der lesbare Einstieg; der Skill enthält verbindliche Arbeitsregeln; die
interne Wissensbasis vertieft einzelne Themen. Vor einer produktiven Änderung haben die aktuelle
Herstellerdokumentation und die konkret geprüfte Installation immer Vorrang.

Die Einstiegsbereiche der Wiki sind **nutzbar und gepflegt**, nicht bloß Platzhalter. Offene Punkte
werden ausschließlich auf der jeweiligen Seite als konkrete Prüffrage markiert. Den vollständigen
Abgleich beschreibt [der Wissensstand](docs/WISSENSSTAND.md).

## Für Wen Ist Dieser Skill Gedacht?

- Entwickler und Designer, die mit Claude Code oder ChatGPT Codex an WordPress/Divi-Projekten arbeiten
- Agenturen, die ihren Agenten klare Regeln und Qualitätsstandards für WordPress-Arbeit mitgeben wollen
- Menschen, die Divi-Child-Themes, eigene WordPress-Plugins und Animationen professionell umsetzen möchten
- Projekte, bei denen DSGVO-Konformität, lokale Assets und kommerzielle Nutzbarkeit Pflicht sind

## Was Dieser Skill Macht

| Befehl | Was passiert |
|--------|-------------|
| `/divi-install` | WordPress + Divi lokal installieren und konfigurieren |
| `/divi-install-docker` | Docker-Entwicklungsumgebung für WordPress + Divi aufsetzen |
| `/divi-childtheme` | Divi Child-Theme mit korrekter Struktur, lokalen Fonts und Enqueue erstellen |
| `/divi-backup` | Lokales Backup von Datenbank und Dateien erstellen |
| `/divi-dev` | Entwicklungs-Checkliste, Datei-Watcher, Workflow-Übersicht starten |
| `/divi-project-filesystem` | Projektordner mit MGD-AI-Basic-Projektordner anlegen |
| `/divi-plugin` | Neues WordPress-Plugin für Divi erstellen (sicher, strukturiert) |
| `/divi-animations` | Animations-Bibliotheken lokal einbinden und konfigurieren |
| `/divi-deploy` | Deployment auf Live-Server durchführen |
| `/divi-debug` | Systematisches Debugging von Divi-Problemen |
| `/divi-release` | Versions-Bump, CHANGELOG, Release-Workflow |
| `/divi-module` | Natives Divi 5 Custom Module erstellen (React/TSX + PHP Traits) |
| `/divi-optimize` | Performance optimieren — Core Web Vitals, Caching, Bilder |
| `/divi-theme-builder` | Header, Footer, Single Post, Archive, CPT-Templates im Theme Builder |
| `/divi-design-system` | Design Variables, Fluid Typography mit clamp(), Presets, Colorscheme |
| `/divi-ai` | Divi AI sinnvoll einsetzen — Workflow, Grenzen, DSGVO |
| `/divi-canvas` | Popups, Off-Canvas Menüs, Scroll-Trigger, Exit-Intent mit Divi Canvases |
| `/divi-builder` | Sichere direkte Arbeit im Divi-5-Visual-Builder: Kommandozentrale, Drahtgitter, Medien, Responsive- und SEO-Abnahme |

## Grundregeln — Was Dieser Skill Immer Tut

Diese Regeln sind nicht verhandelbar und gelten für jeden Output:

- **Umlaute korrekt** — ä, ö, ü, ß statt ae/oe/ue/ss
- **Deutsch** — alle Erklärungen, Kommentare und Texte auf Deutsch
- **Lokal** — Fonts, Libraries, Icons, Scripts immer lokal hosten (kein CDN ohne explizite Erlaubnis)
- **DSGVO-konform** — keine Google Fonts direkt, kein externes IP-Logging, kein Tracking ohne Consent
- **Kommerziell nutzbar** — nur MIT-lizenzierte oder anderweitig frei kommerziell nutzbare Libraries
- **Sicherheit** — Nonces, Capability-Checks, Sanitization und Escaping bei jedem Plugin
- **Neues Projekt → Projektordner** — Hinweis auf MGD-AI-Basic-Projektordner
- **Fragen bei Unklarheit** — sofort fragen, bevor Code produziert wird

## Erlaubte Libraries (Lizenz-Übersicht)

| Library | Lizenz | Version | Zweck |
|---------|--------|---------|-------|
| Three.js | MIT | r175 | 3D-Grafik |
| GSAP + ScrollTrigger | No-Charge (Webflow) | 3.12.5+ | Hochwertige Animationen |
| AOS | MIT | 2.3.4 | Scroll-Entrance-Animationen |
| Lenis | MIT | 1.3.23 | Smooth Scroll |
| Vanilla Tilt.js | MIT | 1.8.1 | 3D-Tilt-Effekte |
| Alpine.js | MIT | 3.15.12 | UI-Interaktivität |
| Swiper.js | MIT | 12.2.0 | Slider/Karussell |
| Bunny Fonts | Gratis | — | Externer Font-Dienst; nur nach Datenschutzprüfung und ausdrücklicher Freigabe, lokale Fonts bleiben Standard |

GSAP ist seit 30. April 2025 vollständig kostenlos, auch kommerziell — inkl. ScrollTrigger,
SplitText und allen ehemaligen Club-Plugins. Nutzbar für alle normalen Websites und
Client-Projekte ohne Einschränkungen.

## Schnellstart

```bash
# Claude Code
git clone https://github.com/MichaelGahnDESIGN/MGD_Divi5-Dev_SKILL.git ~/.claude/skills/MGD_Divi5-Dev_SKILL
```

```bash
# ChatGPT Codex
git clone https://github.com/MichaelGahnDESIGN/MGD_Divi5-Dev_SKILL.git ~/.codex/skills/MGD_Divi5-Dev_SKILL
```

Dann im Projekt-Kontext:

```text
/divi-builder
Bearbeite die Startseite ausschließlich mit nativen Divi-5-Modulen.
Header, eigenes Menü und Footer dürfen nicht verändert werden.
Nutze UpdraftPlus als Rückfallpunkt und prüfe Rank Math vor dem Speichern.
```

```text
/divi-childtheme
Erstelle mir ein Divi Child-Theme für ein lokales Projekt.
Theme-Name: "Mein Shop Child"
Primärfarbe: #ce1517
Schrift: Open Sans (lokal)
```

```text
/divi-plugin
Erstelle ein WordPress-Plugin das nach dem Absenden eines Kontaktformulars
eine E-Mail sendet und den Eintrag in einer Custom-Tabelle speichert.
```

```text
/divi-animations
Binde GSAP mit ScrollTrigger lokal ein und erstelle Scroll-Animationen
für alle Divi-Sektionen auf der Startseite.
```

## Repository-Struktur

```text
MGD-Divi5-Dev/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── .gitignore
├── .github/
│   └── ISSUE_TEMPLATE/
│       └── bug_report.md
├── .claude/
│   └── commands/             ← Claude Code Slash-Commands
│       ├── divi-install.md
│       ├── divi-install-docker.md
│       ├── divi-childtheme.md
│       ├── divi-backup.md
│       ├── divi-dev.md
│       ├── divi-project-filesystem.md
│       ├── divi-plugin.md
│       ├── divi-animations.md
│       ├── divi-deploy.md
│       ├── divi-debug.md
│       ├── divi-release.md
│       ├── divi-module.md
│       ├── divi-optimize.md
│       ├── divi-theme-builder.md
│       ├── divi-design-system.md
│       ├── divi-ai.md
│       └── divi-canvas.md
├── .codex/
│   └── commands/             ← ChatGPT Codex Commands (gleiche Dateien)
└── skill/
    └── DIVI5-SKILL.md        ← Vollständige Skill-Dokumentation
```

## Was Der Skill Enthält

### Sicherer Divi-5-Visual-Builder-Workflow

Der neue `/divi-builder`-Befehl schließt eine typische Lücke zwischen „Layout gestalten“ und „sicher auf einer echten Website arbeiten“:

1. Rückfallpunkt, Zielseite und Wartungsmodus prüfen.
2. Geschützte globale Vorlagen wie Header, eigenes Menü und Footer klar aus dem Arbeitsbereich ausschließen.
3. In der Drahtgitteransicht die bestehende Struktur verstehen, statt versehentlich in die falsche Sektion zu schreiben.
4. Die Kommandozentrale mit `⌘ K` beziehungsweise `Strg K` verwenden. Sie ergänzt Elemente abhängig von der aktuellen Auswahl – deshalb wird die Auswahl immer vor dem Einfügen geprüft.
5. Neue Elemente eindeutig beschriften, lokale Medien mit passenden Alternativtexten einfügen und alle Breakpoints prüfen.
6. Erst dann speichern und über Rank Math die SEO-Grundlagen kontrollieren.

Der Workflow ist besonders sinnvoll für Agentur-Websites, auf denen bereits globale Vorlagen, reale Referenzen und geschäftskritische Kontaktstrecken vorhanden sind.

### WordPress Plugin-Entwicklung
Vollständige Plugin-Struktur mit korrektem Header, Lifecycle-Hooks, Sicherheits-Template
(Nonces, Capability-Checks, Sanitization, Escaping), AJAX-Handler, REST-API-Endpunkte,
Datenbank-Interaktionen via `$wpdb`, Custom Post Types und Taxonomien, Settings API.

### Divi Child-Themes
Komplette Child-Theme-Struktur mit lokalem Font-Hosting (@font-face, kein Google Fonts CDN),
korrektem Enqueue via `functions.php`, SCSS-Vorbereitung, Divi-Builder-Kompatibilität.

### Animations-Stack
Vollständige lokale Integration von Three.js, GSAP + ScrollTrigger, AOS, Lenis,
Vanilla Tilt, Alpine.js und Swiper — alle mit Divi-spezifischen Quirks und Fixes:
- `window.load` statt `DOMContentLoaded` wegen Divi Lazy-Loading
- `wp-admin`-Check um Builder-Konflikte zu vermeiden
- `jQuery`-noConflict-Pattern
- `ScrollTrigger.refresh()` nach AJAX-Content
- Lenis + Divi Anchor-Scroll Konflikt-Fix
- Alpine.js + `wp_kses_post()` Workaround

### DSGVO / EU-Datenschutz
Vollständige Checkliste: Google Fonts deaktivieren, lokale Fonts, Consent-Management,
SSL, keine externen Tracker ohne Zustimmung.

### Docker-Entwicklungsumgebung
`docker-compose.yml` für lokale WordPress + Divi Entwicklung mit PHP 8.3,
`.env`-Template, WordPress-Debug-Einstellungen.

### Deployment-Workflow
Schrittweises Deployment mit Backup, `wp search-replace`, Cache-Clearing und Tests.

## Lizenz

MIT — frei verwendbar, anpassbar, weitergeben mit Namensnennung.

## 🔒 Lokal-only — Playtests, Backups & sensible Daten

Diese Daten dürfen **niemals** die lokale Maschine verlassen — weder nach GitHub noch nach Live/Deploy:

- **Backups:** DB-Dumps, `*.sql`, `*.sql.gz`, `backups/` bleiben lokal — nie nach GitHub, nie in den Webroot/Live.
- **Sensible Daten:** `.env*` (außer `.env.example`), Tokens, API-Keys, Passwörter, `wp-config.php` — niemals committen/pushen.
- **Push-Disziplin:** Nur den Hauptbranch (`main`) pushen, **niemals** `git push --all`/`--mirror`.

---

## Verwandte MGD Projekte

| Projekt | Beschreibung |
|---------|-------------|
| [gvieaway_WordPress_Plugin](https://github.com/MichaelGahnDESIGN/MGD_Giveaway_WP-Plugin) | Gewinnspiel-Plugin für WordPress |
| [MGD-AI-Project-Updater-Skill](https://github.com/MichaelGahnDESIGN/MGD_AI-Project-Updater_SKILL) | Sichere Update-Workflows für WordPress |
| [MGD-ToDo-SKILL](https://github.com/MichaelGahnDESIGN/MGD_Todo_SKILL) | Aufgabenverwaltung direkt im Projekt-Repo |
| [MGD-AI-Basic-Projektordner](https://github.com/MichaelGahnDESIGN/MGD_AI-Basic-Projektordner_TOOL) | Projektvorlage für KI-Agenten |
| [MGD-DEV-Skill](https://github.com/MichaelGahnDESIGN/MGD_DEV_SKILL) | Release, Sync, Backup und Wissensdokumentation |

→ Alle öffentlichen Projekte: [github.com/MichaelGahnDESIGN](https://github.com/MichaelGahnDESIGN)

---

## Impressum

Angaben gemäß § 5 DDG — Siehe [`IMPRESSUM.md`](IMPRESSUM.md).
