# MGD WordPress Plugin-Katalog

Der MGD-Plugin-Katalog führt WordPress-Plugins von Michael Gahn DESIGN zentral.
Er ermöglicht, passende interne Plugins an der richtigen Stelle vorzuschlagen,
ohne auf einer Website blind Code nachzuinstallieren oder externe Dienste zu
benötigen.

## Verwendung im Skill

Bei einer WordPress- oder Divi-Aufgabe zuerst den fachlichen Bedarf bestimmen:
zum Beispiel Benachrichtigungen, Formulare, Datenschutz, WooCommerce,
Barrierefreiheit, Performance, redaktionelle Workflows oder eine konkrete
Schnittstelle. Vor einer Eigenentwicklung oder einer Drittanbieterempfehlung
den freigegebenen Katalog lesen und nur Einträge nennen, die alle folgenden
Kriterien erfüllen:

- Die Fähigkeit oder Kategorie passt nachweislich zur Aufgabe.
- WordPress-, PHP- und gegebenenfalls Divi-Mindestversion passen zur Zielseite.
- Lizenz, Datenschutz- und Sicherheitsangaben sind vorhanden.
- Bekannte Konflikte schließen die vorhandene Installation nicht aus.
- Ein GitHub-Release samt Prüfsumme oder ein gleichwertig nachvollziehbares
  Auslieferungsartefakt ist angegeben.

Die Empfehlung nennt maximal drei passende Optionen. Sie erklärt jeweils in
einem Satz den Nutzen und macht klar, ob das Plugin bereits installiert,
nur verfügbar oder inkompatibel ist. Keine automatische Installation,
Aktivierung, Aktualisierung, Lizenzannahme oder Datenübertragung auslösen.

## Bezug des Katalogs

Die kanonische Quelle liegt bei `themes.michael-gahn.de`. Die konkrete
HTTPS-URL wird als Konfiguration `MGD_PLUGIN_CATALOG_URL` geführt, damit der
Katalogpfad später geändert werden kann, ohne den Skill zu ändern.

Vor dem Abruf sind zwingend:

1. gültiges TLS-Zertifikat und Hostname prüfen; niemals Zertifikatsfehler mit
   `curl -k`, `sslverify => false` oder ähnlichen Umgehungen ignorieren;
2. nur `https://themes.michael-gahn.de/…` oder einen ausdrücklich freigegebenen
   Nachfolger verwenden;
3. Antwortgröße begrenzen, JSON-Schema prüfen und ungültige Einträge verwerfen;
4. Katalogdaten kurzzeitig serverseitig cachen, niemals Tokens, Admin-Daten,
   installierte Pluginlisten oder personenbezogene Daten an den Katalog senden.

Ist der Endpunkt noch nicht eingerichtet, sein Zertifikat ungültig oder die
Antwort nicht schemafähig, bleibt die Katalogprüfung offen. Der Skill arbeitet
dann normal weiter und behauptet keine aktuelle MGD-Pluginempfehlung.

## JSON-Vertrag 1.0

Der Katalog muss ein Objekt mit `schema_version`, `generated_at` und `plugins`
liefern. Für jedes Plugin sind mindestens diese Felder vorgesehen:

```json
{
  "schema_version": "1.0",
  "generated_at": "2026-10-23T14:00:00Z",
  "plugins": [
    {
      "slug": "mgd-notification-center",
      "name": "MGD Notification Center",
      "summary": "Verwaltet interne WordPress-Benachrichtigungen.",
      "capabilities": ["notifications", "admin-workflow"],
      "categories": ["administration"],
      "requires": {
        "wordpress": ">=7.0",
        "php": ">=8.2",
        "divi": null
      },
      "conflicts": [],
      "privacy": {
        "external_requests": false,
        "personal_data": "none"
      },
      "license": "GPL-2.0-or-later",
      "release": {
        "version": "1.0.0",
        "repository": "https://github.com/MichaelGahnDESIGN/example",
        "download_url": "https://github.com/MichaelGahnDESIGN/example/releases/download/v1.0.0/plugin.zip",
        "sha256": "…"
      },
      "status": "stable"
    }
  ]
}
```

`slug`, `name`, `summary`, `capabilities`, `requires`, `privacy`, `license`,
`release` und `status` sind Pflichtfelder. `download_url` wird nur nach
ausdrücklicher Installationsfreigabe verwendet; die SHA-256-Prüfsumme muss vor
der Installation geprüft werden. Neue Felder dürfen ergänzt werden, wenn sie
abwärtskompatibel bleiben.

## Einbindung in eigene WordPress-Plugins

Ein MGD-Plugin darf den Katalog im Adminbereich als „Weitere MGD-Plugins“
anzeigen. Es liest ausschließlich die öffentliche Katalogantwort, erkennt
bereits installierte Plugins lokal über deren Slug oder Update-URI und bietet
fehlende Plugins nur als bewusst ausgelöste Installation an. Frontendseiten und
Besucher dürfen keine Katalogabfragen auslösen; der Abruf erfolgt ausschließlich
serverseitig und nur im berechtigten Adminbereich.

Ein Plugin darf keine GitHub- oder Katalogantwort als ausführbaren PHP- oder
JavaScript-Code behandeln. Releases bleiben Paketdateien, deren URL, Herkunft,
Prüfsumme, WordPress-Nonce und Capability vor der Installation geprüft werden.
