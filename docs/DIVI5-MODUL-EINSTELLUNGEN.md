# Divi 5.18 – Katalog aller Modul-Einstellungen

Quelle: lokales Block-Schema `dev-export-20261028-b/divi-bloecke.json` (113 Blöcke, Divi 5.18.0). Nur gelesen, nichts geändert.
Erzeugt am 28.10.2026 per Skript (Pfade, Labels, Feldtypen, Werte-Listen stammen direkt aus dem Schema).

## 0. So liest du diese Datei

- ✅✅ = in echten gespeicherten Seitendaten gesehen (`divi5-referenz-20261028.md`, Seite "Referenz Module").
- ✅ = steht im Schema (Pfad, Feldname, Auswahlwerte, Grenzen).
- ⚠️ = Annahme aus Divi-5-Wissen. Im Schema steht nur, DASS es die Einstellung gibt, nicht die genaue Form des Wertes. Vor dem Massen-Einsatz einmal im Builder testen und mit "Code ansehen" gegenprüfen.
- Das Schema kennt KEINE Eltern-Kind-Regeln (`parent`/`ancestor` sind überall leer). Die Hierarchie unten ist aus Namen und Referenzseite abgeleitet.
- Labels sind die englischen Schema-Labels. Das deutsche Divi nennt manches anders (Blurb = Informationstafel, CTA = Handlungsaufforderung).

## 1. Grundregeln fürs Speichern (gilt für alle Module)

1. Aufbau eines Wertes: `Attribut > Bereich > Option > Bildschirm > Zustand > Wert`. Beispiel: `title.decoration.font.font.desktop.value.color`.
   - Attribut = Teil des Moduls (`module`, `title`, `content`, `button`, `image` ...). Jedes Modul hat mehrere solcher Teile. `module` ist immer die äußere Hülle.
   - Bereich = `innerContent` (Inhalt), `advanced` (Optionen/Verhalten), `decoration` (Gestaltung), `meta` (Admin-Label).
   - Bildschirm = `desktop`, `tablet`, `phone` ✅✅ (`phoneWide` kommt in echten Daten vor; im Schema auch `tabletWide`). Zustand = `value`, daneben `hover` und `sticky` ✅.
2. Divi speichert NUR Werte, die vom Standard abweichen ✅✅. Leere Gruppen weglassen.
3. `attrName` im Schema (z. B. `button.innerContent`) ist der Pfad OHNE `.desktop.value`. Hat ein Eintrag zusätzlich `subName` (z. B. `text`), dann gilt `attrName.desktop.value.subName` ✅✅ (`button.innerContent.desktop.value.text`).
4. Die Pfade in den Tabellen unten sind schon so zusammengesetzt (`attrName` + `.desktop.value.` + `subName`). Bei Gruppen-Einträgen (Typ font, spacing, border ...) kommt der Pfad der Gruppe, danach die Form aus Abschnitt 3.
5. Ein Feld mit `kein Hover`/`nicht responsiv` im Schema kennt keinen `hover`/`tablet`/`phone`-Wert. Dann nur `desktop.value`.
6. Toggles sind Text: `"on"` / `"off"` ✅✅ (`open: on`, `target: off`), niemals true/false.
7. Zahlen mit Einheit sind Text: `"24px"`, `"1.4em"`, `"50%"` ⚠️ (Schema: `defaultUnit` px/%/em je Feld).
8. Farben: `"#0e0f25"` (Divi schreibt Hex klein ✅✅), `rgba(...)` ⚠️, oder Variable `$variable({"type":"color","value":{"name":"gcid-primary-color","settings":{}}})$` ✅ (steht so im Menü-Schema als Standard).
9. HTML-Texte (richtext): `"<p>Text</p>"`. Im Blockkommentar werden `<`, `>`, `&` als `<`, `>`, `&` geschrieben ✅✅.
10. Hover eines Wertes: neben `value` im selben Bildschirm: `desktop: {value: "#000", hover: "#fff"}` ✅ (offizielle Doku, siehe A-blockformat).
11. Jeder Block braucht `"builderVersion":"5.18.0"` auf oberster Ebene ✅✅. Module ohne Kinder enden mit `/-->`.
12. Hierarchie (✅✅ Referenzseite): `placeholder > section > row > column > Modul`. Kinder: accordion > accordion-item, icon-list > icon-list-item, tabs > tab, slider > slide, pricing-tables > pricing-table, contact-form > contact-field, counters > counter, social-media-follow > social-media-follow-network, video-slider > video-slider-item, map > map-pin, signup > signup-custom-field, post-filter > post-filter-item, timeline > timeline-item. `row-inner`/`column-inner` = verschachtelte Zeile/Spalte (innerhalb einer Spalte). `group` darf geschachtelt werden ✅✅.

## 2. Gemeinsame Gruppen (`module.*`) – einmal erklärt

Die Tabelle gilt für JEDES Modul, das die Gruppe hat. Welche Gruppen ein Modul NICHT hat, steht bei den Modulen unter "ohne:". Tab-Zuordnung ✅ aus den `groupSlug`-Namen des Schemas (content/design/advanced), deutsche Bezeichnungen sind meine Übersetzung.

| Gruppe (Pfad ab `module.`) | Tab | Was es ist | Form des Wertes (unter `.desktop.value`) |
|---|---|---|---|
| `meta.adminLabel` | – | Name im Builder-Ebenenbaum | direkt String: `"Section"` ✅✅ |
| `decoration.background` | Inhalt ✅ | Hintergrund | `{color:"#hex", gradient:{...}, image:{...}}`. `color` ✅✅. gradient/image/video/mask/pattern ⚠️: `gradient:{enabled:"on",type:"linear",direction:"180deg",stops:[{position:"0",color:"#a"},{position:"100",color:"#b"}]}`, `image:{url:"...",size:"cover",position:"center",repeat:"no-repeat"}` |
| `decoration.spacing` | Design ✅ | Außen-/Innenabstand | `{margin:{top,right,bottom,left}, padding:{top,right,bottom,left}}` mit Texten wie `"20px"` ⚠️. Zusätzlich Sync-Schalter `syncVertical`/`syncHorizontal` mit `"on"/"off"` ⚠️. CSS-Namen im Schema: margin/padding (-top/-right/-bottom/-left) ✅ |
| `decoration.sizing` | Design ✅ | Breite/Höhe/Flex | Felder ✅: `width, maxWidth, minWidth, height, minHeight, maxHeight, alignment, alignSelf, flexType, size`. `flexType:"12_24"` (Spaltenbreite in 24stel) ✅✅. Weitere Grid-Felder `gridAlignSelf, gridJustifySelf` ✅. Zahlen als Text mit Einheit ⚠️ |
| `decoration.layout` | Design ✅ | Anordnung der Kinder | Felder ✅: `display` (`block`/`flex`/`grid`), `flexDirection` (`row`/`column`), `flexWrap` (`nowrap`/`wrap` ✅✅), `justifyContent`, `alignItems`, `alignContent`, `columnGap`, `rowGap`, `gridColumnCount` (Text `"3"`), `gridTemplateColumns`, `gridAutoFlow`, `gridRowCount` u. a. Beispiel Schema-Standard: `{flexDirection:"column",columnGap:"30px",rowGap:"30px"}` ✅ |
| `decoration.border` | Design ✅ | Rahmen + Rundung | Felder ✅: `radius`, `styles`. ⚠️ `radius:{sync:"on",topLeft:"8px",topRight:"8px",bottomRight:"8px",bottomLeft:"8px"}`, `styles:{all:{width:"1px",style:"solid",color:"#ccc"}}` (auch `top/right/bottom/left`). CSS ✅: border-radius, border-style, border-width, border-color |
| `decoration.boxShadow` | Design ✅ | Schatten | ✅ offiziell: `{style:"preset1", horizontal:"3px", color:"#960000"}`. Weitere ⚠️: `vertical, blur, spread, position ("outer"/"inner")`. Schema-Felder: `style`, `position` |
| `decoration.filters` | Design | CSS-Filter, Mischmodus | Feld `blendMode` ✅. Rest (hue, saturate, brightness, contrast, invert, sepia, opacity, blur) ⚠️ |
| `decoration.transform` | Design | Skalieren/Verschieben/Drehen | ⚠️ `scale, translate, rotate, skew, origin` |
| `decoration.animation` | Design ✅ | Einblend-Animation beim Scrollen | ⚠️ `style` (fade, slide, bounce, zoom, flip, fold, roll), `direction`, `duration:"1000ms"`, `delay`, `intensity`, `repeat`, `speedCurve`, `startingOpacity` |
| `decoration.transition` | Erweitert | Hover-Übergang | ⚠️ `duration, delay, speedCurve`. Schema: `transition-duration` ✅ |
| `decoration.position` | Erweitert | Positionierung | ⚠️ `{type:"absolute", origin:..., offset:{vertical, horizontal}}`. Schema-CSS: `position` ✅ |
| `decoration.zIndex` | Erweitert | Ebenen-Reihenfolge | ⚠️ einfacher Wert `"10"` |
| `decoration.order` | Design | Reihenfolge in Flex/Grid | ⚠️ Zahl als Text (CSS `order` ✅) |
| `decoration.overflow` | Erweitert ✅ (advancedVisibility) | Überlauf sichtbar/versteckt | ⚠️ `{x:"hidden",y:"hidden"}` |
| `decoration.disabledOn` | Erweitert ✅ | Auf Geräten ausblenden | ⚠️ pro Gerät `"on"/"off"` (desktop/tablet/phone) |
| `decoration.conditions` | Erweitert | Anzeige-Bedingungen | ⚠️ Liste von Regeln |
| `decoration.scroll` | Erweitert ✅ | Scroll-Effekte | Feld `gridMotion` ✅; Rest ⚠️ |
| `decoration.sticky` | Erweitert ✅ | Haftend beim Scrollen | ⚠️ Position/Abstände |
| `decoration.attributes` | Erweitert ✅ | HTML-Attribute (id, class, data-*) | ⚠️ Liste aus `{name, value}` |
| `decoration.interactions` | Erweitert | Klick/Hover-Interaktionen | ⚠️ |
| `advanced.link` | Inhalt ✅ | Ganzes Modul als Link | ⚠️ `{url, target}` |
| `advanced.html` | Erweitert | HTML-Tag ändern | Feld `trailAdvancedHtmltag` ✅; Form ⚠️ |
| `advanced.loop` | Erweitert | Loop-Ausgabe (Posts) | ⚠️ |
| `advanced.elements` | Inhalt ✅ | Elemente ein/aus (je Modul anders) | ⚠️ |
| `advanced.text` | Design ✅ | Textfarbe hell/dunkel, Ausrichtung, Textschatten | Felder ✅: `color`, `orientation`, `textShadowGroup`. ⚠️ `module.advanced.text.text.desktop.value.{color:"light", orientation:"center"}` |

