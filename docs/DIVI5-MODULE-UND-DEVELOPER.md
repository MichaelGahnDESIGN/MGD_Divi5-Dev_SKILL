# Thema D: Divi-5-Developer-Doku und Standardmodule

Stand der Recherche: 28.10.2026. Marker: ✅ belegt, ⚠️ wichtiger Hinweis, ☑️ offen/unklar, 🔎 gefunden.
Alle Webinhalte wurden nur als Daten ausgewertet.

---

## 1. Developer-Doku (Eigene Module)

### 1.1 Wo die Doku liegt
- ✅ Die Entwickler-Doku ist umgezogen: `elegantthemes.com/documentation/developers/` leitet per 301 auf **https://dev.elegantthemes.com/** weiter (Quelle: Abruf der Seite).
- 🔎 Bereiche auf dev.elegantthemes.com: `/docs` (Intro), `/docs/getting-started/installing-divi-5`, `/docs/tutorials/module/beginner/...`, `/docs/hooks` (PHP-Action- und Filter-Hooks), `/docs/extension-examples`, API-Referenz JS `/api/js/` und PHP `/api/php/Global/`.
- 🔎 Beispiel-Repos auf GitHub (Quelle: dev.elegantthemes.com/docs/extension-examples und GitHub):
  - `elegantthemes/d5-example-core-modules` (Ordner: accordion, blog, blurb, button, contact-form, cta, login, pricing-tables, signup, slider). README: nur Studienmaterial, "nicht als echtes Plugin einsetzen".
  - `elegantthemes/d5-extension-example-modules` (5 Modultypen: static, dynamic, parent, child, converted).
  - `elegantthemes/d5-extension-example-modal-dev-state-monitor` und `...-modal-dev-clipboard` (Debug-Modals; Seite sagt, der State-Monitor ist veraltet).
- ☑️ Ein "Starter-Plugin" oder `create-divi-extension` wird in der Doku von Divi 5 **nicht** erwähnt. `create-divi-extension` taucht nur in einem Drittanbieter-Tutorial (diviextended.com, Divi-4-Stand) auf. Nicht für Divi 5 übernehmen.

### 1.2 Aufbau des offiziellen Mini-Moduls (Tutorial "Create Divi 5 Module in 10 Minutes")
✅ Quelle: https://dev.elegantthemes.com/docs/tutorials/module/beginner/create-simple-quick-module

```
d5-tutorial-simple-quick-module/
├── d5-tutorial-simple-quick-module.php   (Plugin-Hauptdatei)
├── server/index.php                      (PHP: Registrierung + Render)
└── visual-builder/
    ├── package.json
    ├── webpack.config.js
    ├── src/
    │   ├── index.jsx                     (Builder-Komponenten, registerModule)
    │   └── module.json                   (Metadaten, von PHP UND JS genutzt)
    └── build/...js                       (Ergebnis von npm run build)
```

- ✅ Build: `cd visual-builder`, `npm install`, `npm run build` (minifiziert) oder `npm run start` (Watch). Kein yarn, kein create-divi-extension.
- ✅ Webpack: Entry `./src/index.jsx`, Babel (`preset-env`, `preset-react`), `react` als External (globales React).
- ✅ module.json Top-Level-Keys: `name`, `d4Shortcode`, `title`, `titles`, `category`, `moduleClassName`, `moduleOrderClassName`, `attributes`, `settings`.
  - `name` z. B. `d5-tut/simple-quick-module`, `d4Shortcode` z. B. `d5_tut_simple_quick_module`.
  - Selektoren mit Platzhalter `{{selector}}` (z. B. `{{selector}} .d5_tut_simple_quick_module_title`).
  - Element-Attribute: `tag`, Inline-Editor `plainText` bzw. `richText`, `innerContent` mit Komponente `divi/text` bzw. `divi/richtext`.
  - `settings`: `content`, `design`, `advanced` jeweils `"auto"`.
- ✅ PHP (server/index.php): Namespace `D5TUTSimpleQuickModule`, Klasse implementiert `DependencyInterface` (`ET\Builder\Framework\DependencyManagement\Interfaces\DependencyInterface`). `load()` hängt `register_module` an `init`. `register_module()` ruft `ModuleRegistration::register_module( $pfad_zum_ordner_mit_module_json, [ 'render_callback' => [ self::class, 'render_callback' ] ] )`.
- ✅ Registrierung in die Modul-Bibliothek:

