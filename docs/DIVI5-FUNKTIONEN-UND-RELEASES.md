# Thema B: Divi 5 Funktionen und Release-Stand (Recherche 28.10.2026)

Marker: ✅ belegt | ⚠️ wichtiger Hinweis | ☑️ offen/unklar | 🔎 gefunden

## 0. Wichtigste Punkte vorab
- ✅ Divi 5.0.0 (stabil) erschien am 26.02.2026. Quelle: Hilfe-Center Update-Status https://help.elegantthemes.com/en/articles/9973580-divi-5-update-status
- ⚠️ Neueste gefundene Version: **5.17 (22.10.2026)**. Eine Version 5.18 habe ich nirgends gefunden (☑️ evtl. noch nicht erschienen oder nicht indexiert; in der Update-Status-Liste endet es bei 5.17).
- ⚠️ Sicherheitsfixes in fast jedem Release: immer auf aktuelle Version updaten (siehe Tabelle).
- ☑️ Offizielle Mindestanforderung "WordPress 7" für Divi 5 nicht gefunden. Hosting-Seite nennt nur WP 5.3 Minimum (siehe Abschnitt 4).

## 1. Release-Geschichte (Quelle: Hilfe-Center Update-Status, https://help.elegantthemes.com/en/articles/9973580-divi-5-update-status)
Die Seite nennt selbst keine "Breaking Changes" (✅). Datumsformat dort MM-TT-JJJJ.

| Version | Datum | Wichtigste Neuerungen | Sicherheit |
|---|---|---|---|
| 5.0.0 | 26.02.2026 | Erster stabiler Release, viele Migrations-/Preset-/Builder-Fixes | - |
| 5.0.1 | 26.02.2026 | Beta-Code entfernt | - |
| 5.0.2 | 09.03.2026 | Editierbare Theme-Builder-Bereiche, Performance | - |
| 5.0.3 | 11.03.2026 | Doku für Custom Modules, Link-Farbe aus Customizer als globale Farbe, AI-Agent-Gerüst | - |
| 5.1.0 | 13.03.2026 | AI-Agent-Icon (Feature-Flag) | - |
| 5.1.1 | 01.04.2026 | **Composable Settings** | Stored XSS im Video-Slider-Shortcode (Contributor+), SSRF bei Video-Thumbnails, unsichere Redirect-URLs im Kontaktformular |
| 5.2.0 | 01.04.2026 | AI-Agent: "Neuer Chat", Vorschau hell/dunkel | - |
| 5.2.1 | 09.04.2026 | Freigabe-Schritt (Human-in-the-loop) für zerstörerische KI-Aktionen; WP-7.0-Button-Fixes | - |
| 5.3.0 | 20.04.2026 | Contact Form 7 Styler, Checkbox/Radio-Gruppen, Focus/Checked/Active-Zustände | - |
| 5.3.1-5.3.3 | 21.-23.04.2026 | Fixes (Presets, Gradients, Post Navigation, PHP-8-Fatal bei Kommentaren) | - |
| 5.4 | 30.04.2026 | **Variable Generator**, Breadcrumbs-Modul, AI-Chat-Verlauf, weniger ungenutztes CSS | - |
| 5.4.1 | 05.05.2026 | AI-Agent Canvas- und Seiten-Tools | - |
| 5.5.0 | 08.05.2026 | SVG-Workflow, Seitenverhältnis-Einstellungen für Bilder, Constant Contact OAuth 2.0 | - |
| 5.5.1 | 11.05.2026 | AI-Checkpoints | - |
| 5.5.2 | 16.05.2026 | Timeline-Modul, Stop-Button für AI, Farbharmonie-Generatoren | - |
| 5.6.0 | 22.05.2026 | Instagram-Feed- und Inhaltsverzeichnis-Modul | - |
| 5.6.1 | 28.05.2026 | **Altes D4-Frontend-Runtime entfernt**; Hinweis: ungültige Bilddaten werden strenger behandelt, manche Bilder erscheinen evtl. erst nach Neu-Speichern | - |
| 5.6.2 | 29.05.2026 | Fixes (Bibliothek, Responsive Editor) | - |
| 5.7.0 | 05.06.2026 | Verlaufs-Felder + Gradient-Variablen, Textfüllung, "In Variable umwandeln" | (Liste abgeschnitten) |
| 5.7.1-5.7.3 | 08.-10.06.2026 | Fixes | - |
| 5.7.4 | 12.06.2026 | Workspace-Verwaltung | - |
| 5.8.0 / 5.8.1 | 19.06. / 25.06.2026 | Tooltip-Modul; Fließtext-Styling, Initialen, Variable Fonts | - |
| 5.9.0 | 09.07.2026 | **Grid Editor** | VB-REST-Antworten gaben Instagram-Tokens preis; ungültige Post-Navigation-Kontexte |
| 5.10.0 / .1 | 07./09.08.2026 | Post Filter + Post Filter Item, Lazy Loading unterhalb des Sichtbereichs, Produkt-Updates-Panel | Fatal-Error-Fixes (Mercado Pago, Speicher) |
| 5.11 / 5.11.1 | 13./19.08.2026 | Gravity-Forms-Modul, Charts, Payment Button, Imagely Gallery; Backdrop-Blur/Filter | - |
| 5.12 / 5.12.1 | 03./05.09.2026 | **AI Agents** eingeführt; Slider-Swipe-Leiste | 5.12.1: interne Dev-Tools lagen im öffentlichen ZIP (löste Malware-Scanner aus) |
| 5.13 / 5.13.1 | 11./18.09.2026 | Formular-Labels, Plugin-API für Icon-Fonts | Viele: KI-Freigabe für riskante Aktionen, SSRF beim Layout-Export, Cloud-Token, unescaped HTML in Loops, Contributor konnte Shortcodes ausführen (VB-AJAX), XSS im Audio-Modul |
| 5.14 | 28.09.2026 | Fixes, Sass-Modul-Migration | Tabs-Titel: unescaped HTML |
| 5.15 / 5.15.1 | 09.10.2026 | **Components-Überarbeitung + Slot-Modul**, Components-Import/Export, neue AI-Tools | Divi-Library konnte fremde Beiträge überschreiben; Kontaktformular: Zeilenumbrüche konnten in Mail-Header |
| 5.16 | 16.10.2026 | Einklappbares Mobile-Menü, Mehrfachauswahl/Bulk-Edit | - |
| 5.17 | 22.10.2026 | Icon-Picker + **Icon Manager** (SVG/Icon-Font-Import) | Editor ohne Publish-Recht konnte über Page Manager veröffentlichen; Rechte-Fixes bei Theme Options/Import; unsichere Custom Attributes in Presets blockiert |