Nur im Builder-JSON, nicht als Modul-Gruppe: freie CSS-Klasse und ID liegen laut Schema oben als `className`-Attribut (Typ `object`, keine Details) ⚠️.

## 3. Wertformen der Element-Gruppen (title, content, button, icon, image ...)

Diese Gruppen hängen an einem Modul-Teil: `<teil>.decoration.<gruppe>`. Im Schema sind sie als Gruppen-Typ (`component.name`) eingetragen.

| Gruppen-Typ | Typischer Pfad | Form |
|---|---|---|
| `font` | `title.decoration.font.font.desktop.value.<key>` ✅ (Schema-Pfade wie `openToggle.decoration.font.font.desktop.value.color`) | Schlüssel ✅ aus Schema: `color, size, weight, lineHeight, letterSpacing, textAlign, family, style, headingLevel, textShadowGroup`. Werte ⚠️: `color:"#fff"`, `size:"32px"`, `weight:"700"`, `lineHeight:"1.3em"`, `letterSpacing:"1px"`, `textAlign:"center"`, `headingLevel:"h2"` ✅✅, `family:"Roboto"`, `style:["italic","uppercase"]` (Liste ⚠️) |
| `font-body` (bodyFont) | `content.decoration.bodyFont.body.font.desktop.value.<key>` ⚠️ | Unterteile ✅: `body`, `link`, `ul`, `ol`, `quote`, `textAlign`. Link: `bodyFont.link.font...`; Listen: `bodyFont.ul.list...` ✅ Schema-Selektoren. Gleiche font-Schlüssel wie oben |
| `headingFont` | `content.decoration.headingFont.h1.font...` (h1 bis h6) ✅ Schema-Selektoren | im Text-Modul für Überschriften im Fließtext |
| `button` | `button.decoration.button.desktop.value...` ⚠️ | Button-Stil-Gruppe. Schema-Unterfelder ✅: `alignment, fontGroup, spacingGroup, borderGroup, backgroundGroup, sizingGroup, boxShadowGroup, buttonIconGroup (settings, placement, onHover)`. Praktisch: Farbe/Schrift/Rahmen des Buttons liegen in den Geschwistern `button.decoration.background`, `.font`, `.border`, `.spacing`, `.sizing`, `.boxShadow` (siehe Button-Modul) ⚠️ |
| `icon` | `<teil>.decoration.icon.desktop.value` | Felder ✅: `icon, color, useSize, size`. Icon-Objekt ✅✅: `{unicode:"&#x21;", type:"divi", weight:"400"}` |
| `image` | `image.decoration.image...` | ✅ Feld `sizingGroup`; Rest ⚠️ |
| `fit` | `image.decoration.fit` | ⚠️ Anpassung des Bildes |

## 4. Feldtypen (`component.name`) und wie der Wert aussieht

| Typ | Wert |
|---|---|
| `toggle` | `"on"` / `"off"` ✅✅ |
| `text` | String. Bei Titeln direkt String (`title.innerContent.desktop.value`), bei Blurb/CTA-Buttons ein Objekt mit `text` ✅✅ |
| `richtext` | HTML-String `"<p>..</p>"` ✅✅ |
| `color-picker` | Hex-String oder `$variable(...)$` |
| `select` / `button-options` | einer der Schlüssel aus der Werte-Liste (Spalte "Werte"), z. B. `left/center/right` |
| `range` | String mit Einheit (`defaultUnit`), Grenzen `min`/`max` im Schema |
| `upload` | Objekt-Teil `src` (URL) ✅✅ (`image.innerContent.desktop.value.src`); weitere Teile: `alt`, `linkUrl`, `linkTarget` ✅ Schema |
| `icon-picker` | Objekt `{unicode, type, weight}` ✅✅ |
| `timepicker` | `"2026-11-27 07:57"` ✅✅ (Datum Uhrzeit, ohne Sekunden) |
| `button-link` | im selben Objekt wie der Button-Text: `button.innerContent.desktop.value.{text, linkUrl, linkTarget}` ✅ Schema; `linkUrl` ✅ in Michaels Baukasten, `linkTarget:"off"/"on"` ⚠️ (neues Fenster = `"on"`) |
| `link` | wie button-link, an Icon/Bild-Modul ⚠️ |
| `composite`, `checkboxes`, `sortable-list`, `conditions`, `table-editor`, `code`, `map`, `textarea`, `upload-gallery`, `border-radius` | Spezialformen, genaue Struktur ⚠️ nicht im Schema |

## 5. Fallstricke für Skripte

- `title.innerContent` ist beim Heading ein String, beim Blurb `{text:"..."}` ✅✅. Schema-Hinweis: wo `subName:"text"` steht, ist es ein Objekt.
- `children.*`-Pfade (z. B. im Slider) sind Voreinstellungen für die Kind-Module (Slides) ⚠️. Zum Befüllen lieber direkt am Kind speichern.
- Unbekannte Gruppen NICHT erfinden: Was nicht in der Tabelle des Moduls steht, gibt es dort nicht ("ohne:").
- Der Button hat KEINE eigene `module.decoration.background`/`border`/`font`. Alles Optische liegt unter `button.decoration.*`.


## 6. Wichtige Module im Detail

Legende pro Zeile: `Pfad` — Label [Feldtyp; Auswahlwerte/Grenzen; Std = Standardwert im Schema; Felder +x = Feld sichtbar, -x = versteckt; Tab]. "Std font" = leere Gruppe im Schema: es gibt sie mit allen Standardfeldern. "ohne" = gemeinsame Gruppen aus Abschnitt 2, die dieses Modul NICHT hat. Beim Typ `font` etc. kommt die Form aus Abschnitt 3.

### divi/section – Section
Sektion: oberstes Band der Seite, enthält Zeilen.

- Sektions-Hintergrund: `module.decoration.background.desktop.value.color` ✅✅. Neue Sektionen haben meist `layout.display:"block"` ✅✅ (alte Importe) bzw. Flex.
- `column1/2/3.decoration.background/spacing` sind Altlasten für die Hintergründe der ersten drei Spalten ⚠️. `innerSizing...` = Breite des Inhaltsbereichs (`width` %, `maxWidth` px, `alignment`).
- `module.advanced.dividers` = Formtrenner oben/unten, `innerShadow` = Innenschatten.

- `module.advanced.innerShadow` — Show Inner Shadow [on/off]
- `module.advanced.dividers` [dividers]
- `module.advanced.gutter` [gutter]
- `column1.decoration.background` — Column 1 [background]
- `column1.decoration.spacing` — Column 1 [spacing; -margin]
- `column2.decoration.background` — Column 2 [background]
- `column2.decoration.spacing` — Column 2 [spacing; -margin]
- `column3.decoration.background` — Column 3 [background]
- `column3.decoration.spacing` — Column 3 [spacing; -margin]
- `innerSizing.decoration.sizing.desktop.value.width` — Inner Width [Zahl; max 100; defaultUnit %]
- `innerSizing.decoration.sizing.desktop.value.maxWidth` — Inner Max Width [Zahl; max 1080; defaultUnit px]
- `innerSizing.decoration.sizing.desktop.value.alignment` — Row Alignment [Wahl; left/center/right]
- ohne: –

Beispiel ✅✅ (echte Referenzdaten):
```
<!-- wp:divi/section {"module":{"decoration":{"background":{"desktop":{"value":{"color":"#0e0f25"}}}}},"builderVersion":"5.18.0"} -->
```

### divi/row – Row
Zeile: liegt in einer Sektion, enthält Spalten.

- `columnStructure` (`"1_2,1_2"`, `"4_4"`, `"1_3,1_3,1_3"`) und `flexColumnStructure` (`"equal-columns_2"`) stehen ✅✅ in echten Daten, aber NICHT im Schema (Builder-intern). Sie müssen zur Zahl der Spalten passen.
- Mobil umbrechen: `layout.phone.value.flexWrap:"wrap"` ✅✅.
- Zeilen-Hintergrund/Abstand sind normale Gruppen (`module.decoration.background/spacing`), siehe Abschnitt 2.

- `module.advanced.gutter` [gutter]
- ohne: –

Beispiel ✅✅ (echte Referenzdaten):
```
<!-- wp:divi/row {"module":{"advanced":{"columnStructure":{"desktop":{"value":"1_2,1_2"}},"flexColumnStructure":{"desktop":{"value":"equal-columns_2"}}},"decoration":{"layout":{"desktop":{"value":{"flexWrap":"nowrap"}},"phone":{"value":{"flexWrap":"wrap"}}}}},"builderVersion":"5.18.0"} -->
```

### divi/column – Column
Spalte: liegt in einer Zeile, enthält Module.

- `module.advanced.type` = Breitentyp (`"4_4"`, `"1_2"`, `"1_3"` ...) ✅✅, `sizing.flexType` = Flex-Breite in 24stel (`"24_24"` voll, `"12_24"` halb, `"8_24"` Drittel, `"6_24"` Viertel) ✅✅. Beides gleichzeitig setzen.
- Im Schema steht für `type` kein Eintrag: Builder-intern.

