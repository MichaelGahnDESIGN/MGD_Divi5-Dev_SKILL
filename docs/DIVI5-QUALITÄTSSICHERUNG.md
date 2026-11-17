# Qualitätssicherung für Divi 5

Diese Referenz ergänzt die bestehenden Build-, Debug- und Optimierungsabläufe. Sie ist
kein Ersatz für eine fachliche Abnahme oder einen Test auf realen Geräten.

## Grundsatz

Das Ergebnis einer Prüfung erhält immer genau einen Evidenzstatus:

| Status | Bedeutung |
| --- | --- |
| Bestätigt | Im Browser oder auf dem Zielgerät sichtbar geprüft. |
| Risikoanalyse | Aus Struktur, Einstellungen oder CSS abgeleitet; nicht visuell bestätigt. |
| Offen | Zugriff, Testdaten oder Freigabe fehlen. |

Nur den Status **Bestätigt** als bestanden bezeichnen. Screenshots, URL und verwendete
Viewport-Größe gehören in den Arbeitsbericht, wenn sie verfügbar sind. Keine Prüfung
darf eigenständig veröffentlichen, Caches leeren oder produktive Inhalte verändern.

## `/divi-validate`: Qualitätsprüfung

1. **Ausgangslage erfassen:** Ziel-URL, WordPress-/Divi-Version, Seitenstatus,
   relevante Plugins, Cache-Ebene und vorhandene Custom-CSS/-JavaScript notieren.
2. **Struktur prüfen:** genau eine H1, sinnvolle H2/H3-Hierarchie, semantische
   Bereiche und keine leeren Überschriften oder Links. Native Divi-Module, Variablen
   und Presets bevorzugen; Code-Module nur auf den beauftragten Zweck begrenzen.
3. **Zugänglichkeit prüfen:** sichtbarer Tastaturfokus, ausreichender Kontrast,
   verständliche Link- und Buttontexte, Alt-Texte für informative Bilder,
   dekorative Bilder korrekt leer sowie `prefers-reduced-motion` für zusätzliche
   Animationen. Automatische Tools sind Hinweise, keine WCAG-Freigabe.
4. **Inhalte und Medien prüfen:** echte Ziel-URLs, keine Platzhalter, Bildformate und
   Größen passend zum Darstellungsbereich, keine unzulässigen externen Assets oder
   Schrift-CDNs ohne Freigabe.
5. **Performance-Risiken prüfen:** übergroße Bilder, blockierende Skripte,
   unnötige Drittanbieter, mehrere Animationen auf derselben Fläche, Layoutsprünge
   durch fehlende Bildmaße sowie Cache-Konflikte. Messwerte nur mit dokumentiertem
   Messwerkzeug und Testzeitpunkt behaupten.
6. **Cache und Builder:** nach gespeicherten Änderungen nur den betroffenen Cache
   über den autorisierten Projektablauf leeren. Anschließend Frontend und – soweit
   möglich – einen erneuten Speichervorgang im Visual Builder prüfen.

## `/divi-responsive`: Viewport-Matrix

Für sichtbare Tests diese Größen verwenden: 360×800, 390×844, 414×896, 768×1024,
820×1180, 1024×768, 1280×800, 1440×900 und 2560×1440. Zusätzlich 1 Pixel vor und
nach einem verwendeten Divi-Breakpoint prüfen, wenn eine Regel dort umschaltet.

Pro Ansicht prüfen:

- Keine horizontale Scrollleiste oder abgeschnittene Elemente.
- Navigation, Formulare, Popups und interaktive Elemente sind erreichbar und
  ausreichend groß bedienbar.
- Spalten, Gruppen, Bilder, Textlängen und Abstände bleiben lesbar; keine
  überlagerten oder unerwartet gestapelten Bereiche.
- Fokus, Hover-Alternativen und Animationen beeinträchtigen die mobile Bedienung
  nicht. Hover-only-Inhalte benötigen eine Touch-Alternative.
- Header, eigenes Menü, Footer und relevante Theme-Builder-Vorlagen kontrollieren,
  da sie häufig seitenübergreifend wirken.

Ohne Browserzugriff nur typische Risiken dokumentieren – etwa feste Breiten,
`100vw`-Überläufe, absolute Positionierung, ungebrochene lange Wörter oder
Desktop-only Hover-Interaktion – und den sichtbaren Test offen lassen.
