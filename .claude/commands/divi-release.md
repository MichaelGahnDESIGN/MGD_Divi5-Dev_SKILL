# /divi-release

Nutze die tatsächlich installierte `SKILL.md` im Stamm des Divi-Skill-Repositories,
Abschnitt `/divi-release`. Der alte Pfad `skill/DIVI5-SKILL.md` gilt nicht mehr.

1. Versionsquelle (Theme, Plugin oder Skill) und nächste freie Version bestimmen.
2. Version, Changelog und Release-Notizen abstimmen und relevante Prüfungen ausführen.
3. Änderungen nach Projektkonvention integrieren und den geprüften Commit festhalten.
4. Bei beauftragter Veröffentlichung ausgewählte Produktdateien samt Lizenzen und
   Begleit-Skills packen, prüfen und einen neuen Tag sowie GitHub-Release erstellen.
5. Release-Status, Tag/Commit und erneut heruntergeladene Paket-Prüfsumme prüfen;
   README und Wiki aktualisieren. Falls vorhanden den Release-Ablauf aus `/dev` nutzen.
6. Nur bei zusätzlichem Deploy-Auftrag: Rückfallpunkt vor Live-Änderungen prüfen,
   kontrolliert deployen und die betroffenen Seiten sichtbar prüfen.

Kein Force-Push, keine verschobenen Release-Tags, keine Secrets oder Backups im
Paket. Wartungsmodus und Zugriffsschutz erhalten. Version, Commit, Release-URL,
Paketprüfung und ein gegebenenfalls erfolgtes Deployment getrennt berichten.