- ohne: –

Beispiel ✅✅ (echte Referenzdaten):
```
<!-- wp:divi/column {"module":{"advanced":{"type":{"desktop":{"value":"1_2"}}},"decoration":{"sizing":{"desktop":{"value":{"flexType":"12_24"}},"phone":{"value":{"flexType":"24_24"}}}}},"builderVersion":"5.18.0"} -->
```

### divi/group – Group
Gruppe: Container für mehrere Module (Flex/Grid), darf geschachtelt werden.

- Eigenes Layout (`display:"flex"/"grid"`, Gaps) in `module.decoration.layout` ⚠️. Hat KEINE Inhaltsfelder, nur Gruppen aus Abschnitt 2.

- ohne: –

### divi/heading – Heading
Überschrift H1 bis H6.

- Text ist ein String ✅✅. Schriftgröße/Farbe/Ebene: `title.decoration.font.font.desktop.value.*` (`headingLevel` ist am Schema als sichtbares Feld ✅).

- `title.innerContent` — Heading [Text]
- `title.decoration.font` — Heading [font; +headingLevel]
- ohne: –

Beispiel ⚠️ (Form aus Schema + Baukasten, nicht aus echten Daten):
```
<!-- wp:divi/heading {"title":{"innerContent":{"desktop":{"value":"Titel"}},"decoration":{"font":{"font":{"desktop":{"value":{"headingLevel":"h2","color":"#ffffff","size":"40px","weight":"700"}}}}}},"builderVersion":"5.18.0"} /-->
```

### divi/text – Text
Fließtext (HTML).

- Fließtext: HTML. Schrift: `content.decoration.bodyFont.body.font.desktop.value.*` ⚠️; Links `...bodyFont.link.font`, Listen `...bodyFont.ul`/`ol`, Zitat `...quote`; Überschriften im Text `headingFont.h1..h6` ✅.

- `content.innerContent` — Body [HTML]
- `content.decoration.headingFont` [Std headingFont]
- `content.decoration.bodyFont` [font-body]
- ohne: –

Beispiel ✅✅ (echte Referenzdaten):
```
<!-- wp:divi/text {"content":{"innerContent":{"desktop":{"value":"<p>Text</p>"}}},"builderVersion":"5.18.0"} /-->
```

### divi/button – Button
Einzelner Button mit Link.

- Text + Link im SELBEN Objekt: `button.innerContent.desktop.value.{text,linkUrl,linkTarget}`.
- Farbe Hintergrund: `button.decoration.background.desktop.value.color`; Textfarbe/-größe: `button.decoration.font.font.desktop.value.*` ⚠️ (so benutzt es Michaels Baukasten).
- Ausrichtung des Buttons: `module.advanced.alignment` (left/center/right) ✅. Abstände des Buttons selbst sind versteckt (`-margin -padding`), Außenabstand über `module.decoration.spacing`.

- `module.advanced.alignment` — Button Alignment [Wahl; left/center/right]
- `button.innerContent.desktop.value.text` — Button Text [Text]
- `button.innerContent` — Button [button-link]
- `button.decoration.{background,border,boxShadow}` [Std-Gruppen]
- `button.decoration.button` [Std button; -alignment -boxShadowGroup +fontGroup.lineHeight -fontGroup.textAlign -spacingGroup]
- `button.decoration.{font,sizing}` [Std-Gruppen]
- `button.decoration.spacing` [Std spacing; -margin -padding]
- ohne: background, border, sizing

Beispiel ⚠️ (Form aus Schema + Baukasten, nicht aus echten Daten):
```
<!-- wp:divi/button {"button":{"innerContent":{"desktop":{"value":{"text":"Hier Klicken","linkUrl":"https://example.org"}}},"decoration":{"background":{"desktop":{"value":{"color":"#D9076D"}}},"font":{"font":{"desktop":{"value":{"color":"#FFFFFF","weight":"600"}}}}}},"builderVersion":"5.18.0"} /-->
```

### divi/image – Image
Einzelnes Bild mit optionalem Link/Lightbox.

- `src` ist Pflicht. Link: `linkUrl`, `linkTarget` (off/on). Lightbox: `image.advanced.lightbox` (on/off).
- Rundung/Schatten: `image.decoration.border`/`boxShadow` (NICHT module). Ausrichtung: `module.advanced.align`.

- `module.advanced.align` — Image Alignment [Wahl; left/center/right]
- `module.advanced.sizing.desktop.value.forceFullwidth` — Force Fullwidth [on/off]
- `module.advanced.sizing` [sizing]
- `module.advanced.spacing.desktop.value.showBottomSpace` — Show Space Below The Image [on/off]
- `module.advanced.spacing` [spacing]
- `image.innerContent.desktop.value.src` — Image [Upload]
- `image.innerContent.desktop.value.linkUrl` — Image Link URL [Text]
- `image.innerContent.desktop.value.linkTarget` — Image Link Target [Wahl; off/on]
- `image.advanced.lightbox` — Open in Lightbox [on/off]
- `image.advanced.overlay.desktop.value.use` — Image Overlay [on/off]
- `image.advanced.overlay.desktop.value.backgroundColor` — Hover Overlay Color [Farbe]
- `image.advanced.overlayIcon.desktop.value.hoverIcon` — Hover Icon Picker [Icon]
- `image.advanced.overlayIcon.desktop.value.iconColor` — Overlay Icon Color [Farbe]
- `image.decoration.{fit,border,boxShadow}` [Std-Gruppen]
- ohne: border, boxShadow, sizing, spacing

Beispiel ⚠️ (Form aus Schema + Baukasten, nicht aus echten Daten):
```
<!-- wp:divi/image {"image":{"innerContent":{"desktop":{"value":{"src":"https://example.org/bild.jpg"}}}},"builderVersion":"5.18.0"} /-->
```

### divi/blurb – Blurb
Informationstafel: Icon oder Bild + Titel + Text.

- Titel + Link als Objekt `title.innerContent.desktop.value.{text,...}` ✅✅. Bild: `imageIcon.innerContent.desktop.value.{useIcon,icon,src}`; `useIcon:"on"` = Icon statt Bild.
- `imageIcon.advanced.placement` top/left. Schrift: `title.decoration.font`, `content.decoration.bodyFont` (Standardgruppen, nicht einzeln aufgelistet = vorhanden).

- `imageIcon.innerContent.desktop.value.useIcon` — Use Icon [on/off]
- `imageIcon.innerContent.desktop.value.icon` — Icon [Icon]
- `imageIcon.innerContent.desktop.value.src` — Image [Upload]
- `imageIcon.advanced.color` — Icon Color [Farbe]
- `imageIcon.advanced.placement` — Image/Icon Placement [Wahl; top/left]
- `imageIcon.decoration.background` — Image/Icon [background]
- `imageIcon.decoration.spacing` — Image/Icon [spacing]
- `imageIcon.decoration.animation` — Image/Icon [animation]
- `title.innerContent` [Std innerContent]
- `title.decoration.font` [Std font]
- `content.innerContent` [Std innerContent]
- `content.decoration.bodyFont` [Std bodyFont]
- `contentContainer.decoration.sizing.desktop.value.maxWidth` — Content Width [Zahl; max 1100]
- ohne: –

Beispiel ✅✅ (echte Referenzdaten):
```
<!-- wp:divi/blurb {"imageIcon":{"innerContent":{"desktop":{"value":{"src":"https://example.org/bild.jpg"}}}},"title":{"innerContent":{"desktop":{"value":{"text":"Titel"}}}},"content":{"innerContent":{"desktop":{"value":"<p>Text</p>"}}},"builderVersion":"5.18.0"} /-->
```

### divi/countdown-timer – Countdown Timer
Countdown bis zu einem Datum.

- Datum: `content.advanced.dateTime.desktop.value` Format `YYYY-MM-DD HH:MM` ✅✅, nicht responsiv, kein Hover.
- Schrift getrennt für Titel, Zahlen (`number`), Trenner (`separator`), Beschriftung (`label`).

- `title.innerContent` — Title [Text]
- `title.decoration.font` — Title [font; +headingLevel]
- `content.advanced.dateTime` — Date [timepicker; Std "2020-03-23 01:30"]
- `number.decoration.font` — Numbers [font]
- `separator.decoration.font` — Separator [font; -textAlign]
- `label.decoration.font` — Label [font]
- ohne: –

Beispiel ✅✅ (echte Referenzdaten):
```
<!-- wp:divi/countdown-timer {"title":{"innerContent":{"desktop":{"value":"Titel"}}},"content":{"advanced":{"dateTime":{"desktop":{"value":"2026-11-27 07:57"}}}},"builderVersion":"5.18.0"} /-->
```

### divi/accordion – Accordion
Ziehharmonika (Container). Kinder: accordion-item.

- Container. Auf/zu-Optik: `openToggle`/`closedToggle` (Hintergrund- und Textfarbe) und Icon `closedToggleIcon`.
- Abstände zwischen Einträgen: `module.decoration.layout` (Standard `flexDirection:column`, Gap 30px) ✅.

- `title.decoration.font` — Title [font; +color +headingLevel]
- `closedToggleIcon.decoration.icon` — Toggle Icon [icon; +icon -color -useSize -size]
- `closedToggleIcon.decoration.icon` — Icon [icon; -icon +color +useSize +size]
- `content.decoration.bodyFont` [Std bodyFont]
- `openToggle.decoration.background.desktop.value.color` — Open Toggle Background Color [Farbe]
- `openToggle.decoration.font.font.desktop.value.color` — Open Title Text Color [Farbe]
- `closedToggle.decoration.background.desktop.value.color` — Closed Toggle Background Color [Farbe]
- `closedToggle.decoration.font` — Closed Title [font; +color]
- ohne: –

### divi/accordion-item – Accordion Item
Ein Eintrag der Ziehharmonika.

