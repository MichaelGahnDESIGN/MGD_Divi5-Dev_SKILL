# Divi 5: Block-Format und programmatische Layouts (Recherche A)

Stand der Recherche: 28.10.2026. Gesucht wurde zuerst bei Elegant Themes (Hilfe-Center, Blog, dev.elegantthemes.com).

## Kurzfazit

- ✅ Divi 5 speichert Inhalte als WordPress-Block-Kommentare mit JSON-Attributen (kein Shortcode mehr).
- ⚠️ Es gibt KEINE offizielle Seite mit vollständigen Markup-Beispielen für section, row, column, heading, button usw. Die offiziellen Developer-Docs beschreiben nur das Prinzip (Breakpoint > State > Value).
- ⚠️ Vollständige Modul-Beispiele gibt es nur aus Drittquellen (Community-Skills). Die Version dort: builderVersion 5.1.1. Diese sind NICHT offiziell belegt.
- ☑️ Ich habe KEINE erfundenen Komplett-Beispiele für section/row/column/blurb/countdown/accordion/cta geschrieben. Sicherster Weg: Modul im Visual Builder bauen, speichern, `post_content` auslesen (siehe Abschnitt "Empfehlung").
- ☑️ Die Versionsangabe "5.18.0" konnte ich nicht prüfen. Belegt ist nur: Divi 5 Launch am 26.02.2026 (Hilfe-Center, Artikel vom 18.09.2026).

---

## 1. Block-Markup

### 🔎 Was offiziell belegt ist

✅ Divi 5 nutzt das "serialized block format" von Gutenberg. Layout-Daten stehen als Block-Kommentare mit JSON-Attributen, z. B. `wp:divi/cta`.
Quelle: https://dev.elegantthemes.com/docs/introducing-divi-5/what-is-divi-5/ (Seite ohne Datum; abgerufen 28.10.2026)

✅ Module werden vom WordPress-Block-Parser gelesen und serverseitig per PHP gerendert. Es wird kein fertiges HTML gespeichert (wegen Presets, globaler Farben, dynamischer Inhalte).
Quellen: https://dev.elegantthemes.com/docs/explanations/module/anatomy-of-module (Stand laut Seite 21.02.2023, evtl. veraltet) und die "What is Divi 5"-Seite oben.

✅ `module.json` eines Moduls ist WordPress' `block.json` plus Divi-eigene Felder. Registrierung per `ModuleRegistration::register_module()`.
Quelle: https://dev.elegantthemes.com/docs/explanations/module/anatomy-of-module