Weitere Meilensteine (🔎 Suchtreffer, nicht tief geprüft):
- Public Beta ab 17.10.2025 (kopfundstift.de, ☑️ Drittquelle). Alpha 19 brachte Flexbox, Interactions, Relative Colors, Find & Replace: https://www.elegantthemes.com/blog/divi-resources/divi-5-public-alpha-19
- Offizieller Termin: https://www.elegantthemes.com/blog/general-news/divi-5-official-release-date

⚠️ Hinweis: Die Update-Status-Seite ist sehr lang (ca. 190.000 Zeichen); ich habe sie bis 5.7.0 vollständig gelesen, Details darunter (ältere Alpha-/Beta-Einträge) nicht.

## 2. Kernkonzepte (praktisch)
Quellen: https://www.elegantthemes.com/blog/divi-resources/how-to-get-started-with-divi-5 (✅ für alles mit diesem Marker), Hilfe-Center-Artikel wie angegeben.

- **Design Variables** ✅: Globale Werte (Zahlen, Text, Bilder, Links, Farben, Schriften) im Variable Manager. Wert ändern, alle Stellen ziehen mit. Praxis: erst Variablen anlegen (Farben, Abstände, Schriftgrößen), dann überall referenzieren. Seit 5.4 Variable Generator, seit 5.7 "In Variable umwandeln".
- **Option Group Presets** ✅: Stil für eine Eigenschaftsgruppe (z. B. Rahmen, Hintergrund, Buttons), seitenweit nutzbar. https://help.elegantthemes.com/en/articles/10725144-how-to-use-option-group-presets-in-divi-5
- **Element Presets** ✅: Stil für ein ganzes Modul. https://help.elegantthemes.com/en/articles/13349150-advanced-styling-using-element-presets-in-divi-5
- **Stacked/Nested Presets** ✅: Mehrere Presets übereinander (Basis + Variante); Option Group Presets bleiben in Element Presets als Live-Verknüpfung. Neuere "Nested Option Presets" erlauben ein Preset in einem Preset. https://www.elegantthemes.com/blog/divi-resources/everything-you-need-to-know-about-divi-5s-nested-option-presets . Empfehlung (VERMUTET): kleines Basis-Preset plus Variationen, wenig Verschachtelungstiefe.
- **Canvases** ✅: Eigene Arbeitsflächen für Inhalte außerhalb der Seite (Popups, Menüs, Slide-in-Header); Canvas-Portal-Modul bindet sie ein.
- **Theme Builder** ☑️: Im Einstiegsartikel nur erwähnt. Aus Update-Status belegt: editierbare Theme-Builder-Bereiche seit 5.0.2, Template-Bearbeitungseinstellung seit 5.11.1. Header/Footer/Bedingungen im Detail NICHT recherchiert (Divi-4-Prinzip, VERMUTET gleich).
- **Components/Slots** ✅ (neu, Status: ausgeliefert seit 5.15, 09.10.2026): Components ersetzen globale Module; Slots sind freie Bereiche pro Instanz; Komponenten können Komponenten enthalten (keine Zirkelbezüge); Anlegen/Bearbeiten braucht das Recht "Edit Global Items". https://help.elegantthemes.com/en/articles/17438180-components-in-divi-5 und https://www.elegantthemes.com/blog/divi-resources/exploring-slots-for-components-in-divi-5 . ⚠️ Sehr jung, erst auf Staging testen.
- **Composable Settings** ✅ seit 5.1.1 genannt; inhaltliche Erklärung ☑️ nicht gelesen.
- **Command Center** ✅: Suchleiste per Blitz-Symbol oder Cmd/Strg+K; Elemente einfügen, Ansichten wechseln (Breakpoints, Wireframe). https://help.elegantthemes.com/en/articles/13741079-the-divi-5-command-center
- **Wireframe-Ansicht** ✅: Abschnitte/Zeilen/Module als beschriftete Blöcke, gut für Struktur. https://help.elegantthemes.com/en/articles/10469465-wireframe-view-in-divi-5
- **Responsive/Container Queries**: Container Queries ☑️ im Einstiegsartikel NICHT erwähnt, nicht belegt. Responsive Editor + Breakpoints ✅ vorhanden.
- **Flexbox/Grid** ✅: Flexbox im Layout-Menü; CSS Grid mit Grid-Vorlagen und Offset-Regeln; Grid Editor seit 5.9.
- **Animationen/Interactions** ✅: Transforms/Animationen im Design-Tab; Interactions im Advanced-Tab (Trigger Klick/Hover/Viewport -> Aktion auf Ziel-Modul, mit Verzögerung).
- **Loop Builder/Dynamic Content** ✅: Loop-Element einmal gestalten, Divi füllt es mit Beiträgen/Produkten, mit Filtern und Paginierung.
- **WooCommerce** ✅: 19 native Module (Produktraster, Produktseite, Warenkorb, Kasse, Bewertungen).
- **Workspaces** ✅ seit 5.7.4: https://www.elegantthemes.com/blog/divi-resources/everything-you-need-to-know-about-workspaces-in-divi-5