```php
// Modul in den Dependency-Tree
add_action(
    'divi_module_library_modules_dependency_tree',
    function( $dependency_tree ) {
        $dependency_tree->add_dependency( new D5TutorialSimpleQuickModule() );
    }
);
```
- ✅ `render_callback( $attrs, $content, $block, $elements )` ist statisch und gibt über `Module::render([...])` aus. Wichtige Keys: `orderIndex`, `storeInstance`, `attrs`, `elements`, `id`, `moduleClassName`, `name`, `classnamesFunction`, `stylesComponent`, `scriptDataComponent`, `moduleCategory`, `children`.
- ✅ Weitere PHP-Imports: `ET\Builder\Framework\Utility\HTMLUtility`, `ET\Builder\FrontEnd\Module\Style`, `ET\Builder\Packages\Module\Module`, `ET\Builder\Packages\Module\Options\Element\ElementClassnames`, `ET\Builder\Packages\ModuleLibrary\ModuleRegistration`.
- ✅ Builder-Assets laden (Plugin-Hauptdatei), nur wenn `et_core_is_fb_enabled()` und `et_builder_d5_enabled()` wahr sind, am Hook `divi_visual_builder_assets_before_enqueue_scripts`:
  `PackageBuildManager::register_package_build()` mit Name, Script-URL, Dependencies `react`, `jquery`, `divi-module-library`, `wp-hooks`, `divi-rest`, und Flags `enqueue_app_window => true`, `enqueue_top_window => false`.
- ✅ JS-Registrierung (index.jsx):
  `addAction('divi.moduleLibrary.registerModuleLibraryStore.after', 'd5Tut.simpleQuickModule', () => { registerModule(simpleQuickModule.metadata, simpleQuickModule); })`. Das Modul-Objekt hat `metadata`, `renderers.edit` (React-Komponente mit `ModuleContainer`) und `placeholderContent`.
- ✅ TSX-Imports laut Tutorial "Customizing Module": `@divi/module` (`ModuleContainer`, `StyleContainer`, `elementClassnames`, Settings-Gruppen wie `FontGroup`, `SpacingGroup`, `BorderGroup`, `BackgroundGroup`, `AdminLabelGroup`, `PositionSettingsGroup`, `VisibilitySettingsGroup`...), `@divi/field-library` (`RichTextContainer`, `TextContainer`), `@divi/modal` (`GroupContainer`), `@divi/module-library` (`registerModule`).

### 1.3 Attribut-Pfade
✅ Quelle: https://dev.elegantthemes.com/docs/tutorials/module/beginner/module-attributes
- Ebenen: Element (`module`, `title`) > Teil (`innerContent`, `decoration`, `meta`, `advanced`) > Option (z. B. `spacing`) > Breakpoint (`desktop`, `tablet`, `phone`) > Status (`value`, `hover`, `sticky`) > Wert (String oder Objekt, z. B. Spacing mit top/right/bottom/left).
- `innerContent` hat **keine** Options-Ebene: Pfad `module.innerContent.desktop.value`.
- `decoration`-Option-Keys sind fest vorgegeben (animation, background, spacing, sizing ...).
- Verschachtelte Gruppen (z. B. `font`) setzen einen Namen vor den Breakpoint: `...title = { font: { desktop: { value: {...} } } }`.