✅ Beginn eines konvertierten Text-Moduls laut offiziellem Migrator-Artikel (Text gekürzt, Rest enthält Hintergrund #E02B20, Textfarbe #FFFFFF und den Absatz):

```
<!-- wp:divi/text {"builderVersion":"4.27.0","modulePreset":"default", ...
```

Quelle: https://help.elegantthemes.com/en/articles/9799364-what-is-the-divi-5-migrator-system
⚠️ Hier steht builderVersion "4.27.0", weil das aus einem Divi-4-Modul konvertiert wurde. Das ist der einzige offizielle Original-Markup-Schnipsel, den ich fand.

### 🔎 Was nur aus Drittquellen kommt (nicht offiziell!)

Quelle: DiviOps-Skill (Community) https://github.com/oaris-dev/diviops (Datei `skills/diviops-divi-5/SKILL.md`; Stand laut Skill: builderVersion 5.1.1; Hover-Gotcha getestet bis Divi 5.10.1). Abruf der Rohdatei per raw-URL gab 404, Inhalt kam über Seiten-Zusammenfassung.

Die Regeln dort (Status: Drittquelle, VERMUTET zuverlässig, der Skill selbst unterscheidet "VB-verified / Verified / UNVERIFIED"):

1. Alles in `divi/placeholder` einwickeln. Zweck: Hülle/Wrapper, damit Divi die Struktur als Layout liest. Offiziell NICHT dokumentiert. (VERMUTET)
2. `builderVersion` an jedem Block (dort: `5.1.1`).
3. Blattmodule (z. B. Text) selbstschließend schreiben, nicht als Öffnen/Schließen-Paar.
4. HTML in `innerContent` mit Unicode escapen (`<` wird `<`).
5. Container (Section, Row, Column, Group): `display: block` über `module.decoration.layout` setzen.
6. Admin-Label unter `module.meta.adminLabel`.
7. `$variable()$`-Token immer mit abschließendem `$`, sonst still kaputt.
8. Kein `var(--eigener-alias)` in Modul-Attributen.
9. Immer Struktur section > row > column, sonst gehen Styles verloren.

Modul-Fallen (ebenfalls Drittquelle):
- Heading: Tag (h1 usw.) explizit setzen (`title.decoration.font.font...headingLevel`).
- Button: Inhalt in `button.innerContent` als Objekt (Text + Link), nicht als String. Button-Styling unter `button.decoration`.
- Blurb: Titel muss Objekt mit Text sein; `useIcon` an, sonst leeres Icon.
- Body-Font: Pfad `content.decoration.bodyFont.body.font` (dreifach verschachtelt).
- Image: Abstände/Größe unter `module.advanced`, nicht `module.decoration`.
- Group-Abstand: `columnGap` und `rowGap`, nicht `gap`.
- Hover: im Breakpoint neben `value` (also `desktop: {value, hover}`), nicht auf oberster Ebene.
- CSS-Klassen: `module.decoration.attributes`. Freies CSS: oberste Ebene, neben `module`.
- Grid-Offsets: `gridOffsetRules` statt `offsetRule/offsetValue`.

⚠️ Eine zweite Drittquelle (Respira-Doku) bestätigt nur: Module sind `divi/*`-Blöcke in `post_content`; globale Module werden als Referenzblock `divi/global-layout` gespeichert; die Element-ID heißt `_nodeId`.
https://www.respira.press/docs/builders/divi

### ☑️ Beispiele nach Modul (BELEGT / NICHT BELEGT)

| Modul | Vollständiges Beispiel offiziell belegt? |
|---|---|
| text | Nur Anfang (siehe oben), Rest nicht abgedruckt |
| cta | Nur Blockname `wp:divi/cta` erwähnt |
| section, row, column, group, heading, button, image, blurb, countdown-timer, accordion | ☑️ NEIN, kein offizielles Voll-Beispiel gefunden |

Ich habe bewusst keine Beispiele ausgedacht. Siehe "Empfehlung".

---

## 2. Hintergrund, Abstände, Typografie, Responsive, Hover

✅ Offiziell (dev.elegantthemes.com): Attribute sind standardmäßig mehrstufig. Baum: Element > Element-Teil (z. B. `decoration`) > Option (z. B. `spacing`) > Breakpoint > State > Wert.
- Breakpoints: `desktop`, `tablet`, `phone`.
- States: `value` (Normalzustand), `hover`, `sticky`.
- Unter `decoration` sind die Option-Keys fest (u. a. spacing, sizing, border, background, sticky).
- Hover/Sticky auf Tablet/Phone: Format erlaubt es, die Doku sagt aber, es brauche noch Anpassung/Tests.

Quellen:
- https://dev.elegantthemes.com/docs/explanations/module/attribute-format/ (Stand laut Seite: 24.12.2022, evtl. veraltet)
- https://dev.elegantthemes.com/docs/introducing-divi-5/what-is-divi-5/

✅ Offizielles Beispiel (JS-Form, gleiche Logik wie im JSON):

```js
// Breite mit Hover/Sticky + Tablet-Override
const width = {
  desktop: { value: '40px', hover: '42px', sticky: '44px' },
  tablet:  { value: '30px' },
}

// Objektwerte: Unterschlüssel in value
const boxShadow = {
  desktop: { value: { style: 'preset1', horizontal: '3px', color: '#960000' } },
}
```

⚠️ Widerspruch zwischen Offiziell und Drittquelle bei Hover: Offiziell ist `desktop: { value, hover }` (hover als Geschwister von value). Die Drittquelle sagt dasselbe ("neben value"). Passt also zusammen.

☑️ Die konkreten Pfade für Hintergrundfarbe (z. B. `module.decoration.background...`), Abstände (`module.decoration.spacing.desktop.value.padding...`) und Typografie pro Modul sind offiziell nur als Prinzip belegt, nicht als Liste. Genaue Schlüssel (z. B. `top`, `bottom`, `syncVertical`) NICHT belegt. Die Seiten "Module Attributes" (https://dev.elegantthemes.com/docs/tutorials/module/beginner/module-attributes/) und "Layout Style" bzw. "Overflow Style" unter `/docs/explanations/module/styles/style-components/` sind die nächsten Lesetipps (nicht von mir geöffnet).

---

## 3. Design-Variablen und Presets

### Offiziell

✅ Presets: Export/Import über Preset Manager (Icon Import/Export), Datei = JSON, enthält nur Preset-Definitionen, keine Layouts/Seiten/Templates. Import benötigt Divi 5 Public Beta 7 oder neuer. Variablen, die von Presets genutzt werden, kamen beim Import des Artikel-Tests mit.
Quelle: https://www.elegantthemes.com/blog/divi-resources/how-import-export-presets-in-divi-5 (22.02.2026)

✅ Design-Variablen: Export/Import über Variable Manager, alle Variablen in einer JSON-Datei, Snapshot. Sechs Typen: Farben, Schriften, Zahlen, Bilder, Text, Links. Anwenden über Variablen-Auswahl im Feld (Dynamic-Content-Icon). Änderung der Variable wirkt überall.
Quellen: https://www.elegantthemes.com/blog/divi-resources/how-to-import-export-design-variables-in-divi-5 (21.02.2026) und https://help.elegantthemes.com/en/articles/13348842-global-variables-in-divi-5

✅ Empfohlene Import-Reihenfolge auf neuer Seite: Presets, dann globale Variablen, dann Layouts, dann Theme-Builder-Templates.
Quelle: https://www.elegantthemes.com/blog/divi-resources/divi-5-launch-gift-design-system

☑️ Beide Artikel sagen ausdrücklich NICHT, wie die Referenzen im JSON bzw. Markup gespeichert werden.

### Drittquelle (nicht offiziell, VERMUTET)

- Variablen im Markup: `$variable({...JSON-Payload...})$` mit zwingendem schließenden `$`. IDs oft `gcid-…` (Farben) und `gvid-…` (andere), von Divi selbst erzeugte können auch UUID-artig sein.
- Presets: per UUID, als `modulePreset: [uuid]` oder `groupPreset.<slot>.presetId`.
- Warnung der Quelle: Ein vom Runtime akzeptiertes Format kann der Visual Builder beim nächsten Speichern umschreiben. Deshalb im Builder speichern und Markup gegenprüfen.
Quelle: https://www.claudepluginhub.com/skills/oaris-dev-divi-5-builder/divi-5-builder (Zusammenfassung über Websuche; direkter Abruf gab "Seite nicht gefunden") und https://github.com/oaris-dev/diviops

Beobachtung: Offizielles Migrator-Beispiel zeigt `"modulePreset":"default"` als String, die Drittquelle spricht von UUID-Arrays. ☑️ Unklar, ob beides gültig ist.

---

## 4. Divi 4 Shortcodes vs. Divi 5 Blöcke, Konvertierung

✅ Divi 5 nutzt keine Shortcodes mehr. Der Migrator (Divi > Divi 5 Migrator) scannt die Seite, konvertiert unterstützte Module in Blöcke, aktualisiert jeden Beitrag. Nicht unterstützte Module werden in Shortcodes verpackt und laufen im Divi-4-Framework weiter (Backward-Compatibility-Modus). Eine einzige Altlast-Modul-Seite lädt dann das Divi-4-Framework (Performance).
Quellen: https://help.elegantthemes.com/en/articles/9799364-what-is-the-divi-5-migrator-system und https://help.elegantthemes.com/en/articles/12767407-how-to-safely-migrate-from-divi-4-to-divi-5 (18.09.2026)

⚠️ WICHTIG: Öffnet man eine Divi-4-Seite im Divi-5-Builder, BEVOR der Migrator lief, wird sie sofort konvertiert, ohne Rollback. Der Migrator legt dagegen eine Sicherheitskopie an ("Restore Divi 4 Content").
Quelle: https://help.elegantthemes.com/en/articles/12767407-how-to-safely-migrate-from-divi-4-to-divi-5

✅ Divi-5-Start: 26.02.2026 (gleiche Quelle).

✅ Es gibt Dev-Doku-Kategorie "Converting Divi 4 Module to Divi 5" (Entwickler-Tutorial für eigene Module), nicht geöffnet: https://dev.elegantthemes.com/docs/intro

Elementor: ☑️ Offiziell von Elegant Themes kein Elementor-Import gefunden. Drittanbieter-Plugin vorhanden: "JHMG Converter For Elementor to Divi 5" (WordPress.org, schreibt Divi-5-Blöcke; Kit-ZIP erst in Pro-Add-on). Aussage stammt aus der Plugin-Beschreibung, nicht von mir getestet. https://it.wordpress.org/plugins/?p=225883

---

## 5. Layout Import/Export (JSON)

✅ Divi Library > Import & Export > Export-Tab, Dateiname, "Download Export" = JSON. Import-Tab, Datei wählen, "Import Divi Builder Layouts". Die Datei muss aus der Divi Library stammen. Theme-Builder-Templates werden separat unter Divi > Theme Builder importiert (Option "Import Presets" anhaken).
Quelle: https://help.elegantthemes.com/en/articles/13616078-divi-library-in-divi-5 (04.02.2026)

☑️ Der Artikel sagt NICHT, ob Presets/Variablen in der Layout-Datei stehen, und nennt keine Versionsanforderung. Die interne JSON-Struktur (Schlüssel) ist für Layouts, Presets und Variablen offiziell nirgends beschrieben.

---

## Empfehlung für den programmatischen Weg

1. ✅ Mini-Layout im Divi-5-Visual-Builder bauen (section, row, column, je ein Modul), speichern.
2. Gespeicherten `post_content` auslesen (z. B. WP-CLI `wp post get <ID> --field=post_content` oder REST `context=edit`). Das ist die einzige verlässliche Vorlage für die genaue Version.
3. Daraus Templates ableiten, nur Werte ersetzen. Danach wieder im Builder öffnen und speichern, prüfen, dass nichts umgeschrieben wird.
4. Presets/Variablen als JSON aus Preset Manager / Variable Manager exportieren und die Dateien im Texteditor ansehen, um die echten Schlüssel zu lernen.
5. Nächste offizielle Lesequellen (nicht geöffnet): https://dev.elegantthemes.com/api/ (PHP API), https://dev.elegantthemes.com/docs/hooks, https://dev.elegantthemes.com/docs/tutorials/module/beginner/module-attributes/.

## Quellenübersicht

Offiziell: dev.elegantthemes.com (what-is-divi-5, attribute-format, anatomy-of-module), help.elegantthemes.com (Artikel 9799364, 12767407, 13616078, 13348842), elegantthemes.com/blog (Presets- und Variablen-Export).
Drittquellen: github.com/oaris-dev/diviops, claudepluginhub.com (divi-5-builder), respira.press, wordpress.org JHMG-Plugin.