## 3. Divi AI / AI-Agent
Quellen: https://help.elegantthemes.com/en/articles/16798164-the-divi-ai-agent-in-divi-5 , https://help.elegantthemes.com/en/articles/16844129-divi-ai-agent-billing-and-your-ai-wallet , https://www.elegantthemes.com/blog/divi-resources/how-divi-ai-agents-pricing-works
- ✅ Kann: Layouts aus Text/Screenshot/URL/Moodboard bauen, bestehende Layouts umbauen, seitenweite Änderungen (Alt-Texte, Farben in Variablen, Rechtschreibung, Responsive), über 190 Skills (Seiten, Beiträge, Menüs, Theme-Builder-Vorlagen, Bibliothek, einzelne Theme-Optionen), Divi-Fragen beantworten. Modellwahl möglich.
- ✅ Kosten: Divi-AI-Abo nötig (oder Divi Pro). Agent ist zusätzlich nach Verbrauch bemessen: 5 USD Guthaben pro Monat im Abo (Reset am Verlängerungstag, verfällt), Aufstocken über "AI Wallet". Kein kostenloser Test. Erstattung ungenutzten Guthabens innerhalb 30 Tage. Abo-Preise selbst: https://help.elegantthemes.com/en/articles/8289311-divi-ai-pricing-overview (☑️ nicht geöffnet).
- ✅ Datenschutz: Seiteninhalte (Texte, Layout, Moduleinstellungen) gehen an den gewählten KI-Anbieter (z. B. Anthropic, OpenAI) über **OpenRouter**. Jeder Anbieter hat eigene Speicher-/Trainingsregeln (siehe OpenRouter-Datenschutz). Internet nötig, auch bei lokal/Staging.
- ⚠️ DSGVO für Kundenprojekte: Drittlandübertragung (USA) und AV-Vertrag prüfen; ob ein AVV mit Elegant Themes/OpenRouter existiert, habe ich NICHT gefunden (☑️).
- ✅ Einschränkungen: nur Divi 5; Ergebnisse sind Ausgangspunkt, keine Kopien; außerhalb des Builders weniger Funktionen; eigener API-Key noch nicht möglich (MCP geplant). Laut Hilfe-Artikel keine Möglichkeit, den Agent per Rollen-Editor ganz abzuschalten und kein beschriebener Bestätigungsschritt, ABER Update-Status nennt Freigabe für zerstörerische Aktionen (5.2.1) und riskante Aktionen (5.13). Widerspruch ☑️ in Praxis prüfen.