- `module.advanced.open:"on"` = beim Laden offen ✅✅. Titel `title.innerContent`, Inhalt `content.innerContent` (HTML) ✅✅.

- `title.innerContent` — Title [Text]
- `title.decoration.font` — Title [font; +color +headingLevel]
- `closedToggleIcon.decoration.icon` — Closed Icon [Icon]
- `closedToggleIcon.decoration.icon` — Icon [icon; -icon +color +useSize +size]
- `openToggle.decoration.background.desktop.value.color` — Open Toggle Background Color [Farbe]
- `openToggle.decoration.font.font.desktop.value.color` — Open Title Text Color [Farbe]
- `closedToggle.decoration.background.desktop.value.color` — Closed Toggle Background Color [Farbe]
- `closedToggle.decoration.font.font.desktop.value.color` — Closed Title Text Color [Farbe]
- `closedToggle.decoration.font` — Closed Title [font; -color]
- `content.innerContent` — Body [HTML]
- `content.decoration.bodyFont` [Std bodyFont]
- ohne: –

Beispiel ✅✅ (echte Referenzdaten):
```
<!-- wp:divi/accordion-item {"module":{"advanced":{"open":{"desktop":{"value":"on"}}}},"title":{"innerContent":{"desktop":{"value":"Titel"}}},"content":{"innerContent":{"desktop":{"value":"<p>Text</p>"}}},"builderVersion":"5.18.0"} /-->
```

### divi/icon – Icon
Einzelnes Icon.

- Icon-Wert wie in Abschnitt 4. Größe `icon.advanced.size` (1 bis 120), Farbe `icon.advanced.color`.

- `icon.innerContent` — Icon [Icon]
- `icon.innerContent` — Icon [link]
- `icon.advanced.color` — Icon Color [Farbe]
- `icon.advanced.size` — Icon Size [Zahl; max 120]
- `icon.advanced.align` — Icon Alignment [Wahl; left/center/right]
- ohne: –

### divi/icon-list – Icon List
Liste mit Icons als Aufzählungszeichen (Container). Kinder: icon-list-item.

- Container: Gap/Richtung `module.decoration.layout` (Standard Spalte, 10px) ✅. Icon-Stil für ALLE Punkte hier, einzelne überschreiben im Item.

- `icon.advanced.color` — Icon Color [Farbe]
- `icon.advanced.size` — Icon Size [Zahl; max 120]
- `icon.decoration.background` — Icon [background]
- `icon.decoration.border` — Icon [border]
- `icon.decoration.boxShadow` — Icon [box-shadow]
- `icon.decoration.spacing` — Icon [spacing]
- `listItem.decoration.font` [font]
- ohne: –

### divi/icon-list-item – Icon List Item
Ein Listenpunkt mit Icon.

- Icon-Objekt mit `target:"off"` ✅✅ (Link-Ziel). Text als String.

- `content.innerContent` — Text [Text]
- `content.decoration.font` [font]
- `icon.innerContent` — Icon [Icon]
- `icon.advanced.color` — Icon Color [Farbe]
- `icon.advanced.size` — Icon Size [Zahl; max 120]
- `icon.decoration.background` — Icon [background]
- `icon.decoration.border` — Icon [border]
- `icon.decoration.boxShadow` — Icon [box-shadow]
- `icon.decoration.spacing` — Icon [spacing]
- ohne: –

Beispiel ✅✅ (echte Referenzdaten):
```
<!-- wp:divi/icon-list-item {"content":{"innerContent":{"desktop":{"value":"List item text"}}},"icon":{"innerContent":{"desktop":{"value":{"unicode":"&#x21;","type":"divi","weight":"400","target":"off"}}}},"builderVersion":"5.18.0"} /-->
```

### divi/cta – Call To Action
Handlungsaufforderung: Titel + Text + Button.

- Button wie beim Button-Modul, aber unter `button.*` mit eigenem Text. `content.innerContent` hat kein Label im Schema = HTML ⚠️.

- `title.innerContent` — Title [Text]
- `title.decoration.font` [Std font]
- `content.innerContent`
- `content.decoration.bodyFont` [Std bodyFont]
- `button.innerContent.desktop.value.text` — Button [Text]
- `button.innerContent` — Button [button-link]
- `button.decoration.{background,border,boxShadow,button,font,sizing,spacing}` [Std-Gruppen]
- ohne: –

### divi/tabs – Tabs
Reiter (Container). Kinder: tab.


- `content.decoration.background` [Std background]
- `content.decoration.bodyFont` [font-body]
- `tab.decoration.background` [background]
- `tab.decoration.font` [font; -textAlign]
- `activeTab.decoration.background` [background]
- `activeTab.decoration.font` [font; -textAlign]
- ohne: background, layout

### divi/tab – Tab
Ein Reiter.


- `content.innerContent` — Body [HTML]
- `content.decoration.bodyFont` [font-body]
- `title.innerContent` — Title [Text]
- `title.decoration.font` [font; -textAlign]
- ohne: border, boxShadow, scroll, sticky

### divi/slider – Slider
Slider (Container). Kinder: slide.

- Container. `children.*` = Voreinstellungen für alle Slides ⚠️.

- `module.advanced.auto` — Automatic Animation [on/off]
- `module.advanced.autoSpeed` — Automatic Animation Speed (in ms) [Text]
- `module.advanced.autoIgnoreHover` — Continue Automatic Slide on Hover [on/off]
- `arrows.advanced.color` — Arrow Color [Farbe]
- `arrows.advanced.show` — Show Arrows [on/off]
- `pagination.advanced.show` — Show Controls [on/off]
- `pagination.advanced.style` — Controls Style [Wahl; swipe/dot]
- `pagination.advanced.swipeText` — Swipe Label [Text]
- `pagination.advanced.showCounter` — Show Slide Count [on/off]
- `pagination.advanced.showSwipeLabel` — Show Swipe Label [on/off]
- `pagination.advanced.color` — Controls Text Color [Farbe]
- `title.decoration.font` — Title [font; +headingLevel]
- `button.decoration.button` — Button [button; -fontGroup.lineHeight -fontGroup.textAlign -borderGroup.styles]
- `content.decoration.bodyFont` [Std bodyFont]
- `content.decoration.sizing.desktop.value.width` — Content Width [Zahl; max 100; defaultUnit %]
- `content.decoration.sizing.desktop.value.maxWidth` — Content Max Width [Zahl; max 100; defaultUnit %]
- `children.slideOverlay.advanced.use` — Use Background Overlay [on/off]
- `children.contentOverlay.advanced.use` — Use Text Overlay [on/off]
- `children.content.advanced.showOnMobile` — Show Content On Mobile [on/off; Std "on"]
- `children.button.advanced.showOnMobile` — Show CTA On Mobile [on/off; Std "on"]
- `children.decoration.background` [background]
- `children.slideOverlay.decoration.background.desktop.value.color` — Background Overlay Color [Farbe]
- `children.contentOverlay.decoration.background.desktop.value.color` — Text Overlay Color [Farbe]
- `children.contentOverlay.decoration.border.desktop.value.radius` — Text Overlay Border Radius [border-radius]
- `image.advanced.showOnMobile` — Show Image / Video On Mobile [on/off]
- `image.decoration.image` — Image [image]
- `dotNav.decoration.background.desktop.value.color` — Dot Navigation Color [Farbe]
- ohne: background

### divi/slide – Slide
Eine Folie des Sliders.


- `image.innerContent.desktop.value.src` — Image [Upload]
- `image.advanced.alignment` — Image Alignment [Wahl; center/bottom]
- `title.innerContent` — Title [Text]
- `title.decoration.font` [Std font; +headingLevel]
- `contentOverlay.advanced.use` — Use Text Overlay [on/off]
- `contentOverlay.decoration.background.desktop.value.color` — Text Overlay Color [Farbe]
- `contentOverlay.decoration.border.desktop.value.radius` — Text Overlay Border Radius [border-radius]
- `button.innerContent.desktop.value.text` — Button [Text]
- `button.innerContent` — Button [button-link]
- `button.decoration.button` — Button [button; -fontGroup.lineHeight -fontGroup.textAlign -borderGroup.styles]
- `content.innerContent` — Body [HTML]
- `content.decoration.bodyFont` [Std bodyFont]
- `slideOverlay.advanced.use` — Use Background Overlay [on/off]
- `slideOverlay.decoration.background.desktop.value.color` — Background Overlay Color [Farbe]
- `arrows.advanced.color` — Arrow Color [Farbe]
- `dotNav.decoration.background.desktop.value.color` — Dot Navigation Color [Farbe]
- `video.innerContent` — Video [Upload]
- ohne: animation, border, boxShadow, position, scroll, sticky

### divi/video – Video
Video (MP4/WebM/YouTube) mit Vorschaubild.

- `video.innerContent.desktop.value.{src,webm}`: `src` nimmt MP4-Datei ODER YouTube-URL ✅. Vorschaubild `thumbnail.innerContent.desktop.value.src`.

- `thumbnail.innerContent.desktop.value.src` — Overlay Image [composite]
- `overlay.decoration.background.desktop.value.color` — Overlay Background Color [Farbe]
- `video.innerContent.desktop.value.src` — Video MP4 File Or Youtube URL [Upload]
- `video.innerContent.desktop.value.webm` — Video WEBM File [Upload]
- `playIcon.decoration.icon` — Play Icon [icon; +icon +size +useSize]
- ohne: –

### divi/divider – Divider
Trennlinie.

- `divider.advanced.line.desktop.value.show` "on" = sichtbar. `weight` px (max 100).

- `divider.advanced.line.desktop.value.show` — Show Divider [on/off]
- `divider.advanced.line.desktop.value.color` — Line Color [Farbe]
- `divider.advanced.line.desktop.value.style` — Line Style [Wahl; solid/dashed/dotted/double/groove/ridge/inset/outset/none]
- `divider.advanced.line.desktop.value.position` — Line Position [Wahl; top/center/bottom]
- `divider.advanced.line.desktop.value.weight` — Divider Weight [Zahl; max 100; defaultUnit px]
- ohne: layout

