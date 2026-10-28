# Thema C: Divi 5 und WordPress 7 automatisieren (REST, WP-CLI, MCP)

Stand der Recherche: 28.10.2026 (Abrufdatum aller Quellen). Die Quellen selbst tragen meist keine genaue Datumsangabe im Abruf; wo ein Datum erkennbar war, steht es dabei.

Legende: ✅ belegt, ⚠️ wichtiger Hinweis, ☑️ offen/unklar, 🔎 gefunden

---

## 0. Kurzfazit

- ⚠️ Eine offizielle, öffentliche Dokumentation für den Namespace `divi/v1` (auch `ai-agent/*`) wurde NICHT gefunden. Das ist keine Aussage, dass es ihn nicht gibt, nur: nicht dokumentiert.
- ✅ Der eingebaute Divi-AI-Agent läuft nur im Visual Builder, nicht als öffentliche REST-/MCP-Schnittstelle. MCP-Support ist laut Elegant Themes erst für ein künftiges Update angekündigt.
- 🔎 Für externe Automatisierung gibt es Drittanbieter: DiviOps Agent (Plugin + MCP-Server), Respira, JHMG AI Editor. Eigener Namespace `diviops/v1`, nicht `divi/v1`.
- ✅ WordPress: Abilities API (`wp-abilities/v1`) ist seit WP 6.9 im Core. WP 7.0 bringt den AI Client dazu. Der MCP Adapter ist ein separates Plugin.
- ☑️ Kein `wp divi ...` / `wp et ...` Befehl gefunden. Cache leeren geht über Divi-Einstellungen oder Ordner `wp-content/et-cache/` löschen.
- ☑️ Zu `_et_pb_use_builder` bei Divi 5, Playwright-Tests für Divi und Divi 5.18 Changelog: nichts Belastbares gefunden.

---

## 1. Divi-REST-Routen (`divi/v1`)

### 1.1 Was ist belegt

- ✅ Elegant Themes hat intern das Paket `divi/ajax` in `divi/rest` umbenannt und eine REST-Permission-Callback für alle registrierten REST-Routen ergänzt. Das ist interner Code, keine Routenliste.
  Quelle: https://www.elegantthemes.com/blog/general-news/divi-5-may-progress-update (Beta-Zeit, 2024)
- ✅ Divi AI Agent (im Builder eingebaut): Chatfenster in der Visual-Builder-Seitenleiste, über 190 eingebaute "Skills", Anfragen laufen über OpenRouter zu den gewählten KI-Modellen, braucht aktives Divi-AI-Abo, Zugriff ist an den Elegant-Themes-Account gebunden. Kein Hinweis auf öffentliche REST-Route. Zitat der Hilfe: "A future update will add MCP support to Divi 5".
  Quelle: https://help.elegantthemes.com/en/articles/16798164-the-divi-ai-agents-in-divi-5
- ✅ Tool-Kategorien des Divi AI Agent (Seite lesen/bearbeiten, Presets und Design-Variablen, Loops, Theme Builder, Divi Library, Medien, Workspaces). Jedes Tool ist Safe / Moderate / Destructive eingestuft, destruktive brauchen Freigabe. Nichts zu REST/MCP-Zugriff, nichts zu Cache-Tools.
  Quelle: https://www.elegantthemes.com/blog/divi-resources/exploring-all-of-divis-ai-agents-tools

### 1.2 Was NICHT gefunden wurde

- ☑️ Keine dokumentierte Liste für `divi/v1/ai-agent/*`, Layouts, Presets, Variablen, Import/Export, Builder-Cache.
- ☑️ Keine Aussage zu Rechten/Auth für diese Routen.
- 🔎 Praktischer Weg zum Klären (VERMUTET, nicht getestet): auf einer Test-Installation `/wp-json/` als Admin aufrufen und nach Namespace `divi` suchen, oder im Divi-Quellcode nach `register_rest_route` grep'en.

### 1.3 Drittanbieter-Routen (Beispiel DiviOps)

