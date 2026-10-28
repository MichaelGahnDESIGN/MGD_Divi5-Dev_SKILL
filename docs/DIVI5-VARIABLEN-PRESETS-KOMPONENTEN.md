# Divi 5: Variablen, Presets, Komponenten (Recherche B)

Stand: 28.10.2026. Marker: ✅ belegt, ⚠️ unsicher, ☑️ offen.
Wichtig vorab: Es gibt öffentlich nur Anwender-Doku (Hilfe-Center, Blog). Entwickler-Doku zu Datenformat, Optionsnamen und REST-Routen wurde NICHT gefunden (devdocs.elegantthemes.com ist nicht erreichbar, DNS-Fehler).

## 1. Variablenmanager (Design-Variablen)
Quelle: https://help.elegantthemes.com/en/articles/11027601-design-variables-in-divi-5

- ✅ In der Oberfläche heißen sie "Design Variables" (älter: "Global Variables"). Man legt einen Wert einmal an und nutzt ihn überall.
- ✅ Typen: Zahlen (alle CSS-Einheiten), Text (Strings), Bilder (Mediathek), Links (volle URL oder relativ), Farben, Verläufe (Gradients), Schriften.
- ✅ Globale Farben (Primary, Secondary usw.) stehen auch im Manager, sind aber nicht umbenennbar, löschbar oder sortierbar.
- ✅ Öffnen: Icon "Design Variable" in der linken Leiste oder im Feld über das Dynamic-Content-Menü > "Manage Variables".
- ✅ Anlegen: Name UND Wert nötig. Bearbeiten, Löschen, Sortieren per Drag and Drop (Sortieren braucht kein Speichern).
- ✅ Gelöschte Variablen werden bis zum Speichern archiviert, sind wiederherstellbar ("Restore Variable"). Felder mit archivierter Variable funktionieren weiter.
- ✅ Verwenden: Feld mit der Maus berühren > Dynamic-Content-Icon > Variable wählen. Im Feld erscheint ein "Chip". Klick darauf: lösen (statischer Wert), ersetzen, verwalten.
- ✅ Änderungen gelten erst nach "Save". Abbrechen verwirft sie.
- ✅ Benennung: Namen dürfen sich jederzeit ändern. Deshalb gibt es KEINE lesbaren CSS-Variablennamen (laut Hilfe-Artikel).
- ⚠️ Wie genau intern daraus CSS wird (ob z. B. --gcid-... Variablen), steht im Hilfe-Artikel nicht. Nur die Aussage "keine lesbaren CSS-Namen" ist belegt.
- ✅ Zahlen-Variablen können laut Suchergebnis auch clamp()/calc() enthalten, es gibt einen Größen-Generator (Quelle: https://www.elegantthemes.com/blog/divi-resources/everything-you-need-to-know-about-divi-5s-sizing-system). ⚠️ nur aus Suchtreffer-Text, Seite nicht geöffnet.
- ✅ Import/Export: Icon oben im Variablenmanager > Export (Dateiname vergeben, JSON-Download) bzw. Import (JSON hochladen). Eine Datei für Variablen, eine getrennte für Presets.
  Quelle: https://www.elegantthemes.com/blog/divi-resources/how-to-import-export-design-variables-in-divi-5
- ⚠️ Wie Duplikate beim Import behandelt werden: nicht dokumentiert. Export ist nur eine Momentaufnahme.
- ✅ Divi AI Agent kann feste Farben/Schriften/Abstände auf einer Seite finden und in Variablen umwandeln (nur mit Divi-AI-Abo).
- ✅ Hierarchie laut Blog: Design Variables > Option-Group-Presets > Element-Presets > Modul-Einstellungen (https://www.elegantthemes.com/blog/divi-resources/using-divi-default-presets-to-style-your-entire-site).

## 2. Preset-Manager
Quellen: https://help.elegantthemes.com/en/articles/13427552-preset-manager-and-preset-preview-systems-in-divi-5 , https://www.elegantthemes.com/blog/divi-resources/using-divi-default-presets-to-style-your-entire-site , https://www.elegantthemes.com/blog/divi-resources/how-to-stack-nest-mix-and-match-presets-in-divi-5

- ✅ Zugang: Visual-Builder-Seitenleiste. Zwei Bereiche: Element-Presets (ganze Module/Zeilen/Sektionen) und Option-Group-Presets (nur eine Einstellungsgruppe, z. B. Typografie, Button, Rahmen, Abstand).
- ✅ Funktionen: anlegen, duplizieren, löschen, per Drag and Drop sortieren (Reihenfolge erscheint im Preset-Menü des Moduls), Suche und Filter.
- ✅ Preset bearbeiten öffnet die "Preset Preview" (Live-Vorschau). Die Seite bleibt unverändert, bis man den Preset-Modus verlässt.
- ✅ Änderungen an einem Preset wirken auf ALLE Elemente, die es nutzen (also seitenübergreifend).
- ✅ Standard-Presets: Jedes Element und jede Options-Gruppe hat eins. Neue Elemente bekommen es automatisch. Ein eigenes Preset wird per Stern-Icon zum Standard. Eigene Presets werden NICHT automatisch zugewiesen, nur manuell.
- ✅ Unveränderte Standards erben Werte aus dem WordPress-Customizer (graue Werte). Verbindung nicht nötig, Hersteller empfiehlt, Standard-Presets direkt zu bearbeiten.
- ✅ Zuweisen: Option-Group-Preset: Gruppentitel berühren > Preset-Icon > wählen oder "New Preset From Current Styles". Element-Preset: oben im Einstellungsfenster Preset-Icon.
- ✅ Nesting: Ein Element-Preset speichert Option-Group-Presets als lebende Verweise (keine Kopien). Ein Option-Group-Preset kann ein anderes enthalten (z. B. Rahmen in Button in CTA). Änderungen laufen nach oben durch.
- ✅ Stacking: Mehrere Presets auf demselben Element/derselben Gruppe, Divi kombiniert sie.
- ⚠️ Nicht dokumentiert: Konfliktregel bei Stacking, maximale Tiefe.
- ✅ Import/Export: eigene JSON-Datei für alle Presets (Export enthält laut Hilfe "alle Presets und Variablen"). Anleitung: https://www.elegantthemes.com/blog/divi-resources/how-import-export-presets-in-divi-5 (nur in Suchtreffer gesehen, nicht geöffnet).
- ✅ Alles löschen: https://help.elegantthemes.com/en/articles/9910009-how-to-delete-all-presets-and-global-variables-on-a-divi-website (nur Titel gesehen, ⚠️ Inhalt nicht geprüft).

## 3. Komponenten-Manager / Components
Quellen: https://help.elegantthemes.com/en/articles/17438180-components-in-divi-5 , https://help.elegantthemes.com/en/articles/17438193-the-components-manager-in-divi-5 , https://www.elegantthemes.com/blog/divi-resources/exploring-slots-for-components-in-divi-5

- ✅ Eingeführt mit Divi 5.15 (laut Suchtreffer zu Release Notes: https://www.elegantthemes.com/blog/?p=322045 , ⚠️ nicht selbst geöffnet).
- ✅ Erstellen: Rechtsklick auf Modul/Zeile/Sektion > "Save to Library" > Name > "Save as Component" aktivieren. Oder Komponenten-Icon in den Einstellungen. Der Divi AI Agent kann auch per Text-Auftrag erstellen.
- ✅ Instanzen: Jede Kopie bleibt mit dem Original verknüpft. Änderung am Original ändert alle Kopien. Komponenten sind lila markiert (Rahmen, Toolbar, Ebenen).
- ✅ Zwei Modi: Instanz-Modus (Standard, nur diese Kopie, nur freigegebene Einstellungen) und Komponenten-Modus (ändert alle, mit Bestätigung "alle Instanzen werden aktualisiert").
- ✅ "Eigenschaften" (Props) im Figma-Sinn: Es gibt den Begriff nicht. Das Gegenstück heißt "Make Editable on Instances" (selektive Synchronisation): Einstellung freigeben, jede Kopie startet mit dem Wert der Komponente und darf abweichen. Funktioniert auch für Sektionen und Zeilen.
- ✅ Slots: Ein Slot-Modul in der Komponente ist ein Platzhalter für seitenspezifische Inhalte. Mehrere Slots pro Komponente möglich, Slot kann eine verschachtelte Komponente enthalten, aber nicht in einem anderen Slot oder Karussell-Slide stehen. Slot entfernen entfernt den Bereich in allen Instanzen.
- ✅ Verschachteln: Komponenten in Komponenten erlaubt, nicht in sich selbst.
- ✅ Lösen (Detach): einzelne Instanz oder ein Modul darin lösen, später wieder verbinden.
- ✅ Unterschied zu globalen Modulen: Globale Module sind jetzt Komponenten und werden automatisch umgewandelt. Neu: Kopien behalten Werte bei ausgewählten Einstellungen, Auswahl auch für Sektionen/Zeilen, eigener Bearbeitungsmodus, kein Lade-Spinner.
- ✅ Unterschied zur Bibliothek: Komponenten liegen in der Divi-Bibliothek (Library) und werden dort gespeichert, sind aber verknüpft, normale Bibliothekselemente sind Kopien. ⚠️ Das "Kopie vs. verknüpft" ist aus dem Verhalten abgeleitet, nicht als Satz belegt.
- ✅ Components Manager (Seitenleiste): Liste nach Elementtyp gruppiert (Button, Blurb, Zeilen, Sektionen), Suche, bearbeiten (Vorschau in Desktop-Breite, "Component Title" umbenennen), duplizieren ("Name Copy"), sortieren, löschen, Import/Export.
- ✅ Löschen wandelt Instanzen NICHT um, sie rendern evtl. nicht mehr. Vorher ersetzen oder lösen.
- ✅ Export: eine .json mit Komponenten plus deren Presets, globalen Farben und Variablen. Import nutzt vorhandene Komponenten mit gleichem Namen + Typ wieder (kein Überschreiben/Duplizieren).
- ✅ Rechte: "Edit Global Items" im Rollen-Editor plus Divi-Library-Rechte.
- ☑️ Offen: Datenmodell (Post-Type, Verweis im Block) nicht dokumentiert.

## 4. Speicherung / Datenformat (Entwickler-Ebene)
- ⚠️ In der offiziellen Anwender-Doku NICHT dokumentiert: WordPress-Optionsnamen für Presets/Variablen, REST-Routen unter divi/v1, Block-Schlüssel.
- ⚠️ Einzige Fundstelle (Drittanbieter, kein Hersteller, Seite nicht abrufbar, nur Suchtreffer-Auszug von claudepluginhub.com "divi-5-builder"): Variablen-Verweise im Block-JSON als `$variable({...JSON-Payload...})$` (Payload vollständig, das End-`$` wichtig); Presets per UUID über `modulePreset` oder `groupPreset.<slot>.presetId`. Der Name ist dort Singular `groupPreset`, nicht `groupPresets`. Attribut-Baum entspricht dem Block-Markup (z. B. `module.decoration`, `content`).
- ☑️ Offen/zu prüfen direkt auf der Kundenseite: Block-Markup einer Divi-5-Seite ansehen, Tabelle wp_options nach Einträgen mit "et_" / "divi" durchsuchen, REST-Routen via /wp-json/ (Namespace divi/v1) auflisten. Das wäre die verlässliche Quelle, nicht die Doku.
- ⚠️ Release-Notes 5.0 bis 5.18 wurden aus Token-Spargründen nicht einzeln durchgesehen. Struktur der Daten kann sich zwischen Versionen geändert haben.

## Weitere Quellen (nur Titel gesehen)
- https://www.elegantthemes.com/blog/divi-resources/using-design-variables-with-presets-in-divi-5
- https://www.elegantthemes.com/blog/divi-resources/exploring-components-in-divi-5
- https://help.elegantthemes.com/en/articles/17438185-how-to-create-a-component-in-divi-5
- https://help.elegantthemes.com/en/articles/17438188-how-to-edit-a-component-in-divi-5