### divi/counter – Bar Counter
Ein Balken im Balkenzähler (Kind von counters).

- Balken im Container `counters`; Prozent als Text (`barProgress.innerContent`).

- `barCounter.decoration.{background,border,boxShadow,sizing}` [Std-Gruppen]
- `title.innerContent` — Title [Text]
- `title.decoration.font` [Std font; -headingLevel]
- `barProgress.innerContent` — Percent [Text]
- `barProgress.decoration.background` — Bar Counter [composite; +color]
- `barProgress.decoration.font` [Std font]
- ohne: background, border, boxShadow, disabledOn, sizing, sticky

### divi/counters – Bar Counters
Balkenzähler (Container). Kinder: counter.


- `barCounter.decoration.{background,border,boxShadow}` [Std-Gruppen]
- `title.decoration.font` [Std font; -headingLevel]
- `barProgress.decoration.font` [Std font]
- `barProgress.advanced.usePercentages` — Show Percentage [on/off]
- `children.decoration.background` — Bar [composite; +color]
- ohne: background, border, boxShadow

### divi/number-counter – Number Counter
Zahlen-Zähler (zählt hoch).


- `title.innerContent` — Title [Text]
- `title.decoration.font` [Std font; +headingLevel]
- `number.advanced.enablePercentSign` — Percent Sign [on/off; Std "on"]
- `number.innerContent` — Number [Text; Std "0"]
- `number.decoration.font` [Std font; -headingLevel]
- ohne: –

### divi/circle-counter – Circle Counter
Kreis-Zähler (Prozent-Ring).


- `circle.advanced.circle` — Circle [composite; +color +backgroundColor +backgroundOpacity]
- `title.innerContent` — Title [Text]
- `title.decoration.font` — Title [font; +headingLevel]
- `number.advanced.percentSign` — Percent Sign [on/off]
- `number.innerContent` — Number [Text]
- `number.decoration.font` — Number [font; -headingLevel -lineHeight]
- ohne: –

### divi/testimonial – Testimonial
Kundenstimme mit Bild, Name, Position.

- Bild: `portrait.innerContent.desktop.value.src`. Zitat: `content.innerContent` (HTML).

- `company.innerContent.desktop.value.text` — Company [Text]
- `company.innerContent.desktop.value.linkUrl` — Company Link URL [Text]
- `company.innerContent.desktop.value.linkTarget` — Company Link Target [Wahl; off/on]
- `company.decoration.font` — Company Text [font; -textAlign]
- `quoteIcon.decoration.background.desktop.value.color` — Quote Icon Background Color [Farbe]
- `quoteIcon.decoration.icon.desktop.value.show` — Show Quote Icon [on/off]
- `quoteIcon.decoration.icon` — Quote Icon [icon]
- `content.innerContent` — Body [HTML]
- `content.decoration.bodyFont` [font-body]
- `author.innerContent` — Author [Text]
- `author.decoration.font` — Author Text [font]
- `jobTitle.innerContent` — Job Title [Text]
- `jobTitle.decoration.font` — Position Text [font; -textAlign]
- `portrait.innerContent.desktop.value.src` — Image [Upload]
- `portrait.decoration.image` — Image [image]
- ohne: –

### divi/pricing-tables – Pricing Tables
Preistabellen (Container). Kinder: pricing-table.

- Container. Farben der ausgewählten ("featured") Tabelle: `featured*`. Gestaltung gilt für alle Kinder.

- `title.decoration.background.desktop.value.color` — Table Header Background Color [Farbe]
- `title.decoration.font` — Title [font; +headingLevel]
- `subtitle.decoration.font` — Subtitle [font]
- `price.decoration.background.desktop.value.color` — Pricing Area Background Color [Farbe]
- `price.decoration.font` — Price [font]
- `price.decoration.border` [border]
- `currencyFrequency.decoration.font` — Currency & Frequency [font]
- `content.decoration.bodyFont` [font-body]
- `content.advanced.bulletColor` — Bullet Color [Farbe]
- `content.advanced.showBullet` — Show Bullets [on/off]
- `excluded.decoration.font` — Excluded Item [font]
- `featuredTable.decoration.background.desktop.value.color` — Featured Background Color [Farbe]
- `featuredTable.advanced.showDropShadow` — Show Featured Drop Shadow [on/off]
- `featuredTitle.decoration.background.desktop.value.color` — Featured Header Background Color [Farbe]
- `featuredTitle.decoration.font.font.desktop.value.color` — Featured Title Text Color [Farbe]
- `featuredContent.decoration.font.font.desktop.value.color` — Featured Body Text Color [Farbe]
- `featuredContent.advanced.bulletColor` — Featured Bullet Color [Farbe]
- `featuredSubtitle.decoration.font.font.desktop.value.color` — Featured Subtitle Text Color [Farbe]
- `featuredPrice.decoration.background.desktop.value.color` — Featured Pricing Area Background Color [Farbe]
- `featuredPrice.decoration.font.font.desktop.value.color` — Featured Price Text Color [Farbe]
- `featuredCurrencyFrequency.decoration.font.font.desktop.value.color` — Featured Currency & Frequency Text Color [Farbe]
- `featuredExcluded.decoration.font.font.desktop.value.color` — Featured Excluded Item Color [Farbe]
- `button.innerContent` [Std innerContent]
- `button.decoration.{background,border,boxShadow,button,font,sizing,spacing}` [Std-Gruppen]
- ohne: –

### divi/pricing-table – Pricing Table
Eine Preisspalte.

- `module.advanced.featured:"on"` = hervorgehobene Tabelle. Features als HTML-Liste in `content.innerContent` ⚠️.

- `module.advanced.featured` — Make This Table Featured [on/off]
- `currencyFrequency.innerContent.desktop.value.currency` — Currency [Text]
- `currencyFrequency.innerContent.desktop.value.per` — Frequency [Text]
- `currencyFrequency.decoration.font` [Std font; -headingLevel]
- `subtitle.innerContent` — Subtitle [Text]
- `subtitle.decoration.font` [Std font; -headingLevel]
- `title.innerContent` — Title [Text]
- `title.decoration.background.desktop.value.color` — Table Header Background Color [Farbe]
- `title.decoration.font` — Title [font; +headingLevel]
- `price.innerContent` — Price [Text]
- `price.decoration.background.desktop.value.color` — Pricing Area Background Color [Farbe]
- `price.decoration.font` — Price [font]
- `price.decoration.border` [border]
- `button.innerContent.desktop.value.text` — Button [Text]
- `button.innerContent` — Button [button-link]
- `button.decoration.{background,border,boxShadow,button,font,sizing,spacing}` [Std-Gruppen]
- `excluded.decoration.font` [Std font]
- `content.innerContent` — Body [HTML]
- `content.decoration.bodyFont` [Std bodyFont]
- `content.advanced.bulletColor` — Bullet [composite; +bulletColor]
- ohne: sticky

### divi/contact-form – Contact Form
Kontaktformular (Container). Kinder: contact-field.

- Empfänger: `email.advanced.receiver`. Eigener Absender/SMTP-Konfiguration im Modul NICHT im Schema.

- `module.advanced.showLabels` — Show Labels [on/off]
- `module.advanced.successMessage` — Success Message [Text]
- `title.innerContent` — Title [Text]
- `title.decoration.font` [Std font; +headingLevel]
- `captcha.decoration.font` [Std font; -textAlign]
- `button.innerContent.desktop.value.text` — Submit Button [Text]
- `button.decoration.{background,border,boxShadow,button,font,sizing,spacing}` [Std-Gruppen]
- `email.advanced.receiver` — Email Address [Text]
- `email.innerContent` — Message Pattern [textarea]
- `redirect.advanced.useRedirect` — Enable Redirect URL [on/off]
- `redirect.innerContent` — Redirect URL [Text]
- ohne: –

### divi/contact-field – Field
Ein Formularfeld.

- Typ: `fieldItem.advanced.type` ∈ input/email/text/checkbox/radio/select. Pflichtfeld: `fieldItem.advanced.required`.

- `fieldTitle.decoration.font` [Std font]
- `fieldItem.advanced.id` — Field ID [Text]
- `fieldItem.advanced.type` — Type [Wahl; input/email/text/checkbox/radio/select]
- `fieldItem.advanced.minLength` — Minimum Length [Zahl; defaultUnit ]
- `fieldItem.advanced.maxLength` — Maximum Length [Zahl; defaultUnit ]
- `fieldItem.advanced.allowedSymbols` — Allowed Symbols [Wahl; all/letters/numbers/alphanumeric]
- `fieldItem.advanced.checkboxOptions` — Options [sortable-list]
- `fieldItem.advanced.radioOptions` — Options [sortable-list]
- `fieldItem.advanced.selectOptions` — Options [sortable-list]
- `fieldItem.advanced.required` — Required Field [on/off]
- `fieldItem.innerContent` — Title [Text]
- `conditionalLogic.innerContent` — Rules [conditions]
- `conditionalLogic.advanced.enable` — Enable [on/off]
- `conditionalLogic.advanced.relation` — Relation [on/off]
- ohne: –

### divi/menu – Menu
Menü (Navigation, Logo, Warenkorb, Suche).

- Welches Menü: `menu.advanced.menuId`. Logo mit Link: `logo.innerContent.desktop.value.{src,linkUrl,linkTarget}`. Cart/Suche/Hamburger sind standardmäßig aus bzw. mit Variable `gcid-primary-color` gefärbt ✅.

