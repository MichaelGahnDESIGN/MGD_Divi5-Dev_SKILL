# /divi-validate

Prüfe eine Divi-5-Seite nachweisorientiert, ohne selbst Inhalte zu veröffentlichen,
Caches zu leeren oder produktive Daten zu verändern.

## Ablauf

1. Ziel-URL, Seitenstatus, WordPress-/Divi-Version, vorhandenes Custom-CSS/-JavaScript
   und Cache-Ebenen erfassen.
2. Struktur prüfen: eine H1, logische Überschriftenfolge, semantische Bereiche,
   keine leeren oder irreführenden Links. Native Divi-Module, Variablen und Presets
   gegenüber Code-Modulen bevorzugen.
3. Zugänglichkeit prüfen: Kontrast, Tastaturfokus, verständliche Link-/Buttontexte,
   Alt-Texte, Dekorationsbilder und reduzierte Bewegung bei Zusatzanimationen.
4. Medien und Inhalte prüfen: gültige Links, keine Platzhalter, passende Bildmaße,
   keine nicht freigegebenen externen Assets oder Schrift-CDNs.
5. Performance-Risiken prüfen: übergroße Medien, Layoutsprünge, blockierende Skripte,
   Drittanbieter, zu viele gleichzeitige Animationen und Cache-Konflikte.
6. Sichtbare Frontend- und Visual-Builder-Prüfung nur ausführen, wenn Zugriff und
   Auftrag dafür vorliegen.

## Ergebnis

Jeden Befund als **Bestätigt**, **Risikoanalyse** oder **Offen** markieren. Nur
Browser- oder Geräteprüfungen gelten als bestätigt. Messwerte ausschließlich mit
Testwerkzeug, Zeitpunkt und Testziel angeben. Konkrete Korrekturvorschläge nach
Priorität nennen, aber nicht automatisch anwenden.

Details: `docs/DIVI5-QUALITÄTSSICHERUNG.md`.
