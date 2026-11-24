# Divi 5 – Kommandozentrale im Alltag und Designsystem aufbauen

Stand: 24.11.2026. Quellen: offizielle Hilfe-Artikel von Elegant Themes, praktisch am Builder geprüft (Divi 5.9 bis 5.18).
Legende: ✅ belegt · ⚠️ unsicher · ☑️ offen

Ergänzt die Docs [Werkzeuge](DIVI5-WERKZEUGE.md) (Befehlssyntax, Canvases, Schichten, Inspektor) und [Variablen, Presets, Komponenten](DIVI5-VARIABLEN-PRESETS-KOMPONENTEN.md). Hier steht, WIE man beides im Alltag sicher einsetzt.

---

## 1. Kommandozentrale: sicherer Ablauf

Öffnen: `⌘ K` (Mac), `Strg K` (Windows) oder Blitz-Symbol links. Treffer mit Pfeiltasten wählen, Enter führt aus.

| Kategorie | Wofür |
|---|---|
| Element | Sektion, Zeile, Spalte, Gruppe, Modul einfügen |
| Modal | Fenster öffnen (Schichten, Import/Export, Variablen) |
| Einstellungen | direkt zu einer Optionsgruppe springen |
| Ansicht | Drahtgitter, Breakpoints, Vorschau |
| Ändern | kopieren, einfügen, duplizieren, zurücksetzen |
| Navigation | Seiten, Theme Builder, Theme Options |
| Voreinstellung | Presets anwenden |
| Seite | speichern, Vorschau, Builder beenden |

### Neuen Bereich auf einer Seite anlegen (Schritt für Schritt)

1. Im Drahtgitter die Sektion auswählen, NACH der der neue Bereich kommen soll.
2. `⌘ K`, nach `section` suchen.
3. Den Befehl für eine leere, normale Sektion nehmen. NICHT "Layout laden" und NICHT die KI-Erstellung, wenn eine leere native Struktur gebraucht wird.
4. Danach per `row` die Zeile mit passender Spaltenstruktur anlegen.
5. Erst wenn die Struktur stimmt, Inhalte (Text, Bild, Button) ergänzen.
6. Der Sektion einen eindeutigen Admin-Namen geben, dann speichern.

✅ Elemente werden kontextbezogen eingefügt (nach, über oder in der Auswahl). Die echte Position danach immer in der Schichtenansicht prüfen.

### Regeln

- ✅ Vor jedem `Element`-Befehl zuerst die richtige Stelle auswählen. Ohne Auswahl landet das Element irgendwo im sichtbaren Bereich.
- ✅ Header, Footer und globale Vorlagen nicht aus Versehen öffnen: bei "Theme Builder" oder "Theme Options" im Befehlstext genau hinschauen.
- ✅ Nach jeder eingefügten Sektion: Schichten und Vorschau (angemeldet) prüfen.
- ✅ Einheitliche Admin-Namen helfen der Suche. Erst benennen, dann bauen.
- ⚠️ Wo ein Projekt kein eigenes CSS oder JavaScript erlaubt, nur native Elemente und Einstellungen nutzen.

---

## 2. Variablen, Presets, Bibliothek, Theme Builder

### Variablen
Speichern Farben, Zahlen, Schriften und weitere Designwerte. Einmal ändern, wirkt überall, wo verbunden. Namen nach ROLLE, nicht nach Seite:

```text
Farbe – Primär
Farbe – Text dunkel
Abstand – Sektion groß
Radius – Karte
```

### Presets
- ✅ Modul-Preset: komplette Modulgestaltung wiederverwenden.
- ✅ Option-Group-Preset: nur eine Einstellungsgruppe teilen (z. B. nur Rahmen).
- ✅ Direkte Einzelwerte überschreiben Preset-Werte. Überschreibungen bleiben mit "Geändert" sichtbar und sollten die Ausnahme sein.
- Empfohlene Rollen: Überschrift H1/H2/H3, Text Standard/Groß/Klein, Button Primär/Sekundär, Sektion Hell/Dunkel, Karte Standard/Akzent.

### Divi-Bibliothek
- ✅ Speichert Layouts, Sektionen, Zeilen, Module.
- ✅ Normale Kopie: nach dem Einfügen unabhängig.
- ✅ Globales Element: bleibt verknüpft, Änderung wirkt überall. Redakteuren klar sagen.

### Theme Builder
- ✅ Steuert Header, Footer und bedingte Templates (Seiten, Beiträge, Archive, Produkte).
- ✅ Bedingungen auf Überschneidungen prüfen.
- ✅ Native Abstände und Sichtbarkeit im Template gehen vor breitem CSS auf `.et-l--header` oder `.et-l--footer`.

---

## 3. Designsystem aufbauen (Reihenfolge)

1. Markenfarben und Kontraste festlegen.
2. Schrift und Abstandsmaßstab festlegen.
3. Variablen anlegen.
4. Kleine Preset-Sammlung nach Rollen bauen.
5. Wiederkehrende Strukturen in die Bibliothek (oder als Komponenten) legen.
6. Header und Footer im Theme Builder verwalten.
7. Nutzung dokumentieren, regelmäßig prüfen.

## 4. Typische Fehler

- Presets nach Seitenname statt Rolle benennen
- globales Element nutzen, obwohl ein unabhängiger Inhalt gebraucht wird
- lokale Einzelwerte überdecken Preset-Änderungen
- Preset löschen, ohne die Verwendungen zu prüfen
- Theme-Builder-Bedingungen überlagern sich

## 5. Prüfliste vor dem Speichern

- Namen verständlich und rollenbasiert?
- Ist klar, ob eine Bibliotheksinstanz global verknüpft ist?
- Direkte Überschreibungen ("Geändert") geprüft?
- Header und Footer auf Desktop und Mobil getestet?
- Schichtenansicht stimmt mit der geplanten Struktur überein?

## Quellen

- https://help.elegantthemes.com/en/articles/13741079-the-divi-5-command-center
- https://www.elegantthemes.com/blog/divi-resources/how-the-command-center-changes-the-divi-5-workflow
- https://www.elegantthemes.com/blog/divi-resources/divi-5-commands-every-power-user-should-know
- https://help.elegantthemes.com/en/articles/15530394-part-4-mastering-divi-5-presets-for-faster-more-consistent-web-design
- https://help.elegantthemes.com/en/articles/13616078-divi-library-in-divi-5