### 1.4 Dynamic Content
- 🔎 Es gibt keinen eigenen Dynamic-Content-Abschnitt in den Beispielen. Die PHP-Filter-Hooks (https://dev.elegantthemes.com/docs/hooks/php/filters/) enthalten Filter für aufgelöste Dynamic-Content-Werte, pro Option und für die Optionsliste, außerdem für Custom-Meta-Felder (auch versteckte mit Unterstrich). Genaue Hook-Namen habe ich nicht abgerufen.
- ☑️ Die Dev-Beta-Notizen erwähnen eine "neue Art", Dynamic-Content-Optionen zu registrieren; die konkrete API ist nicht belegt.
- 🔎 Für Loop-Selektoren eigener Module: Tutorial "Adding Loop Group" (`/docs/tutorials/module/advanced/customize-module-settings-output/adding-loop-group`).

### 1.5 Abgleich mit Skill-Abschnitt `/divi-module` (~/.claude/skills/mgd-divi5-dev/SKILL.md, ab Zeile 966)

| Punkt im Skill | Offizielle Quelle | Bewertung |
|---|---|---|
| Hook `divi_module_library_modules_dependency_tree` | gleicher Hook | ✅ passt |
| `$tree->register(new MeinModul())` | `$dependency_tree->add_dependency( new Klasse() )` | ⚠️ Methode weicht ab. Offiziell `add_dependency`. Skill-Variante ist unbelegt, vermutlich falsch |
| Klasse ohne `load()` / `DependencyInterface` | Klasse implementiert `DependencyInterface`, `load()` hängt `register_module` an `init` | ⚠️ im Skill fehlt das |
| `ModuleRegistration::register_module(...)` fehlt komplett | Pflicht, liest `module.json` und setzt `render_callback` | ⚠️ im Skill fehlt das |
| module.json: `"selector": "%%order_class%%"` | `{{selector}}` | ⚠️ Platzhalter abweichend (`%%order_class%%` ist Divi-4-Stil) |
| module.json: `wrapper`, `tagName`, `"settings": {"editors": [...]}` | `tag`, Inline-Editor `plainText`/`richText`, `d4Shortcode`, `moduleClassName`, `moduleOrderClassName`, `settings: content/design/advanced = "auto"` | ⚠️ Struktur weicht ab; offizielle Keys fehlen im Skill |
| `PackageBuildManager::register_package_build('name', Pfad, [... 'enqueue_location' => 'app_window'])` | Argumente laut Tutorial: Name, Script, Dependencies; Flags `enqueue_app_window`/`enqueue_top_window`; Hook dazu offiziell identisch | ⚠️ `enqueue_location` ist nicht belegt; Dependencies `jquery`, `divi-rest` fehlen im Skill |
| Check `function_exists('et_builder_d5_enabled') && et_builder_d5_enabled()` | offiziell `et_core_is_fb_enabled()` UND `et_builder_d5_enabled()` für Builder-Assets | ☑️ Skill prüft nur D5; Frontend-Check sinnvoll, aber nur für Assets relevant |
| `render_callback(array $attrs, $content, $render_slug)` | `render_callback( $attrs, $content, $block, $elements )`, statisch, Ausgabe über `Module::render()` | ⚠️ Signatur abweicht |
| Zugriff `$attrs['titel']['innerContent']['desktop']['value']` | passt zur Attributstruktur | ✅ |
| Eigener Namespace `MeinDiviModul\Modules\...` | Namespaces beliebig, Tutorial `D5TUTSimpleQuickModule` | ✅ unkritisch |
| Imports `ET\Builder\Packages\Module\Options\Element\ElementComponents` | im Tutorial `ElementClassnames`, `Style`, `Module`; `ElementComponents` nicht abgerufen | ☑️ offen, in API-Referenz prüfen |
| `import { ModuleContainer } from '@divi/module'` | passt | ✅ |
| Build: webpack, TSX | Tutorial nutzt webpack + JSX/Babel; TS optional | ✅ ok |
| Skill-Dateistruktur (`modules/...`, `src/components/...`, Traits) | Offiziell `server/` + `visual-builder/src/`; Traits sind Skill-Erfindung bzw. ableitbar aus statischen Methoden `module_styles`, `module_script_data`, `module_classnames`, `render_callback` | ⚠️ Struktur nicht offiziell; als "eigene Variante" kennzeichnen |
| JS: `registerModule` + `addAction('divi.moduleLibrary.registerModuleLibraryStore.after', ...)` | offiziell nötig | ⚠️ im Skill nicht gezeigt (nur Zeilen bis ca. 1120 gelesen) |

Empfehlung: Skill-Abschnitt an das offizielle 10-Minuten-Tutorial anpassen und die Beispiele aus `d5-example-core-modules` als Referenz nennen.

---

## 2. Standardmodule (kurz)

Quelle aller Zeilen: help.elegantthemes.com, Collection "Divi 5 Modules" (https://help.elegantthemes.com/en/collections/10650978-divi-5-modules), pro Modul der Artikel "The X Module in Divi 5". ✅ = so in der Doku. "Eignung" ist teils meine Einordnung (VERMUTET), wo die Doku nur Beispiele nennt.

Gemeinsam bei fast allen Modulen: Content (Inhalt, **Link** macht ganzes Modul klickbar, Background, Loop, Order, Meta), Design (Layout Block/Flex/Grid, Sizing, Spacing, Border, Box Shadow, Filters, Transform, Animation), Advanced (CSS-ID/Klassen, **Attributes**, Custom CSS, **HTML-Tag**, Conditions, Interactions, Visibility, Transitions, Position, Scroll Effects).

| Modul | Wichtigste Einstellungen | Eignung |
|---|---|---|
| Section ✅ | Typen Regular/Fullwidth/Specialty; Layout, Divider, Hintergrund, HTML-Tag | große Seitenbereiche |
| Row ✅ | Spaltenstruktur, Layout Standard/Flexbox/CSS-Grid, ganze Zeile verlinkbar | Spalten, responsive Raster |
| Column | nicht separat abgerufen ☑️ | Inhalte in Row |
| Group ✅ | leichter Container um beliebige Module, Layout Block/Flex/Grid, Link, als Global speicherbar | Karten, gruppierte Blöcke |
| Heading ✅ | Text, Link, HTML-Option (semantisches Tag) in Advanced | Überschriften |
| Text ✅ | Text, Heading/Body-Text-Styles, Link, HTML-Tag | Fließtext, Listen |
| Button ✅ | Text, Link, Button-Styling, Icons, Hover | Aktionen, Downloads, Navigation |
| Image ✅ | Bild aus Mediathek, Link, "Open in Lightbox", Overlay, Filter | Bilder, Lightbox |
| Blurb ✅ | Titel, Text, Bild/Icon, Link, Layout | Leistungen, Features, Schritte |
| Countdown Timer ✅ | Titel, Datum/Uhrzeit, Label-Texte, Styles | Events, Aktionen, Coming Soon |
| Accordion ✅ | Einträge, Toggle-Icon, immer nur einer offen | FAQ, Produktdetails |
| Toggle ✅ | Titel/Text, Start offen oder zu, Icons | einzelne aufklappbare Infos |
| Tabs ✅ | Tab-Einträge, aktiv/inaktiv-Styles; auf Mobil gestapelt | gruppierte Inhalte |
| Call to Action ✅ | Titel, Text, Button, Link | Angebot, Lead |
| Slider ✅ | Slides, Pfeile/Punkte an/aus, Parallax, Video-Hintergrund; Autoplay im Artikel nicht erwähnt | Hero, Slideshow |
| Gallery ✅ | Bilder, Bilder pro Seite, Titel/Caption, Pagination, Grid oder Slider; Lightbox im Artikel nicht erwähnt | Bildersammlungen |
| Menu ✅ | WP-Menü wählen, Logo, Suche/Warenkorb-Icons, Mobile-Menü, Dropdown-Farben | Header/Footer-Navigation |
| Contact Form ✅ | Felder, Titel, Erfolgsmeldung, Submit-Text, Empfänger-E-Mail, Message Pattern, Redirect, Spam-Schutz | Kontaktformular |
| Code ✅ | HTML, CSS (style-Tag), JS (script-Tag), Shortcodes | Drittanbieter-Code, Shortcodes |
| Video ✅ | Datei, YouTube oder Vimeo, Overlay-Bild ("Generate From Video") | eingebettete Videos |
| Icon List ✅ | Einträge mit Icon, Layout, Link | Merkmale, Kontaktdaten |
| Pricing Tables ✅ | Tabellen mit Titel, Untertitel, Preis, Features, Button; hervorheben | Pakete, Preise |
| Testimonial ✅ | Autor, Position, Firma, Text, Foto, Zitat-Icon an/aus | Kundenstimmen |
| Person ✅ (= "Team Member") | Name, Position, Bio, Foto, Social-URLs | Team |
| Social Media Follow ✅ | über 50 Netzwerke, Follow-Button, Link-Ziel | Social-Links |
| Map ✅ | Google Map, Pins mit Titel/Text; braucht Google-Maps-API-Key und Billing | Standort |
| Divider ✅ | sichtbar an/aus, Linienfarbe/-stil/-position | Trennlinie |

⚠️ In Divi 5 heißt das Team-Modul **Person** (nicht "Team Member").
🔎 Weitere Module in Divi 5 (Auswahl): Group Carousel, Hero, Icon, Link, Dropdown, Before/After Image, Timeline, Table of Contents, Breadcrumbs, SVG, Lottie, Chart, Slot, Tooltip, Post-Module (Blog, Portfolio, Post Slider, Post Title, Post Content, Post Filter), Login, Search, Sidebar, Comments, Email Optin, Number-/Circle-/Bar-Counter, Audio. Insgesamt 66 Artikel in der Collection.

---

## 3. Barrierefreiheit in der Doku

- ✅ **HTML-Tag / Element Type:** In Advanced > HTML wählbar, z. B. nav, section, header, article. Layout bleibt gleich. Quelle: https://help.elegantthemes.com/en/articles/13284097-semantic-elements-custom-html-wrappers-for-divi-5
- ✅ **ARIA und eigene Attribute:** Modul wählen > Advanced > Attributes > "Add Attribute". Felder: Admin Label, Target Element (Modul oder Unterelement), Attribute Name, Attribute Value. Dropdown mit häufigen Typen oder "Custom Attribute". Beispiel Icon-Button: `aria-label="Close popup"`, `role="button"`, `tabindex="0"`. Quelle: https://www.elegantthemes.com/blog/divi-resources/how-to-add-aria-attributes-to-modules-in-divi-5 (Blog, nicht Help-Center)
- ✅ **Heading-Level:** laut Blog in den Content-Einstellungen der Heading-Optionsgruppe einstellbar; für Kartentitel unter einem H2 wird H3/H4 empfohlen. Quelle: https://www.elegantthemes.com/blog/divi-resources/how-to-create-looping-semantic-lists-in-divi-5
  ⚠️ Der Help-Artikel zum Heading-Modul sagt zum Level nichts. Er nennt nur die Option "HTML" in Advanced. Genauen Ort im Builder am Live-System prüfen (☑️).
- ✅ **Alt-Text:** Image-Modul kann den Alt-Text aus der WP-Mediathek übernehmen, Überschreiben in Divi möglich; dekorative Bilder leeres alt, dekorative Icons `aria-hidden="true"`. Quelle: https://www.elegantthemes.com/blog/divi-resources/the-ultimate-guide-to-using-images-in-divi-5 (nur über Suchzusammenfassung, Seite nicht selbst abgerufen)
  ⚠️ Der Help-Artikel zum Image-Modul beschreibt kein Alt-Feld.
- ✅ In den abgerufenen Modul-Artikeln steht **keine** eigene Barrierefreiheit-Anleitung (Accordion, Toggle, Tabs, Slider, Menu: Tastatur/Screenreader-Verhalten nicht dokumentiert). Selbst testen.
- 🔎 Hinweise aus den Artikeln (Row, Group, Testimonial, Pricing, CTA): Ganzes Modul als Link nur mit klarem Ziel nutzen und nicht mit Button im selben Modul doppeln. Visibility pro Gerät kann wichtigen Inhalt verstecken.
- ☑️ Help-Artikel "How to Make Your Divi Website More Accessible" (https://help.elegantthemes.com/en/articles/10296543-how-to-make-your-divi-website-more-accessible) nicht abgerufen.

---

## Quellenliste
- https://dev.elegantthemes.com/ , /docs/tutorials/module/beginner/create-simple-quick-module , .../customizing-module , .../module-attributes , .../server-side-rendering-element , /docs/extension-examples , /docs/hooks , /docs/hooks/php/filters/
- https://github.com/elegantthemes/d5-example-core-modules
- https://help.elegantthemes.com/en/collections/10650978-divi-5-modules und die Einzelartikel
- Blog-Artikel (ARIA, Bilder, Looping Lists) siehe oben
