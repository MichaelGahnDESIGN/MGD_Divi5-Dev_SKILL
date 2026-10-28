# Divi-5-Blockdaten: echte Referenz und Fallen beim Anlegen per REST

Quelle: private Seite "Referenz Module" auf der Dev-Seite, im Visual Builder gebaut und gespeichert. Divi 5.18.0. Gelesen über die WordPress-Schnittstelle (`/wp-json/wp/v2/pages/<ID>?context=edit`, `content.raw`).
Das Bild ist hier gekürzt (war ein eingebettetes Platzhalter-Bild).

## Was daraus folgt

- Alles steckt in `<!-- wp:divi/placeholder -->` ... `<!-- /wp:divi/placeholder -->` und darin `section > row > column > Module`.
- Divi speichert **nur Werte, die vom Standard abweichen**. Ein neues Button-Modul besteht nur aus Text und `builderVersion`.
- Aufbau der Werte: `Bereich > Option > Bildschirmgröße (desktop, phone, phoneWide) > value`.
- Sonderzeichen in Texten bleiben als `<` (für `<`) und `&` (für `&`) stehen. Nicht umwandeln.
- Module ohne Kinder enden mit `/-->`, Module mit Kindern (accordion, icon-list, row, column) haben ein Ende-Tag.
- Zwei Zeilen-Arten kommen vor: alte Form mit `display: block` (aus dem Elementor-Import, builderVersion alpha.18.2) und neue Flex-Form (`columnStructure`, `flexColumnStructure`, `flexType`).
- Neu gebaute Module tragen `builderVersion` 5.18.0.

## Gesehene Blöcke

`section, row, column, accordion, accordion-item, button, countdown-timer, image, icon, icon-list, icon-list-item, heading`

## Rohdaten (Auszug)

```
<!-- wp:divi/placeholder -->
<!-- wp:divi/section {"module":{"meta":{"adminLabel":{"desktop":{"value":"Section"}}},"decoration":{"layout":{"desktop":{"value":{"display":"block"}}}}},"builderVersion":"5.0.0-public-alpha.18.2"} -->
<!-- wp:divi/row {"module":{"meta":{"adminLabel":{"desktop":{"value":"Row"}}},"decoration":{"layout":{"desktop":{"value":{"display":"block"}}}}},"builderVersion":"5.0.0-public-alpha.18.2"} -->
<!-- wp:divi/column {"module":{"advanced":{"type":{"desktop":{"value":"4_4"}}},"decoration":{"layout":{"desktop":{"value":{"display":"block"}}}}},"builderVersion":"5.0.0-public-alpha.18.2"} -->
<!-- wp:divi/accordion {"builderVersion":"5.18.0"} -->
<!-- wp:divi/accordion-item {"module":{"advanced":{"open":{"desktop":{"value":"on"}}}},"title":{"innerContent":{"desktop":{"value":"Titel"}}},"content":{"innerContent":{"desktop":{"value":"<p>Text</p>"}}},"builderVersion":"5.18.0"} /-->
<!-- /wp:divi/accordion -->
<!-- wp:divi/button {"button":{"innerContent":{"desktop":{"value":{"text":"Hier Klicken"}}}},"builderVersion":"5.18.0"} /-->
<!-- /wp:divi/column -->
<!-- /wp:divi/row -->

<!-- wp:divi/row {"module":{"advanced":{"columnStructure":{"desktop":{"value":"1_2,1_2"}},"flexColumnStructure":{"desktop":{"value":"equal-columns_2"}}},"decoration":{"layout":{"desktop":{"value":{"flexWrap":"nowrap"}},"phone":{"value":{"flexWrap":"wrap"}},"phoneWide":{"value":{"flexWrap":"wrap"}}}}},"builderVersion":"5.18.0"} -->
<!-- wp:divi/column {"module":{"advanced":{"type":{"desktop":{"value":"1_2"}}},"decoration":{"sizing":{"desktop":{"value":{"flexType":"12_24"}},"phone":{"value":{"flexType":"24_24"}},"phoneWide":{"value":{"flexType":"24_24"}}}}},"builderVersion":"5.18.0"} -->
<!-- wp:divi/countdown-timer {"title":{"innerContent":{"desktop":{"value":"Titel"}}},"content":{"advanced":{"dateTime":{"desktop":{"value":"2026-11-27 07:57"}}}},"builderVersion":"5.18.0"} /-->
<!-- /wp:divi/column -->
<!-- wp:divi/column { ...gleiche Spalten-Angaben wie oben... } -->
<!-- wp:divi/image {"image":{"innerContent":{"desktop":{"value":{"src":"(Platzhalter, gekürzt)"}}}},"builderVersion":"5.18.0"} /-->
<!-- wp:divi/icon {"builderVersion":"5.18.0"} /-->
<!-- wp:divi/icon-list {"module":{"meta":{"adminLabel":{"desktop":{"value":"Icon List"}}}},"builderVersion":"5.18.0"} -->
<!-- wp:divi/icon-list-item {"content":{"innerContent":{"desktop":{"value":"List item text"}}},"icon":{"innerContent":{"desktop":{"value":{"unicode":"&#x21;","type":"divi","weight":"400","target":"off"}}}},"builderVersion":"5.18.0"} /-->
<!-- /wp:divi/icon-list -->
<!-- wp:divi/heading {"title":{"innerContent":{"desktop":{"value":"Titel"}}},"builderVersion":"5.18.0"} /-->
<!-- /wp:divi/column -->
<!-- /wp:divi/row -->
<!-- /wp:divi/section -->
<!-- /wp:divi/placeholder -->
```