- ✅ DiviOps Agent (WordPress.org): eigene REST-Endpunkte `diviops/v1/*`, Auth per Application Password. Lesen meist `edit_posts`, Schreiben meist `edit_pages`, Presets und Variablen `manage_options`. Erstellen/Status ändern braucht zusätzlich die passende Capability des Post-Typs. Ohne aktives Divi kommt Fehler `divi_unavailable`.
  Quelle: https://wordpress.org/plugins/diviops-agent/
- ✅ Einzige konkret genannte Route im GitHub-Readme: `/wp-json/diviops/v1/schema/settings` (ohne Login 401, zeigt dass Plugin aktiv ist). Rest siehe `diviops-server/README.md` im Repo.
  Quelle: https://github.com/oaris-dev/diviops

---

## 2. WordPress 7: Abilities API und MCP-Adapter

### 2.1 Was ist das (einfach erklärt)

- Abilities API = ein "Fähigkeiten-Verzeichnis" in WordPress. Plugins melden darin an, was man tun kann (z. B. "Seite anlegen"), samt Eingabe-Schema und Rechteprüfung.
- MCP-Adapter = Übersetzer, der diese Fähigkeiten als MCP-Tools für KI-Clients (Claude, Cursor ...) bereitstellt.

### 2.2 Belege

- ✅ `wp-abilities/v1` stammt aus WordPress 6.9 (PHP-API zum Registrieren, REST-Endpunkte, Hooks). Auflisten als Admin: `https://deine-seite/wp-json/wp-abilities/v1/`. Mehrere Quellen verwechseln 6.9 und 7.0; WP 7.0 ergänzt den AI Client.
  Quellen: https://jorijn.com/en/blog/wordpress-7-0-abilities-mcp-plugin-developers-learn-first/ , https://webdevstudios.com/2026/06/29/decoding-wordpress-7-0-how-the-abilities-api-and-mcp-adapter-change-enterprise-ai/
- ✅ Client-seitig (WP 7.0): `@wordpress/abilities` und `@wordpress/core-abilities` laden Server-Abilities aus `/wp-abilities/v1/`. Ausführung per HTTP GET (readonly), DELETE (destructive + idempotent), sonst POST. Bekanntes Problem: `sanitize_callback` kann die Schema-Validierung brechen.
  Quelle: https://make.wordpress.org/core/2026/03/24/client-side-abilities-api-in-wordpress-7-0/ (24.03.2026)
- ✅ MCP-Adapter (offizieller Dev-Blog, Feb 2026): Plugin aus GitHub `WordPress/mcp-adapter` installieren. Standard-Server `mcp-adapter-default-server` mit drei Tools: `mcp-adapter-discover-abilities`, `mcp-adapter-get-ability-info`, `mcp-adapter-execute-ability`.
  Quelle: https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/
- ✅ Abilities sind für den Default-Server nur sichtbar, wenn beim Registrieren `'meta' => array( 'mcp' => array( 'public' => true ) )` gesetzt ist. Core-Abilities (`core/get-site-info` usw.) bekommen das Flag über den Filter `wp_register_ability_args`. Eigene Server (`create_server()` per Hook `mcp_adapter_init`) brauchen das Flag nicht.
- ✅ Transport:
  - STDIO (lokal): `wp mcp-adapter serve --server=mcp-adapter-default-server --user=...` (braucht WP-CLI)
  - HTTP (remote): Endpunkt `https://deineseite/wp-json/mcp/mcp-adapter-default-server`, Proxy `@automattic/mcp-wordpress-remote` (Node/npx), Auth per Application Password.