- `logo.innerContent.desktop.value.src` — Logo [Upload]
- `logo.innerContent.desktop.value.linkUrl` — Logo Link URL [Text]
- `logo.innerContent.desktop.value.linkTarget` — Logo Link Target [Wahl; off/on]
- `logo.decoration.border` — Logo [border]
- `logo.decoration.boxShadow` — Logo [box-shadow]
- `logo.decoration.filters` — Logo [filters]
- `logo.decoration.sizing` — Logo [sizing; -alignment -minHeight]
- `menu.advanced.menuId` — Menu [select-menu]
- `menu.advanced.style` — Menu Style [Wahl; left_aligned/centered/inline_centered_logo]
- `menu.advanced.activeLinkColor` — Active Link Color [Farbe]
- `menu.decoration.font` — Menu [font; -textAlign]
- `menuDropdown.advanced.direction` — Dropdown Menu Direction [Wahl; downwards/upwards]
- `menuDropdown.advanced.animation` — Dropdown Menu Animation [Wahl; expand/fade/flip/slide]
- `menuDropdown.advanced.lineColor` — Dropdown Menu Line Color [Farbe]
- `menuDropdown.advanced.activeLinkColor` — Dropdown Menu Active Link Color [Farbe]
- `menuDropdown.decoration.background.desktop.value.color` — Dropdown Menu Background Color [Farbe]
- `menuDropdown.decoration.font.font.desktop.value.color` — Dropdown Menu Text Color [Farbe]
- `menuMobile.advanced.collapsible` — Collapsible Mobile Menu [on/off; Std "off"]
- `menuMobile.advanced.parentLinksActive` — Parent Links Active [on/off; Std "on"]
- `menuMobile.decoration.background.desktop.value.color` — Mobile Menu Background Color [Farbe]
- `menuMobile.decoration.font.font.desktop.value.color` — Mobile Menu Text Color [Farbe]
- `cartQuantity.advanced.show` — Show Cart Quantity [on/off; Std "off"]
- `cartQuantity.decoration.font` — Cart Quantity [font; -textAlign]
- `cartIcon.advanced.show` — Show Shopping Cart Icon [on/off; Std "off"]
- `cartIcon.decoration.font.font.desktop.value.color` — Shopping Cart Icon Color [Farbe; Std Variable/lang]
- `cartIcon.decoration.font.font.desktop.value.size` — Shopping Cart Icon Font Size [Zahl; max 120; defaultUnit px; Std {"size": "17px"}]
- `searchIcon.advanced.show` — Show Search Icon [on/off; Std "off"]
- `searchIcon.decoration.font.font.desktop.value.color` — Search Icon Color [Farbe; Std Variable/lang]
- `searchIcon.decoration.font.font.desktop.value.size` — Search Icon Font Size [Zahl; max 120; defaultUnit px; Std {"size": "17px"}]
- `hamburgerMenuIcon.decoration.font.font.desktop.value.color` — Hamburger Menu Icon Color [Farbe; Std Variable/lang]
- `hamburgerMenuIcon.decoration.font.font.desktop.value.size` — Hamburger Menu Icon Font Size [Zahl; max 120; defaultUnit px; Std {"size": "32px"}]
- `collapsibleMenu.decoration.background` — Toggle [background]
- `collapsibleMenu.decoration.spacing` — Toggle [spacing]
- `collapsibleMenu.decoration.border` — Toggle [border]
- `collapsibleMenu.decoration.boxShadow` — Toggle [box-shadow]
- `collapsibleMenuOpenIcon.decoration.icon` — Collapsible Menu Open Icon [Icon]
- `collapsibleMenuOpenIcon.decoration.font.font.desktop.value.size` — Collapsible Menu Open Icon Size [Zahl; max 120; defaultUnit px; Std {"size": "24px"}]
- `collapsibleMenuOpenIcon.decoration.font.font.desktop.value.color` — Collapsible Menu Open Icon Color [Farbe]
- `collapsibleMenuCloseIcon.decoration.icon` — Collapsible Menu Close Icon [Icon]
- `collapsibleMenuCloseIcon.decoration.font.font.desktop.value.size` — Collapsible Menu Close Icon Size [Zahl; max 120; defaultUnit px; Std {"size": "24px"}]
- `collapsibleMenuCloseIcon.decoration.font.font.desktop.value.color` — Collapsible Menu Close Icon Color [Farbe]
- ohne: –

### divi/gallery – Gallery
Bildergalerie (Raster oder Slider).

- Bilder: `image.advanced.galleryIds` (Upload-Galerie, IDs ⚠️). Raster-Spalten: `galleryGrid.decoration.layout` (`display:"grid"`, `gridColumnCount:"4"`) ✅.

- `module.advanced.fullwidth` — Layout [Wahl; off/on]
- `module.advanced.postsNumber` — Image Count [Text]
- `module.advanced.showTitleAndCaption` — Show Title and Caption [on/off]
- `module.advanced.auto` — Automatic Animation [on/off]
- `module.advanced.autoSpeed` — Automatic Animation Speed (in ms) [Text]
- `title.decoration.font` [Std font; +headingLevel]
- `caption.decoration.font` [Std font]
- `pagination.advanced.showPagination` — Show Pagination [on/off]
- `pagination.decoration.font` [Std font]
- `item.decoration.border` — Border [border]
- `image.advanced.orientation` — Thumbnail Orientation [Wahl; landscape/portrait]
- `image.advanced.galleryIds` — Images [upload-gallery]
- `image.advanced.galleryOrderby` — Image Order [Wahl; default/rand]
- `image.decoration.image` — Image [image]
- `overlay.innerContent.desktop.value.icon` — Overlay Icon [Icon]
- `overlay.advanced.zoomIconColor` — Overlay Icon Color [Farbe]
- `overlay.advanced.hoverOverlayColor` — Overlay Background Color [Farbe]
- `galleryGrid.decoration.layout` [layout; Std {"display":"grid","gridColumnCount":"4"}]
- ohne: border, layout

### divi/blog – Blog
Beitragsliste (Blog).

- Raster: `blogGrid.decoration.layout` (`display:"grid"`, `gridColumnCount:"3"`) ✅.

- `post.advanced.useCurrentLoop` — Posts For Current Page [on/off]
- `post.advanced.type` — Post Type [Wahl]
- `post.advanced.number` — Post Count [Text]
- `post.advanced.categories` — Included Categories [checkboxes]
- `post.advanced.dateFormat` — Date Format [Text]
- `post.advanced.excerptContent` — Content Length [Wahl; off/on]
- `post.advanced.excerptManual` — Use Post Excerpts [on/off]
- `post.advanced.excerptLength` — Excerpt Length [Text]
- `post.advanced.offset` — Post Offset Number [Text]
- `post.advanced.showExcerpt` — Show Excerpt [on/off]
- `post.decoration.border` — Grid Layout [border]
- `image.advanced.enable` — Show Featured Image [on/off]
- `image.decoration.image` — Image [image]
- `readMore.advanced.enable` — Show Read More Button [on/off]
- `readMore.decoration.font` [Std font]
- `pagination.advanced.enable` — Show Pagination [on/off]
- `pagination.decoration.font` [Std font]
- `meta.advanced.showAuthor` — Show Author [on/off]
- `meta.advanced.showDate` — Show Date [on/off]
- `meta.advanced.showCategories` — Show Categories [on/off]
- `meta.advanced.showComments` — Show Comment Count [on/off]
- `meta.decoration.font` [Std font]
- `title.decoration.font` [Std font; +headingLevel]
- `content.decoration.bodyFont` [Std bodyFont]
- `overlay.decoration.background.desktop.value.color` — Overlay Background Color [Farbe]
- `overlay.advanced.enable` — Featured Image Overlay [on/off]
- `overlayIcon.decoration.icon.desktop.value.color` — Overlay Icon Color [Farbe]
- `overlayIcon.decoration.icon` — Overlay Icon [Icon]
- `fullwidth.decoration.border` [border]
- `blogGrid.decoration.layout` [layout; Std {"display":"grid","gridColumnCount":"3","flexDirection":"column"}]
- `masonry.decoration.background.desktop.value.color` — Grid Tile Background Color [Farbe]
- ohne: border, layout

## 7. Alle übrigen Module (kompakt)

Format: `Attribut`: Pfad-Teil (Label). Der volle Pfad ist Attribut + Rest (z. B. `title: advanced.show` = `title.advanced.show`). Bei Teilfeldern ist `.desktop.value` hier weggelassen (`line.show` = `...line.desktop.value.show`). Leere Standardgruppen (font, bodyFont, background ...) sind hier nicht einzeln genannt: sie gelten für Teile mit Namen wie title/content/button. WooCommerce-Module (Shop, Warenkorb, Kasse, Produkt) sind nur als Liste der Modul-Teile mit Anzahl der Einstellungen genannt; Details bei Bedarf per `python3 -I` aus der JSON-Datei ziehen. `ohne:` = fehlende gemeinsame Gruppen. Werte-Formen wie in Abschnitt 1, 3, 4.

**divi/audio** – Audio. ohne: –
`artistName`: innerContent; `albumName`: innerContent; `audio`: innerContent; `title`: innerContent; `image`: innerContent.src, decoration.image

**divi/before-after-image** – Before/After Image. ohne: –
`beforeImage`: innerContent.src, decoration.image; `afterImage`: innerContent.src, decoration.image; `slider`: advanced.{orientation,position,color,arrowColor}; `labels`: decoration.{font,spacing,border,background}

**divi/breadcrumbs** – Breadcrumbs. ohne: order
`home`: innerContent.text, innerContent.url; `separator`: innerContent.text

**divi/canvas-portal** – Canvas Portal. ohne: layout
`canvas`: advanced.canvasId

**divi/charts** – Chart. ohne: –
`chart`: innerContent.data, innerContent.title, innerContent.subtitle, innerContent.legendTitle, advanced.config.type, advanced.config.showTitle, advanced.config.showSubtitle, advanced.config.showLegend, advanced.config.showLegendTitle, advanced.config.showTooltip, advanced.legend.title, advanced.legend.title.color, advanced.legend.labels, advanced.tooltip.titleFont, advanced.tooltip.bodyFont, advanced.{title,subtitle,legend,legend,tooltip,tooltip}