## Nachtrag: Text, Blurb, Gruppe, Sektion mit Farbe ✅ (belegt, gleiche Seite)

Im deutschen Divi heißt das Blurb **Informationstafel**.

```
<!-- wp:divi/section {"module":{"decoration":{"background":{"desktop":{"value":{"color":"#0e0f25"}}}}},"builderVersion":"5.18.0"} -->
<!-- wp:divi/row {"module":{"advanced":{"columnStructure":{"desktop":{"value":"4_4"}},"flexColumnStructure":{"desktop":{"value":"equal-columns_1"}}},"decoration":{"layout":{"desktop":{"value":{"flexWrap":"nowrap"}}}}},"builderVersion":"5.18.0"} -->
<!-- wp:divi/column {"module":{"advanced":{"type":{"desktop":{"value":"4_4"}}},"decoration":{"sizing":{"desktop":{"value":{"flexType":"24_24"}}}}},"builderVersion":"5.18.0"} -->
<!-- wp:divi/text {"content":{"innerContent":{"desktop":{"value":"<p>Text</p>"}}},"builderVersion":"5.18.0"} /-->
<!-- wp:divi/blurb {"imageIcon":{"innerContent":{"desktop":{"value":{"src":"(Bild)"}}}},"title":{"innerContent":{"desktop":{"value":{"text":"Titel"}}}},"content":{"innerContent":{"desktop":{"value":"<p>Text</p>"}}},"builderVersion":"5.18.0"} /-->
<!-- wp:divi/group {"builderVersion":"5.18.0"} -->
  ... Module in der Gruppe ...
<!-- /wp:divi/group -->
<!-- /wp:divi/column -->
<!-- /wp:divi/row -->
<!-- /wp:divi/section -->
```

- **Hintergrundfarbe der Sektion:** `module.decoration.background.desktop.value.color`. Divi schreibt den Hex-Wert klein (`#0e0f25`).
- **Titel beim Blurb** liegt anders als beim Heading: `title.innerContent.desktop.value.text` (beim Heading direkt `value`).
- **Gruppe** ist ein eigener Block `wp:divi/group` und kann geschachtelt werden. Auf der Referenzseite ist sie durch Mehrfachklicks 4-fach geschachtelt, das ist nur Testmaterial.
- Mehrere Zeilen in einer Sektion stehen einfach hintereinander.

## Noch nicht belegt ☑️

- Schriftgrößen, Farben, Abstände als Variablen oder Voreinstellungen (Presets).
- Button-Farben und -Formen, Bildzuordnung aus der Mediathek (statt eingebettetem Platzhalter).
- Mehrere Bildschirmgrößen für Texte (tablet, phone).

## Hinweis zum Arbeiten im Builder

Die Bildschirmanzeige hinkt dem echten Zustand oft hinterher. Verlässlich ist der gespeicherte Inhalt (`content.raw` der Seite), nicht die Vorschau.

## Seiten per WordPress-Schnittstelle (REST) anlegen: Lehren (28.10.2026)

1. **Nie `<`, `>` und `&` vorab als `<` schicken.** WordPress entfernt den Backslash, im Text steht dann sichtbar `u003c`. Rohe Zeichen schicken: WordPress/Divi machen daraus beim Speichern selbst `<`. Prüfen: In `content.raw` muss `<` stehen, nicht `u003c` und nicht `\u003c`.
2. **Die Seite wird erst zur Divi-Seite, wenn `_et_pb_use_builder` = `on` gesetzt ist.** Ohne das fehlen Hintergrundfarben (Divi-CSS greift nicht). Einfachster Weg: Seite einmal im Backend mit "Den Divi Builder verwenden" öffnen.
3. **Blöcke in `<!-- wp:divi/placeholder -->` einpacken.** Ohne Platzhalter erkennt der Builder die Seite nicht sauber.
4. **Immer als Entwurf anlegen** (`status: draft`) und per `?page_id=ID&preview=true` prüfen: Farben, Schriftgröße, Links, Bilder per Skript abfragen (`getComputedStyle`).
5. **Divi-Namen im deutschen Builder:** Blurb = Informationstafel, Countdown = Countdown-Timer, Gruppe, Icon-Liste.
6. **Pfade, die sich bewährt haben** (Divi 5.18, geprüft an der Vorschau):
   - Überschrift: `title.decoration.font.font.desktop.value.{color,size,weight,headingLevel}`
   - Text: `content.decoration.bodyFont.body.font.desktop.value.{color,size}`
   - Button: `button.innerContent.desktop.value.{text,linkUrl}`, Farbe `button.decoration.background...color`, Schrift `button.decoration.font.font...`
   - Bild: `image.innerContent.desktop.value.{src,alt,linkUrl}`
   - Sektion: `module.decoration.background.desktop.value.color`, Name im Builder: `module.meta.adminLabel.desktop.value`
7. **Zeilen mit 3 und 4 Spalten** (`1_3,1_3,1_3` / `1_4,...`, `flexType` `8_24` / `6_24`) funktionieren, auch ohne Referenz aus dem Builder.
8. **Der Builder-Bildschirm hinkt hinterher.** Verlässlich ist nur `content.raw` der gespeicherten Seite.