## 4. Systemanforderungen und Konflikte
- ✅ Hosting-Seite: https://help.elegantthemes.com/en/articles/10340853-divi-hosting-requirements-optimizing-your-server-for-peak-performance : WordPress min. 5.3 (empfohlen: aktuell), MySQL 5.7+/MariaDB 10.2+ (empfohlen MySQL 8.0+/MariaDB 10.11+), PHP-Memory 128M (empfohlen 256M+), PHP empfohlen 8.2 bis 8.5 (Patch-Stände genannt). Keine Divi-5-spezifischen Werte auf der Seite.
- ☑️ "WordPress 7" als Pflicht: nicht belegt. Belegt nur: 5.2.1 enthält "WordPress 7.0 button fixes", d. h. Divi passt sich an WP 7.0 an.
- ☑️ Konflikte Performance/WP Rocket/Complianz/Rank Math: KEINE offizielle Aussage gefunden.
  - ✅ Divi 5 hat Cache-Integrationen (u. a. WP Rocket, Cloudflare-Plugin, Swift Performance), die Cache leeren, wenn Presets/Variablen geändert werden (🔎 Suchergebnis zu "New Cache Improvements For Divi 5").
  - 🔎 Rank Math: Foren-Hinweis, dass JS-Aktionen im Divi-Umfeld bei aktivem Rank Math nicht liefen (Altfall, unklar welche Version). Complianz: nichts zu Divi 5.
  - VERMUTET: Nach Updates/Preset-Änderungen Cache leeren, JS-Minify/Defer-Optionen ausschließen, Staging-Test.
- ⚠️ Drittanbieter-Module ohne D5-Version laufen im Kompatibilitätsmodus (D4-Engine), kein D5-Performancegewinn.

## 5. Migration Divi 4 -> 5
Quelle: https://elegantthemes.com/blog/divi-resources/how-to-migrate-your-website-to-divi-5 und https://help.elegantthemes.com/en/articles/12767407-how-to-safely-migrate-from-divi-4-to-divi-5
- ✅ Ablauf: Backup + Staging; alles updaten (Divi 4.27.6 oder höher); Erweiterungen auf D5-Kompatibilität prüfen; Divi 5 aktivieren oder ZIP hochladen; Menü Divi > Divi 5 Migrator; Kompatibilitätscheck (blauer Haken = nativ, orange = Rückwärtskompatibilitätsmodus); "Migrate This Site to Divi 5"; testen (Templates, WooCommerce, Formulare); live schalten.
- ✅ Shortcodes werden automatisch ins neue Format umgewandelt; Dauer meist Sekunden bis Minuten.
- ✅ Rollback: Button "Restore Divi 4 Content", sonst Staging/Backup.
- ⚠️ Bekannte Probleme laut Kommentaren: Check hängt (Plugins deaktivieren, Memory-Limit erhöhen), Layout-/Farb-/Hover-Abweichungen, Staging ca. 25 % größer.
- ✅ Elementor: im Migrationsartikel nicht erwähnt. ☑️ Ob es einen Elementor-Import gibt: nicht gefunden.
- 🔎 Hinweis aus Kommentaren: Divi-4-Support mindestens 12 Monate (nur Kommentar, nicht offiziell belegt).

## 6. Offene Punkte
- ☑️ Version 5.18 prüfen (https://www.elegantthemes.com/blog/category/theme-releases/ und Update-Status-Seite).
- ☑️ Theme-Builder-Details, Container Queries, Composable Settings, AVV/DSGVO zur KI.
- ☑️ Konflikte mit WP Rocket, Complianz, Rank Math selbst auf Staging testen.