**divi/payment-button** – Payment Button. ohne: background, border, sizing
`module`: advanced.alignment; `button`: innerContent.provider, innerContent.resourceId, innerContent.environment, innerContent.amountMode, innerContent.amount, innerContent.currency, innerContent.returnUrl, innerContent.cancelUrl, innerContent.description, innerContent.openInNewTab, innerContent.text, innerContent

**divi/group-carousel** – Group Carousel. ohne: layout, order
`module`: advanced.{auto,speed,transitionSpeed,pauseOnHover,centerMode,slidesToShow,slidesToScroll}; `arrows`: advanced.{showArrows,leftIcon,rightIcon,color,size,position}, decoration.{background,border,boxShadow,spacing}; `dotNav`: advanced.{showDots,position,alignment,size,color}; `children`: decoration.{layout,spacing,background,border,boxShadow,filters,transform}; `activeGroups`: decoration.{layout,spacing,background,border,boxShadow,filters,transform}

**divi/code** – Code. ohne: layout
`content`: innerContent

**divi/column-inner** – Inner Column. ohne: layout, sizing
(keine eigenen Einstellungen im Schema)

**divi/comments** – Comments. ohne: –
`module`: advanced.{showReply,showLabels}; `image`: advanced.showAvatar, decoration.image; `commentCount`: advanced.showCount; `meta`: advanced.showMeta

**divi/dropdown** – Dropdown. ohne: position
`module`: advanced.dropdown.position, advanced.dropdown.horizontalMode, advanced.dropdown.showOn, advanced.dropdown.direction, advanced.dropdown.alignment, advanced.dropdown.offset

**divi/filterable-portfolio** – Filterable Portfolio. ohne: border, layout
`portfolio`: advanced.{postsNumber,includedCategories,showTitle,showCategories,showPagination}; `portfolioGrid`: decoration.layout; `portfolioItem`: decoration.border; `overlay`: decoration.background.color, decoration.icon.color, decoration.icon; `image`: decoration.image

**divi/fullwidth-code** – Fullwidth Code. ohne: layout
`content`: innerContent

**divi/fullwidth-header** – Hero. ohne: –
`module`: advanced.headerFullscreen; `image`: innerContent.src, advanced.orientation; `logo`: innerContent.src; `title`: innerContent; `subhead`: innerContent, decoration.font; `content`: innerContent, advanced.{orientation,maxWidth}; `buttonOne`: innerContent.text, innerContent.linkUrl; `buttonTwo`: innerContent.text, innerContent.linkUrl, decoration.button; `scrollDown`: decoration.icon.show, decoration.icon.color, decoration.icon.size, decoration.icon; `overlay`: decoration.background.color

**divi/fullwidth-image** – Fullwidth Image. ohne: layout
`image`: innerContent.src, innerContent.linkUrl, innerContent.linkTarget, advanced.overlay.use, advanced.overlay.backgroundColor, advanced.overlayIcon.hoverIcon, advanced.overlayIcon.iconColor, advanced.lightbox

**divi/fullwidth-map** – Fullwidth Map. ohne: layout
`map`: innerContent, advanced.{googleAPIKey,googleAPIKey,mouseWheel,mobileDragging}

**divi/fullwidth-menu** – Fullwidth Menu. ohne: layout
`logo`: innerContent.src, innerContent.linkUrl, innerContent.linkTarget, decoration.{border,boxShadow,filters,sizing}; `menu`: advanced.{menuId,style,activeLinkColor,fullwidth}, decoration.font; `menuDropdown`: decoration.background.color, decoration.font.font.color, advanced.{direction,animation,lineColor,activeLinkColor}; `menuMobile`: decoration.background.color, decoration.font.font.color; `cartQuantity`: advanced.show, decoration.font; `cartIcon`: decoration.font.font.color, decoration.font.font.size, advanced.show; `searchIcon`: decoration.font.font.color, decoration.font.font.size, advanced.show; `hamburgerMenuIcon`: decoration.font.font.color, decoration.font.font.size

**divi/fullwidth-portfolio** – Post Carousel. ohne: –
`module`: advanced.{autoRotate,autoRotateSpeed}; `portfolio`: innerContent.includedCategories, innerContent.type, innerContent.postsNumber, advanced.{layout,showTitle,showDate}, decoration.font; `title`: innerContent, decoration.font; `overlay`: decoration.background.color, decoration.icon.color, decoration.icon; `image`: decoration.image

**divi/fullwidth-post-content** – Fullwidth Post Content. ohne: layout, transition
`image`: decoration.{border,boxShadow}

**divi/fullwidth-post-slider** – Fullwidth Post Slider. ohne: layout
`module`: advanced.{auto,autoSpeed,autoIgnoreHover}; `content`: advanced.showOnMobile, decoration.sizing; `meta`: advanced.enable, decoration.font; `image`: advanced.{enable,placement,showOnMobile}, decoration.{border,boxShadow,filters}; `button`: innerContent.text, innerContent, advanced.{enable,showOnMobile}; `post`: advanced.{number,categories,orderby,contentSource,excerptManual,excerptLength,offset}; `arrows`: advanced.{color,enable}; `pagination`: decoration.background.color, advanced.enable; `slideOverlay`: decoration.background.color, advanced.use; `contentOverlay`: decoration.background.color, advanced.use, decoration.border

**divi/fullwidth-post-title** – Fullwidth Post Title. ohne: layout
`title`: advanced.showTitle; `meta`: advanced.{showMeta,showAuthor,showDate,dateFormat,showCategories,showCommentsCount}; `textWrapper`: decoration.background.color, advanced.useBackground; `featuredImage`: decoration.sizing.alignment, decoration.sizing.width, decoration.sizing.maxWidth, decoration.sizing.height, decoration.sizing.maxHeight, advanced.{enabled,forceFullwidth,placement}

**divi/fullwidth-slider** – Fullwidth Slider. ohne: layout
`module`: advanced.{auto,autoSpeed,autoIgnoreHover}; `arrows`: advanced.{color,show}; `pagination`: advanced.show; `title`: decoration.font; `button`: decoration.button; `content`: decoration.sizing.width, decoration.sizing.maxWidth; `children`: slideOverlay.advanced.use, contentOverlay.advanced.use, content.advanced.showOnMobile, button.advanced.showOnMobile, slideOverlay.decoration.background.color, contentOverlay.decoration.background.color, contentOverlay.decoration.border.radius; `image`: advanced.showOnMobile, decoration.{border,boxShadow}; `dotNav`: decoration.background.color

**divi/global-slot** – Slot. ohne: –
(keine eigenen Einstellungen im Schema)

**divi/instagram-feed** – Instagram Feed. ohne: –
`feed`: innerContent.accountId, innerContent.postCount, advanced.config.lightbox; `media`: decoration.image; `followButton`: innerContent.text, advanced.show

**divi/link** – Link. ohne: –
`content`: innerContent.text, innerContent, decoration.font; `icon`: innerContent, advanced.{color,size}, decoration.{background,border,boxShadow,spacing}

**divi/lottie** – Lottie. ohne: –
`lottie`: innerContent.src, innerContent.uploadNotice, innerContent.trigger, innerContent.loop, innerContent.speed, innerContent.direction, innerContent.mode

**divi/login** – Login. ohne: –
`module`: advanced.currentPageRedirect; `title`: innerContent; `content`: innerContent; `button`: innerContent.text, innerContent

**divi/map-pin** – Map Pin. hat nur: 
`pin`: innerContent; `title`: innerContent; `content`: innerContent

**divi/map** – Map. ohne: –
`map`: innerContent, advanced.grayscaleFilter.enabled, advanced.grayscaleFilter.amount, advanced.{warning,googleAPIKey,mouseWheel,mobileDragging}, decoration.filters

**divi/portfolio** – Portfolio. ohne: layout
`portfolio`: innerContent.postsNumber, innerContent.includedCategories, advanced.{showTitle,showCategories,showPagination}; `portfolioGrid`: decoration.layout; `overlay`: decoration.background.color, advanced.{iconColor,hoverIcon}; `image`: decoration.image

**divi/post-content** – Post Content. ohne: layout, transition
`image`: decoration.image

**divi/post-filter** – Post Filter. ohne: –
`module`: advanced.filters.applyMode, advanced.filters.relation, advanced.targetLoop

**divi/post-filter-item** – Post Filter Item. ohne: –
`field`: innerContent.type, innerContent.fieldValueType, innerContent.option, innerContent.customFieldKey, innerContent, innerContent, innerContent, innerContent.labelDateFormat, innerContent.comparison, innerContent.placeholder, innerContent.optionsMethod, advanced.{orderbyEnabledOptions,checkboxOptions,radioOptions,selectOptions}; `label`: innerContent

**divi/post-nav** – Pagination. ohne: background, border, boxShadow, spacing
`module`: advanced.{inSameTerm,taxonomyName,targetLoop}; `links`: advanced.{prevText,nextText,showPrev,showNext}, decoration.{spacing,border,boxShadow,background}

**divi/post-slider** – Post Slider. ohne: –
`module`: advanced.{auto,autoSpeed,autoIgnoreHover}; `content`: advanced.showOnMobile, decoration.sizing; `meta`: advanced.enable, decoration.font; `image`: advanced.{enable,placement,showOnMobile}, decoration.image; `button`: innerContent.text, innerContent, advanced.{enable,showOnMobile}; `post`: advanced.{number,categories,orderby,contentSource,excerptManual,excerptLength,offset}; `arrows`: advanced.{color,enable}; `pagination`: decoration.background.color, advanced.{enable,style,swipeText,showCounter,showSwipeLabel,color}; `slideOverlay`: decoration.background.color, advanced.use; `contentOverlay`: decoration.background.color, advanced.use, decoration.border

**divi/post-title** – Post Title. ohne: –
`title`: advanced.showTitle; `meta`: advanced.{showMeta,showAuthor,showDate,dateFormat,showCategories,showCommentsCount}; `textWrapper`: decoration.background.color, advanced.useBackground; `image`: advanced.{enabled,placement}, decoration.image

