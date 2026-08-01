# Changelog

Alle nennenswerten Änderungen an diesem Projekt werden hier dokumentiert.

## [1.4.0] — 2026-08-02

### Hinzugefügt

- `/divi-builder` für sichere direkte Arbeit im Divi-5-Visual-Builder.
- Verbindlicher Ablauf für UpdraftPlus-Rückfallpunkte, geschützte globale Vorlagen, Drahtgitteransicht, Kommandozentrale und responsive Abnahme.
- Leitlinien für lokale Medien, konkrete Alternativtexte, native Divi-Icons und einen zurückhaltenden Glass-Eindruck ohne eigenes CSS.
- Wiki-Seiten zu Kommandozentrale, Visual-Builder-Workflow, Medien/Barrierefreiheit sowie Rank Math.

### Korrigiert

- Der Skill unterscheidet jetzt klar zwischen einer belegten Projektreferenz und einer ungesicherten Leistungsbehauptung.

## [1.3.0] — 2026-06-20

### Hinzugefügt

- `/divi-theme-builder` — Divi 5 Theme Builder: Header, Footer, Single Post, Archive, CPT-Templates, WooCommerce, Sticky Header, Dynamic Content
- `/divi-design-system` — Design System: Divi Global Colors, CSS Custom Properties, Fluid Typography mit `clamp()`, Button-Presets, Spacing-System, Colorscheme Generator (Divi 5.5+)
- `/divi-ai` — Divi AI Workflow: Was AI kann, wann Claude Code besser ist, DSGVO-Einschränkungen, Phasen-Workflow
- `/divi-canvas` — Divi Canvases: Popups, Off-Canvas Menüs, Scroll-Trigger, Exit-Intent, Timer, iOS Fix, ARIA
- Wiki: Divi Theme Builder, Divi Design System, Divi AI Workflow, Divi Canvas (4 neue Seiten)
- Beide neue Commands-Sets in `.claude/commands/` und `.codex/commands/`

---

## [1.2.0] — 2026-06-20

### Hinzugefügt

- `/divi-module` — Natives Divi 5 Custom Module erstellen (React/TSX, PHP Traits, `module.json`, Webpack-Externals, D5/D4-Kompatibilitätserkennung)
- `/divi-optimize` — Performance-Optimierung: Core Web Vitals, kritisches CSS, Script-Defer-Strategie, Bild-Optimierung, Caching-Konfiguration, ungenutzte WP-Scripts deaktivieren
- Wiki: GSAP SplitText — vollständiges Beispiel für Textanimationen (Zeichen, Wörter, Zeilen) mit Divi-Kompatibilität
- Beide neuen Commands in `.claude/commands/` und `.codex/commands/`

---

## [1.1.0] — 2026-06-20

### Hinzugefügt

- GitHub Wiki mit 12 Seiten und umfangreichen Code-Beispielen
  - Schnellstart — Installation und alle Slash-Commands mit Beispielen
  - Divi Child-Theme erstellen — vollständige Anleitung mit allen Dateien
  - WordPress-Plugin entwickeln — Sicherheit, AJAX, REST API
  - Animations-Stack — GSAP, Three.js, AOS, Lenis, Alpine.js, Swiper mit Divi-Fixes
  - DSGVO und Fonts — lokales Font-Hosting, Bunny Fonts, Checkliste
  - Divi-Quirks und Fixes — CSS-Spezifität, Builder-Ausschluss, jQuery noConflict
  - Docker-Entwicklungsumgebung — docker-compose.yml, WP-CLI, PHPMyAdmin
  - Library-Referenz — Lizenzen, Versionen, Download-Quellen, DSGVO-konforme Icons
  - Praxisbeispiel Unternehmenswebsite — Hero-Animation, Zähler, AJAX-Kontaktformular
  - Praxisbeispiel App-Landingpage — Three.js Partikel, horizontaler Scroll, Swiper
  - Praxisbeispiel WooCommerce — Template-Overrides, Produkt-Animationen, Payments

---

## [1.0.0] — 2026-06-20

### Hinzugefügt

- Haupt-Skill-Datei `skill/DIVI5-SKILL.md` mit vollständiger Dokumentation
- 11 Slash-Commands für Claude Code und ChatGPT Codex
- `/divi-install` — WordPress + Divi lokal installieren
- `/divi-install-docker` — Docker-Entwicklungsumgebung aufsetzen
- `/divi-childtheme` — Divi Child-Theme mit lokalem Font-Hosting erstellen
- `/divi-backup` — Lokales Backup (DB + Dateien)
- `/divi-dev` — Entwicklungs-Checkliste und Workflow
- `/divi-project-filesystem` — Projektordner mit MGD-AI-Basic-Projektordner
- `/divi-plugin` — WordPress-Plugin mit Sicherheits-Template erstellen
- `/divi-animations` — Animations-Bibliotheken lokal einbinden (GSAP, Three.js, AOS, Lenis, Swiper, Alpine, Tilt)
- `/divi-deploy` — Schrittweises Deployment auf Live-Server
- `/divi-debug` — Systematisches Debugging
- `/divi-release` — Versions-Bump und Release-Workflow
- DSGVO/EU-Datenschutz-Checkliste
- Vollständige Library-Lizenz-Übersicht (MIT + GSAP No-Charge)
- Divi-spezifische Quirks und Fixes für alle Animations-Libraries
- WordPress 7.0 Kompatibilität (PHP 8.3, Block API v3)
