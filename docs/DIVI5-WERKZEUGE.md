# Divi 5 – Werkzeuge im Visual Builder (Recherche)

Stand der Recherche: 28.10.2026. Quellen: offizielle Hilfe-Artikel und Blog von Elegant Themes.
Legende: ✅ belegt (steht in der Quelle) · ⚠️ unsicher / nicht eindeutig belegt · ☑️ offen (nicht gefunden, muss geprüft werden)

---

## 1. Kommandozentrale (Command Center)

**Was ist das?** Eine Suchleiste im Visual Builder. Man tippt, was man tun will, und drückt Enter.

- ✅ Öffnen: **Cmd+K** (Mac) bzw. **Strg+K** (Windows), oder Klick auf das Blitz-Symbol in der linken Leiste.
- ✅ Tippen filtert die Liste, **Enter** führt den Treffer aus.
- ✅ Kategorien: Element, Modal, Settings, View, Modify, Navigate, Preset, Page.
- ✅ Kategorie-Filter: Doppelpunkt plus Kategorie, z. B. `:modal`.
- ✅ **Elemente einfügen:** Name tippen (z. B. „button") + Enter. Wo es landet, hängt von der Auswahl ab:
  - Modul markiert: danach eingefügt.
  - Zeile markiert: neue Zeile, darin das Modul.
  - Section markiert: neue Section + Zeile + Modul.
  - Nichts markiert: je nach Modul im sichtbaren Bereich.
- ✅ **Mehrfach:** `button * 2` fügt zwei Buttons ein.
- ✅ **Warteschlange:** Cmd/Strg+Enter legt Befehle in die Queue, danach Enter führt alle aus (gilt für Elemente und Presets).
- ✅ **Operatoren:** `>` verschachtelt (z. B. `blurb > button`), `^` fügt über dem markierten Element ein, `+` hängt ein Preset an (z. B. `button + Primary Preset`).
- ✅ **Presets:** Preset-Namen tippen und Enter = anwenden.
- ✅ **Einstellungen:** Namen einer Optionsgruppe tippen („animation", „border", „interactions") springt direkt im Einstellungs-Panel dorthin.
- ✅ **Fenster (Modals):** z. B. „variables" oder „export" öffnet das jeweilige Fenster.
- ✅ **Modify-Befehle:** duplicate, delete, copy, cut, paste, reset.
- ✅ **Navigation:** Seitenname tippen = Seite bearbeiten; auch „Theme Builder", „Theme Options".
- ✅ **Ansicht:** Desktop / Phone / Wireframe umschalten.
- ✅ Weitere Beispiele: `canvas grid` (Canvas-Übersicht), `layers`, `inspector` (Panels öffnen), `hover state` / `default state`, `save` (Schnellspeichern ohne Statuswechsel; Varianten: Entwurf, Ausstehend, Privat).
- ✅ Tipp: Einheitliche „Admin Labels" (Namen der Elemente) vergeben, dann findet die Suche sie besser.
- ✅ Divi AI Agent: Alternative, man beschreibt in normalen Worten, der Agent baut; bei zerstörerischen Änderungen fragt er nach.
- ⚠️ „Einfügen" im Sinne von Inhalt aus der Zwischenablage: Die Doku nennt nur den Modify-Befehl „paste". Details nicht beschrieben.
- ☑️ Vollständige Befehlsliste: nicht gefunden. Im Builder selbst durchblättern.

Quellen:
- https://help.elegantthemes.com/en/articles/13741079-the-divi-5-command-center
- https://www.elegantthemes.com/blog/divi-resources/divi-5-commands-every-power-user-should-know
- https://www.elegantthemes.com/blog/divi-resources/everything-you-need-to-know-about-the-command-center-in-divi-5
- https://www.elegantthemes.com/blog/divi-resources/effectively-navigate-content-in-divi-5-new-shortcuts-content-drill-down

---

## 2. Canvases (Canvas)

**Was ist das?** Ein Canvas ist ein eigener Arbeitsbereich auf derselben Seite oder Vorlage, getrennt vom normalen Seiteninhalt. Gut für Off-Canvas-Menüs, Popups, Mega-Menüs und Testversionen.

- ✅ **Haupt-Canvas (Main Canvas):** enthält den sichtbaren Seiteninhalt. Andere Canvases sind davon abgekoppelt, bis man sie verbindet.
- ✅ **Lokal vs. global:** Lokale Canvases gehören zu einer Seite/Vorlage, globale kann man auf der ganzen Website wiederverwenden.
- ✅ **Anlegen und Wechseln:** über das **Canvas-Dropdown** oben im Visual Builder (neu anlegen, wechseln, als global markieren, festlegen welche Canvases automatisch im Frontend angehängt werden).
- ✅ **Canvas Grid View:** Übersicht aller Canvases der Seite. Wechseln, Rechtsklick (bearbeiten, duplizieren, exportieren, löschen), beliebigen Canvas zum Haupt-Canvas machen. Auch über Kommandozentrale: `canvas grid`.
- ✅ **Testumgebung (Staging):** Haupt-Canvas duplizieren, Kopie bearbeiten, wenn fertig als Haupt-Canvas festlegen.
- ✅ **Off-Canvas-Menüs und Popups:** Auf eigenen Canvases speichern. Im Haupt-Canvas per **Interaktion** (Interaction Builder) ein-/ausblenden, z. B. Klick auf ein Header-Icon oder Scroll-Trigger (Viewport). Ein anvisierter Canvas wird im Frontend automatisch an den Haupt-Canvas angehängt.
- ✅ **Canvas Portal Modul:** zeigt einen Canvas an einer bestimmten Stelle im Layout oder Theme-Builder-Template (statt automatisches Anhängen). Beispiel: Mega-Menü innerhalb eines Textmoduls mit Link.
  - Content: Canvas wählen, Link, Background, Meta (Label und Sichtbarkeit im Builder).
  - Design: Sizing, Spacing, Border, Box Shadow, Filters, Transform, Animation.
  - Advanced: Attribute (ID, Klassen), CSS, HTML-Tag, Conditions, Interactions, Sichtbarkeit pro Gerät, Transitions, Position, Scroll Effects.
  - Der Canvas kann nicht direkt im Portal bearbeitet werden, sondern über Canvas Grid View oder Canvas-Dropdown. Änderung am Quell-Canvas wirkt überall, wo er per Portal erscheint.
- ✅ Veröffentlichung der Canvas-Funktion im Blog: 23.12.2025. Die Version (5.x) wird im Artikel nicht genannt.
- ✅ Divi AI Agent kann Canvases anlegen, global machen und befüllen.
- ⚠️ Genaue Divi-5-Versionsnummer für Canvases: nicht belegt (Release Notes 5.0 bis 5.18 nicht einzeln geprüft).
- ☑️ Konkrete Interaktions-Einstellungen („Cross-Canvas"-Anleitung) nicht im Detail gelesen. Siehe Links unten.

Quellen:
- https://help.elegantthemes.com/en/articles/13249775-divi-5-canvases-off-canvas-menus-popups-canvas-portals
- https://help.elegantthemes.com/en/articles/14718409-the-canvas-portal-module-in-divi-5
- https://www.elegantthemes.com/blog/theme-releases/divi-canvases
- https://www.elegantthemes.com/blog/divi-resources/everything-you-need-to-know-about-canvases-in-divi-5
- https://www.elegantthemes.com/blog/divi-resources/everything-you-need-to-know-about-the-canvas-portal-module-in-divi-5
- https://www.elegantthemes.com/blog/divi-resources/how-to-create-cross-canvas-interactions-in-divi-5
- https://www.elegantthemes.com/blog/divi-resources/how-to-use-interactions-canvases-and-portals-together

---

## 3. Schichten (Layers View) und Wireframe

**Layers View**
- ✅ Baumansicht von Sections, Rows, Columns und Modulen in der linken Leiste. Hilft bei vollen Layouts: auswählen, umbenennen, Struktur umbauen.
- ✅ Öffnen: Layers-Symbol in der linken Leiste, oder Kommandozentrale `layers`.
- ✅ Auswahl in Layers = Auswahl auf der Seite. Rechtsklick-Menü und Tastenkürzel wirken auf diese Auswahl.
- ✅ Multi-Auswahl auch hier (siehe Abschnitt 5).
- ✅ Panels lassen sich andocken, als Tabs gruppieren oder schweben lassen (laut Interface-Beschreibung).
- ⚠️ Folgende Details stammen aus dem **Divi-4-Artikel** (Dez. 2023) und gelten für Divi 5 nicht sicher: Suche und Filter nach Elementtyp, alles auf-/zuklappen, Umbenennen per Klick + Enter, Drag & Drop, Menü mit „Disable" und „Lock", „Go to layer" per Rechtsklick. Das Drag & Drop und Rechtsklick in Layers wird in Divi-5-Quellen ebenfalls erwähnt.
- ⚠️ Alte Multi-Auswahl-Tasten aus Divi 4 (Shift + Option/Ctrl bzw. Shift + Cmd/Alt): gelten für Divi 5 laut neuer Doku NICHT, dort Cmd/Strg+Klick und Shift+Klick.

**Wireframe-Ansicht**
- ✅ Einschalten: Wireframe-Symbol in der linken Leiste (oder Kommandozentrale, View). Kann auch als Standardansicht beim Öffnen eingestellt werden (Desktop, Tablet, Phone oder Wireframe).
- ✅ Zeigt Module, Zeilen und Sections als beschriftete Blöcke ohne Styling. Gut zum Finden, Umordnen und Umbenennen.
- ⚠️ Tastenkürzel für Wireframe: in der Doku nicht genannt.

Quellen:
- https://help.elegantthemes.com/en/articles/12991185-divi-5-visual-builder-interface
- https://help.elegantthemes.com/en/articles/10469465-wireframe-view-in-divi-5
- https://help.elegantthemes.com/en/articles/8662395-using-the-divi-layers-view (Divi 4!)
- https://help.elegantthemes.com/en/articles/17633664-multi-select-and-bulk-editing-in-divi-5
- https://www.elegantthemes.com/blog/divi-resources/part-2-exploring-every-aspect-of-the-divi-5-interface

---

## 4. Inspektor (Style Inspector)

**Was ist das?** Ein Panel, das alle Stile, Inhalte und Presets einer Seite oder eines Elements an einem Ort zeigt. Man kann direkt dort ändern.

- ✅ Öffnen: Inspector-Symbol in der linken Leiste, oder Kommandozentrale `inspector`.
- ✅ Nichts markiert = Überblick für die ganze Seite. Section/Row/Modul markiert = nur dieses Element.
- ✅ **Tab Styles:** Farben (globale zuerst, nach Nutzung sortiert, dann statische), Zahlen, Schriften, Schriftstärken. Mit der Maus darüber sieht man, welche Felder den Wert nutzen.
- ✅ **Tab Content:** Medien (z. B. Hintergrundbilder), Code (eigenes CSS), Attribute (IDs, Klassen, Alt-Text, Titel), Text.
- ✅ **Tab Presets:** benutzte Modul- und Optionsgruppen-Presets.
- ✅ Änderungen gelten sofort für den aktuellen Bereich (Seite oder markiertes Element).
- ✅ Der Divi AI Agent kann ähnlich prüfen und vorschlagen, Wiederholungen in Variablen und Presets zu bündeln.
- ✅ Inspector funktioniert auch mit mehreren markierten Elementen; „Inspect" per Rechtsklick gibt es bei Mehrfachauswahl nicht.
- ✅ Element-Auswahl/Navigation: Breadcrumbs im Einstellungs-Panel (Page, Section, Row, Column, Module) sind klickbar; „Content Drill Down"-Menü am Ende der Breadcrumbs geht abwärts in Kind-Elemente. Pfeiltasten: links/rechts Eltern/Kind, hoch/runter Nachbarn im selben Container.
- ✅ Einstellungen-Suche: Das rechte Einstellungs-Panel hat Suche und Filter. (Spezifische Tastenkürzel dafür nicht belegt.)
- ✅ Einstellungen kopieren/einfügen: Tastenkürzel **Alt+Cmd/Strg+C** (Design-Einstellungen kopieren) und **Alt+Cmd/Strg+V** (einfügen); Rechtsklick-Menü „Copy Attributes" (All, Design, Style, Content, Presets) und „Extend Attributes".
- ⚠️ Kopieren/Einfügen direkt im Inspector: Der Artikel erwähnt es nicht.

Quellen:
- https://help.elegantthemes.com/en/articles/12457386-style-inspector-in-divi-5
- https://help.elegantthemes.com/en/articles/12991185-divi-5-visual-builder-interface
- https://www.elegantthemes.com/blog/divi-resources/effectively-navigate-content-in-divi-5-new-shortcuts-content-drill-down

---

## 5. Tastenkürzel, Multi-Auswahl, Rechtsklick, Gruppen

**Tastenkürzel (Windows / Mac)** – komplette Liste im Builder mit **Shift + ?**
- ✅ Speichern: Strg+S / Cmd+S · Als Entwurf: Strg+Shift+S / Cmd+Shift+S
- ✅ Rückgängig: Strg+Z / Cmd+Z · Wiederholen: Strg+Y / Cmd+Shift+Z
- ✅ Builder verlassen: Strg+E / Cmd+E · Zoom: Strg/Cmd + Plus/Minus
- ✅ Seiteneinstellungen: O · Portabilität (Import/Export): P · Shortcut-Hilfe: ?
- ✅ Kopieren/Ausschneiden/Einfügen: Strg/Cmd + C / X / V
- ✅ Design-Einstellungen kopieren/einfügen: Alt + Strg/Cmd + C / V
- ✅ Element duplizieren: Strg/Cmd + Shift + D · Löschen: Strg/Cmd + Backspace
- ✅ Layout (Tasten nacheinander): R+1..4 = Zeile mit 1 bis 4 Spalten · R+F = Zeile Fullwidth · S+1 = Section mit einer Zeile · C+1..4 = Spaltenstruktur ändern
- ✅ Esc: Inline-Textbearbeitung beenden
- ✅ Cmd+K / Strg+K: Kommandozentrale · Cmd+Enter: Befehl in Queue
- ✅ Cmd+Punkt (Mac): Vorschau-Modus verlassen (andere Systeme: Anzeige im Builder)
- ✅ Pfeiltasten: Navigation zwischen Eltern/Kind/Nachbar (siehe Abschnitt 4)

**Multi-Auswahl und Mehrfachbearbeitung**
- ✅ Auswahl auf der Seite oder in Layers.
- ✅ Cmd/Strg+Klick: einzelne Elemente hinzufügen/entfernen · Shift+Klick: Bereich (nur gleicher Eltern-Container) · Cmd/Strg+A: alles im Container des Elements unter der Maus · Cmd/Strg+D: Auswahl aufheben.
- ✅ Aktionen für die ganze Auswahl: verschieben (Ziehen, Cmd/Strg+Hoch/Runter, Rechtsklick), kopieren, ausschneiden, einfügen, duplizieren, löschen, sperren/entsperren, Attribute zurücksetzen/einfügen, Element hinzufügen, Komponente lösen.
- ✅ Einstellungs-Panel ändert alle markierten Elemente (auch responsive/Hover). Unterschiedliche Werte zeigen „Mixed".
- ✅ Presets: für die ganze Auswahl hinzufügen, entfernen, leeren, erstellen.
- ✅ Grenzen: Gesperrte Elemente werden übersprungen; Bereichsauswahl nur im selben Eltern-Element; im Theme Builder nicht über Template-Bereiche hinweg; Kopieren/Ausschneiden nur wenn alle denselben Typ haben; Copy Attributes, Extend Attributes, Inspect, In Bibliothek speichern, Als Komponente speichern gehen nicht bei Mehrfachauswahl; Attributes, Interactions, Conditions zeigen kein „Mixed" (einzeln bearbeiten).
- ⚠️ Ab welcher Divi-5-Version Multi-Auswahl da ist: nicht in der Doku genannt.

**Gruppen**
- ✅ Cmd/Strg+G packt markierte Module in ein **Group-Modul**. Nur Module können gruppiert werden.
- ✅ Rechtsklick auf Gruppen: Attribute kopieren/einfügen, Extend Attributes, Presets, Sperren, Deaktivieren.

**Rechtsklick-Menü (je nach Element)**
- ✅ Section/Row/Column: kopieren, einfügen, verschieben, deaktivieren, sperren, „Save to Library".
- ✅ Module: Attribute kopieren/einfügen, Extend Attributes, Presets, sperren, deaktivieren.
- ✅ Verschachtelte Module: Layouts und Stile innerhalb von Container-Modulen kopieren.
- ✅ Felder/Optionsgruppen: Reset, Stile kopieren/einfügen in kleinerem Umfang.
- ✅ Allgemein: Undo/Redo, Copy Attributes (All, Design, Style, Content, Presets). **Extend Attributes** überträgt Änderungen auf passende Elemente im gewählten Bereich (Section, Row, Seite).
- ✅ Nur Administratoren können sperren/entsperren.

Quellen:
- https://help.elegantthemes.com/en/articles/12992094-divi-5-visual-builder-keyboard-shortcuts
- https://help.elegantthemes.com/en/articles/12992238-divi-5-visual-builder-right-click-contextual-menus
- https://help.elegantthemes.com/en/articles/17633664-multi-select-and-bulk-editing-in-divi-5
- https://www.elegantthemes.com/blog/theme-releases/multi-select-and-bulk-editing
- https://www.elegantthemes.com/blog/divi-resources/effectively-navigate-content-in-divi-5-new-shortcuts-content-drill-down

---

## Offen / nicht geprüft
- ☑️ Release Notes 5.0 bis 5.18 nicht einzeln durchgesehen (Versionszuordnung Canvases, Multi-Auswahl, Command Center).
- ☑️ YouTube-Beschreibungen nicht genutzt (nicht nötig).
- ⚠️ Hilfe-Artikel liegen unter help.elegantthemes.com (die Doku zieht dorthin um); frühe Alpha/Beta-Artikel können abweichende Beschriftungen haben.