**divi/row-inner** – Inner Row. ohne: layout
`module`: advanced.gutter

**divi/search** – Search. ohne: –
`searchPlaceholder`: innerContent; `search`: advanced.{showButton,excludePages,excludePosts}; `module`: advanced.excludedCategories; `button`: decoration.background.color, decoration.font

**divi/sidebar** – Sidebar. ohne: –
`sidebar`: innerContent.area, advanced.layout.alignment, advanced.layout.showBorder; `sidebarWidgets`: advanced.flexType

**divi/signup-custom-field** – Custom Field. ohne: interactions, layout, sticky
`fieldItem`: innerContent, advanced.{fullwidth,predefinedField,id,type,minLength,maxLength,allowedSymbols,checkboxOptions,radioOptions,selectOptions,required,hidden}; `conditionalLogic`: innerContent, advanced.{enable,relation}

**divi/signup** – Email Optin. ohne: –
`module`: advanced.showLabels; `content`: innerContent; `resultMessage`: decoration.font; `button`: innerContent.text, innerContent; `field`: advanced.{nameFieldOnly,nameField,firstNameField,lastNameField,nameFullwidth,firstNameFullwidth,lastNameFullwidth,emailFullwidth,ipAddress}; `footerContent`: innerContent; `customFields`: advanced.{enable,fields,notice}; `success`: advanced.{action,message,redirectUrl,redirectQuery}

**divi/social-media-follow-network** – Social Network. ohne: sticky
`icon`: advanced.size.useSize, advanced.size.size, advanced.color; `socialNetwork`: innerContent.title, innerContent.skypeUrl, innerContent.skypeAction, innerContent.link

**divi/social-media-follow** – Social Media Follow. ohne: –
`icon`: advanced.size.useSize, advanced.size.size, advanced.color; `socialNetwork`: advanced.followButton; `button`: socialNetwork.advanced.followButton

**divi/svg** – SVG. ohne: –
`svg`: innerContent.sourceType, innerContent.code, innerContent.src, innerContent.srcNotice, innerContent.title, innerContent.linkUrl, innerContent.linkTarget, innerContent.rel, advanced.fill.color, advanced.fill.opacity, advanced.stroke.color, advanced.stroke.width, advanced.stroke.opacity

**divi/table-of-contents** – Table of Contents. ohne: –
`title`: innerContent; `list`: innerContent.includedHeadings, innerContent.includeOwnTitle, advanced.interaction.smoothScroll, advanced.interaction.scrollOffsetPx; `emptyState`: innerContent

**divi/team-member** – Person. ohne: –
`name`: innerContent; `position`: innerContent; `image`: innerContent.animation, innerContent.url, decoration.image; `content`: innerContent; `social`: innerContent.facebookUrl, innerContent.twitterUrl, innerContent.linkedinUrl, decoration.icon

**divi/timeline** – Timeline. ohne: layout
`module`: advanced.timeline.direction, advanced.timeline.position, advanced.timeline.position, advanced.timeline.startFrom, advanced.timeline.startFrom, advanced.timeline; `children`: spacer.advanced.displayElementsOnSpacer; `marker`: advanced.position, decoration.icon; `date`: decoration.font; `dateEven`: decoration.font; `title`: decoration.font; `titleEven`: decoration.font; `content`: decoration.bodyFont; `contentEven`: decoration.bodyFont

**divi/timeline-item** – Timeline Item. ohne: layout, sticky
`spacer`: advanced.displayElementsOnSpacer; `marker`: innerContent, advanced.position, decoration.icon; `date`: innerContent, decoration.font; `title`: innerContent, decoration.font; `content`: innerContent, advanced.text, decoration.bodyFont

**divi/toggle** – Toggle. ohne: –
`module`: advanced.open; `openToggleIcon`: decoration.icon; `closedToggleIcon`: decoration.icon; `title`: decoration.font; `closedTitle`: decoration.font.font; `content`: innerContent; `openToggle`: decoration.background.color, decoration.font.font.color; `closedToggle`: decoration.background.color

**divi/tooltip** – Tooltip. ohne: position
`content`: innerContent; `module`: advanced.tooltip.trigger, advanced.tooltip.positionMode, advanced.tooltip.placement, advanced.tooltip.skid, advanced.tooltip.distance, advanced.tooltip.openDelay, advanced.tooltip.closeDelay, advanced.tooltip.showArrow, advanced.tooltip.arrowColor, advanced.tooltip.arrowPlacement, advanced.tooltip.arrowOffset, advanced.tooltip.arrowSize

**divi/video-slider-item** – Video Slider Item. ohne: background, border, boxShadow, layout, scroll, sizing, spacing
`overlay`: thumbnail.innerContent.src, decoration.background.color; `playIcon`: decoration.icon; `sliderControls`: advanced.color; `video`: innerContent.src, innerContent.webm

**divi/video-slider** – Video Slider. ohne: border, boxShadow, layout
`overlay`: advanced.showImageOverlay; `playIcon`: overlay.decoration.background.color, decoration.icon; `sliderControls`: advanced.{color,useArrows,useThumbnails}

**divi/woocommerce-breadcrumb** – Woo Breadcrumbs. ohne: layout
`content` (5)

**divi/woocommerce-cart-notice** – Woo Notice. ohne: layout
`content` (3); `button` (1); `field` (1); `form` (4); `title` (1)

**divi/woocommerce-product-add-to-cart** – Woo Product Add To Cart. ohne: layout
`content` (1); `button` (1); `elements` (2); `fieldLabels` (1)

**divi/woocommerce-product-additional-info** – Woo Product Information. ohne: layout
`title` (1); `content` (2); `attribute` (1); `elements` (1); `table` (4); `tableCell` (4); `tableRow` (4)

**divi/woocommerce-product-description** – Woo Product Description. ohne: layout
`content` (4)

**divi/woocommerce-product-gallery** – Woo Product Gallery. ohne: layout
`title` (1); `image` (4); `content` (4); `caption` (1); `layout` (2); `galleryGrid` (1); `pagination` (1); `overlay` (1); `overlayIcon` (2)

**divi/woocommerce-product-images** – Woo Product Images. ohne: layout
`image` (1); `content` (1); `elements` (3); `saleBadge` (5); `galleryGrid` (1)

**divi/woocommerce-product-meta** – Woo Product Meta. ohne: layout
`content` (3); `elements` (3); `layout` (1)

**divi/woocommerce-product-price** – Woo Product Price. ohne: layout
`content` (1); `price` (1); `saleNewPrice` (1); `saleOldPrice` (1)

**divi/woocommerce-product-rating** – Woo Product Rating. ohne: layout
`content` (1); `body` (1); `elements` (2); `layout` (1); `rating` (1)

**divi/woocommerce-product-reviews** – Woo Product Reviews. ohne: layout
`image` (1); `content` (1); `button` (1); `comment` (1); `elements` (4); `formTitle` (1); `meta` (1); `reviewCount` (1); `starRating` (1)

**divi/woocommerce-product-stock** – Woo Product Stock. ohne: layout
`content` (1); `inStock` (1); `onBackorder` (1); `outOfStock` (1)

**divi/woocommerce-product-tabs** – Woo Product Tabs. ohne: layout
`content` (3); `activeTab` (2); `inactiveTab` (1); `tab` (1)

**divi/woocommerce-product-title** – Woo Product Title. ohne: layout
`title` (1); `content` (1)

**divi/woocommerce-product-upsell** – Woo Product Upsell. ohne: layout
`title` (1); `image` (1); `content` (5); `elements` (5); `overlay` (1); `overlayIcon` (2); `price` (1); `productTitle` (1); `rating` (1); `saleBadge` (5); `salePrice` (1)

**divi/woocommerce-related-products** – Woo Related Products. ohne: layout
`title` (1); `image` (1); `content` (6); `elements` (5); `overlay` (1); `overlayIcon` (2); `price` (1); `productTitle` (1); `rating` (1); `saleBadge` (5); `salePrice` (1)

**divi/shop** – Woo Products. ohne: layout
`title` (1); `image` (1); `overlay` (1); `overlayIcon` (2); `content` (7); `elements` (6); `price` (1); `rating` (1); `saleBadge` (5); `salePrice` (1); `pagination` (1)

**divi/woocommerce-cart-products** – Woo Cart Products. ohne: layout
`elements` (4); `layout` (1); `tableHeader` (2); `content` (1); `table` (7); `tableRow` (3); `tableCell` (5); `removeIcon` (3); `image` (1); `button` (1); `disabledButton` (1)

**divi/woocommerce-cart-totals** – Woo Cart Totals. ohne: layout
`title` (1); `content` (1); `button` (4); `columnLabel` (1); `table` (7); `tableCell` (4); `tableRow` (3)

**divi/woocommerce-checkout-additional-info** – Woo Checkout Information. ohne: layout
`title` (1); `elements` (1)

**divi/woocommerce-checkout-billing** – Woo Checkout Billing. ohne: layout
`module` (1); `title` (1); `formNotice` (5); `layout` (1)

**divi/woocommerce-checkout-order-details** – Woo Checkout Details. ohne: layout
`title` (1); `content` (1); `columnLabel` (1); `table` (7); `tableCell` (4); `tableRow` (3)

**divi/woocommerce-checkout-payment-info** – Woo Checkout Payment. ohne: layout
`module` (1); `content` (1); `button` (1); `formNotice` (5); `radioButton` (5); `selectedRadioButton` (5); `tooltip` (5)

**divi/woocommerce-checkout-shipping** – Woo Checkout Shipping. ohne: layout
`module` (1); `title` (1); `layout` (1)

**divi/woocommerce-cross-sells** – Woo Cross Sells. ohne: layout
`title` (1); `price` (1)

**divi/layout** – . hat nur: 
(keine eigenen Einstellungen im Schema)

**divi/shortcode-module** – Shortcode Module. hat nur: 
(keine eigenen Einstellungen im Schema)