- ⚠️ Widerspruch in Drittquellen: manche nennen `/wp-json/mcp/v1/`. Der offizielle Dev-Blog nennt `/wp-json/mcp/mcp-adapter-default-server`. Im Zweifel `/wp-json/` selbst abfragen. ☑️
- ✅ OAuth: laut Dev-Blog "über eigene Implementierung möglich", kein fertiger OAuth-Server im Adapter beschrieben. ☑️ Ein "OAuth-Server" mit festem Namen wurde nicht belegt.
- ✅ Hinweis aus Suchergebnis: MCP Adapter verlangt WordPress 6.9+ (Plugin-Seite https://wordpress.org/plugins/?p=374872). ☑️ Meta-Public wird laut Listing in 7.1 an `show_in_rest` gekoppelt (nur Drittquelle, nicht geprüft).

### 2.3 Sicherheitsempfehlungen (aus Dev-Blog, ✅)

- Pro Ability die minimal nötige Capability prüfen. Kein `__return_true` bei zerstörerischen Aktionen.
- Eigener Benutzer mit kleiner Rolle statt Admin-Account.
- Bei öffentlich erreichbaren HTTP-Endpunkten erst nur lesende Abilities.
- Application Password ist Standard; für mehr Kontrolle OAuth ergänzen.
- Fehler- und Observability-Handler für Protokoll der Agent-Aktionen.
- Ergänzend (VERMUTET, gesunder Menschenverstand): erst Staging, Backup vor Schreibläufen, HTTPS Pflicht, Application Password nur in der lokalen Client-Config, nicht ins Repo.

### 2.4 Divi-Abilities/Tools

- ☑️ Keine offiziellen Divi-Abilities für den WP-MCP-Adapter dokumentiert gefunden. Offiziell steht nur "MCP kommt in einem künftigen Update".
- 🔎 Drittanbieter: DiviOps (MCP-Server `@diviops/mcp-server`, Node 22+; Tools z. B. `diviops_meta_info`, `diviops_page_create`, `diviops_validate_blocks`, `diviops_meta_flush_cache`, `diviops_meta_wp_cli`). Quelle: https://diviops.com/docs/ und https://github.com/oaris-dev/diviops
- 🔎 Weitere: Respira (https://www.respira.press/cli/docs/builders/divi), JHMG AI Editor (https://wordpress.org/plugins/?p=379088), Novamira (https://novamira.ai/mcp/divi/, Abruf 403, nicht geprüft). Alle Drittanbieter = fremder Code mit Schreibzugriff, vorher prüfen.

---

## 3. Seiten per `wp/v2/pages` mit Divi-5-Inhalt

- ✅ Divi 5 speichert Layouts als Block-Kommentare in `post_content` (Divi 4: verschachtelte Shortcodes). Jeder Block trägt `builderVersion`. Beispiel aus Skill-Seite: `wp:divi/placeholder`. Quelle: Suchtreffer https://wordpress.org/plugins/?p=379088 und https://skillsmp.com/de/creators/oaris-dev/diviops/skills-divi-5-builder
- ⚠️ String-Basteln an Divi-5-Blöcken ist riskant (Drittquelle). Besser Schema/Validierung nutzen.
- ✅ DiviOps-Praxis (Changelog-Aussagen): erst Dry-Run, Prüfsumme (Checksum) gegen paralleles Überschreiben, Rollback-Snapshot, Nachlesen nach dem Schreiben, JSON- und Block-Begrenzer müssen gültig bleiben, bestimmte Strings in Button-Attributen werden abgelehnt. Quelle: https://wordpress.org/plugins/diviops-agent/
- ✅ Empfohlener Ablauf (DiviOps-Doku): Staging, Seite als unveröffentlichten Entwurf anlegen, Markup validieren (vor und nach dem Speichern), nie bestehende Seiten/Presets anfassen, nicht veröffentlichen. Quelle: https://diviops.com/docs/
- ✅ Cache: Divi liefert Frontend-CSS aus `wp-content/et-cache/{post_id}/`. `wp cache flush` leert das NICHT. Nach Preset-Änderungen Cache extra leeren. Quelle: https://github.com/oaris-dev/diviops
- ☑️ `_et_pb_use_builder` (Divi 4) bzw. Divi-5-Äquivalent als Meta, Page-Template-Pflicht: NICHT belegt gefunden. Nicht raten; auf Test-Install per `wp post meta list <ID>` an einer im Builder gespeicherten Seite ablesen. (VERMUTET, dass Divi die Meta-Felder beim ersten Builder-Speichern selbst setzt.)
- ☑️ Revisionen: nur DiviOps-eigene Snapshots belegt; WP-Standardrevisionen laufen bei `wp/v2/pages` normal mit (VERMUTET, Standardverhalten WordPress).
- ⚠️ Divi-5-Seiten sind groß: bei REST-Timeouts Limits erhöhen (Hinweis aus Suchtreffer zu MCP-Servern, Drittquelle).
- Beispiel (VERMUTET, nur das generische WP-REST-Muster, Inhalt ist Platzhalter):

```bash
# Entwurf anlegen, Application Password
curl -u "USER:APP-PASSWORT" -X POST \
  https://staging.example.de/wp-json/wp/v2/pages \
  -H "Content-Type: application/json" \
  -d '{"title":"Test","status":"draft","content":"<!-- wp:divi/... -->"}'
```

---

## 4. WP-CLI und Cache

- ☑️ Kein `wp divi` / `wp et` Befehl gefunden (weder Suche noch Doku).
- ✅ Statisches CSS leeren per Admin: Divi > Theme-Optionen > Builder > Advanced > Static CSS File Generation > CLEAR (Pfad aus älterer Divi-Version, in Divi 5 ggf. anders). Alternativ Inhalt von `wp-content/et-cache/` löschen. Quellen: https://divibooster.com/clearing-divis-static-css-cache/ , https://pressable.com/blog/clearing-css-cache-in-divi/
- 🔎 Plugin "Builder Critical CSS Tools" nutzt Divis interne Cache-Methode (Funktionsname nicht gefunden). https://wordpress.org/plugins/builder-critical-css-tools/
- Muster (VERMUTET, funktioniert nur wenn Pfad stimmt):

```bash
# Divi Cache leeren
wp eval 'array_map("unlink", glob(WP_CONTENT_DIR."/et-cache/*/*"));'
# WP Objekt-Cache
wp cache flush
```

- ⚠️ Das `wp eval`-Beispiel löscht nur Dateien eine Ebene tief; vor Einsatz auf Staging testen oder `rm -rf wp-content/et-cache/*` per Shell nutzen.
- ✅ DiviOps hat `diviops_meta_wp_cli` als Notausgang, vom Server begrenzt (braucht `WP_PATH`). Details in deren SETUP.md.

---

## 5. Testen und Abnahme (Visual Builder bleibt bearbeitbar)

- ✅ Nur eine dokumentierte Prüfung: DiviOps empfiehlt Entwurf im Visual Builder öffnen, eine Überschrift ändern, Desktop- und Mobile-Vorschau prüfen, Teständerung wieder entfernen. Und: Strukturprüfung "ersetzt keine visuelle Prüfung". Quellen: https://diviops.com/docs/ , https://wordpress.org/plugins/diviops-agent/
- ☑️ Kein Hinweis auf offizielle Playwright-/Headless-Tests für den Divi-Builder gefunden (Suche ohne Treffer).
- VERMUTET (eigene Ableitung, nicht belegt) für eine Abnahme:
  1. Per REST/Validierungstool prüfen, dass nur native `divi/*`-Blöcke vorkommen (keine Roh-HTML-Blöcke).
  2. Playwright: als eingeloggter Admin die Seite mit `?et_fb=1` öffnen (Divi-Visual-Builder-Parameter, aus Divi 4 bekannt, für Divi 5 prüfen), warten bis Builder geladen, Konsole auf Fehler prüfen, Überschrift ändern, speichern, Seite neu laden, Text prüfen.
  3. Screenshots Desktop/Tablet/Mobile vergleichen.
  4. Auf Staging, mit Backup, Application Password nur für Testnutzer.

---

## 6. Offene Punkte

- ☑️ Existiert `divi/v1` überhaupt öffentlich? Auf Test-Install `/wp-json/` prüfen.
- ☑️ Divi 5.18 Changelog (offiziell) prüfen: https://www.elegantthemes.com/blog/ (Release Notes), MCP-Support angekündigt, Stand unklar.
- ☑️ Exakte Meta-Felder für Divi-5-Seiten per Stichprobe ermitteln.
- ☑️ Endpoint-Pfad MCP: `/wp-json/mcp/mcp-adapter-default-server` (Dev-Blog) vs. `/wp-json/mcp/v1/` (Drittquelle).
