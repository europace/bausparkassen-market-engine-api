# bausparkassen-me-api
Market Engine-API für Bausparkassen

## API Version

Die Version der API orientiert sich am [Semantic Versioning](https://semver.org/) und hat das Format

`MAJOR.MINOR.PATCH`

und ist in der [Swagger Definition](https://github.com/europace-privatkredit/bausparkassen-me-api/blob/master/swagger.yml) enthalten (`info.version`).

1. die `MAJOR` Version wird erhöht bei API inkompatiblen Änderungen (z.B. neue Pflichtangaben)
2. die `MINOR` Version wird erhöht bei abwärtskompatiblen API Änderungen (z.B. neue optionale Angaben)
3. die `PATCH` Version wird erhöht, wenn die API gleich bleibt, jedoch die Swagger Definition angepasst wird (z.B. Erweiterung oder Anpassung von Beschreibungen in der API)

Die aktuelle Version der API ist jeweils in den [Releases](https://github.com/europace-privatkredit/bausparkassen-me-api/releases) zu finden.

## Beispiel `bonitaetscheck`

### Minimales Angebot

Angabe von
- Kreditbetrag
- Laufzeit
- Wohnart (im eigenen Haus)
- Einkommen

<details><summary>Request</summary>
<p>

```json
{
  "antragsteller": [
    {
      "id": "...",
      "persoenlicheAngaben": {},
      "derzeitigeBeschaeftigung": {
        "beschaeftigungsverhaeltnis": "ANGESTELLT",
        "beruf": "Angestellter",
        "anschrift": {}
      },
      "vorherigeBeschaeftigung": {
        "anschrift": {}
      },
      "derzeitigeWohnsituation": {
        "wohnart": "IM_EIGENEN_HAUS",
        "wohnhaftSeit": "2000-01-01",
        "anschrift": {
          "land": "DE"
        }
      },
      "kontakt": {},
      "herkunft": {},
      "rentenversicherung": {
        "anschrift": {}
      },
      "bonitaetsangaben": {
        "ausgaben": {},
        "einnahmen": {
          "monatlicheEinnahmen": {
            "regelmaessigesUnselbstaendigesEinkommen": 3000,
            "mietUndPachteinnahmen": {}
          },
          "jaehrlicheEinnahmen": {
            "einkommenAusSelbstaendigkeit": {
              "zuVersteuerndesEinkommen": {},
              "einkommenssteuer": {},
              "abschreibungen": {}
            }
          }
        },
        "vermoegen": {
          "immobilien": []
        },
        "verbindlichkeiten": {
          "ratenkredite": [],
          "sonstigeVerbindlichkeiten": [],
          "leasings": [],
          "kreditkarten": [],
          "dispositionskredite": [],
          "immobiliendarlehen": [],
          "geschaeftskredite": [],
          "kontokorrentkredite": []
        }
      }
    }
  ],
  "gemeinsameAntragstellerangaben": {
    "bonitaetsangaben": {}
  },
  "finanzierungswunsch": {
    "kreditwunsch": {
      "finanzierungszweck": "MODERNISIERUNG_UND_WOHNEN",
      "auszahlungsbetrag": 25000,
      "ratenzahlungstermin": "ULTIMO",
      "laufzeitInMonaten": 60
    },
    "versicherungsWunsch": [],
    "konto": {
      "kontoinhaberIds": []
    },
    "abzuloesendeVerbindlichkeiten": {
      "ratenkredite": [],
      "sonstigeVerbindlichkeiten": [],
      "kreditkarten": [],
      "dispositionskredite": [],
      "geschaeftskredite": []
    },
    "fahrzeug": {}
  },
  "kundenbetreuer": {
    "partnerId": "ABC12",
    "firmenname": "Beispiel AG",
    "vorname": "Beispiel Vorname",
    "nachname": "Beispiel Nachname",
    "anschrift": {
      "strasse": "Beispielstr.",
      "hausnummer": "42",
      "postleitzahl": "10179",
      "ort": "Berlin"
    },
    "telefon": "030 123456",
    "email": "beispiel@beispiel.de",
    "iban": "DE75201207003100124444",
    "anrede": "HERR"
  },
  "metadaten": {
    "traceId": "ks-abc01234",
    "vorgangsnummer": "AB01234"
  },
  "featureToggles": [
    {
      "id": "MOD_DARLEHEN",
      "aktiv": true
    }
  ],
  "handelsbeziehungen": [
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "kreditProvisionswunsch": 0.02,
      "vertriebsgruppe": "creditfair"
    }
  ]
}
```

</p>
</details>

<details><summary>Response</summary>
<p>

```json
{
  "supportMeldung": null,
  "angebote": [
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "referenznummerProduktanbieter": null,
      "referenznummerDienstleister": null,
      "produktbezeichnung": "Modernisierungsdarlehen",
      "produktart": "MODERNISIERUNGSKREDIT",
      "angebotsvariantentyp": "ZinsGarant15_Mod_Neo_16",
      "gesamtkonditionen": {
        "effektivzinssatz": 0.038,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32975.37,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 187,
        "rateProMonat": 177.83,
        "vertragsbeginn": "2019-10-01"
      },
      "kredit": {
        "effektivzinssatz": 0.038,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32975.37,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 94,
        "rateProMonat": 64.58,
        "letzteRate": 64.58,
        "provisionsbetrag": 375.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "vorlaufzinsenProTag": 0.0,
        "versicherung": null
      },
      "bausparvertrag": {
        "tarifname": "AL_Neo Klassik (1.6 %)",
        "bausparsumme": 25000.0,
        "gesamtlaufzeitInMonaten": 187,
        "zuteilungsZeitpunkt": "2027-07-31",
        "provision": 450.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "jahresentgelt": 15.0,
        "abschlussgebuehr": 400.0,
        "sparphase": {
          "sparbeitragMonatlich": 113.25,
          "dauerInMonaten": 94,
          "guthabenBeiZuteilung": 10088.01,
          "guthabenZinssatz": 0.002
        },
        "darlehensphase": {
          "darlehenssumme": 14911.99,
          "rateMonatlich": 177.83,
          "dauerInMonaten": 93,
          "sollzinsSatz": 0.0245,
          "effektivzinsSatz": 0.0292,
          "letzteRate": 12.24,
          "tilgungsende": "2035-04-30"
        }
      },
      "status": {
        "machbarkeitsstatus": "MACHBAR",
        "angepasst": true
      },
      "meldungen": [
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Vorname] Für den Antragsteller ohne Namen ist der Vorname zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Nachname] Für den Antragsteller ohne Namen ist der Nachname zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Anrede] Für den Antragsteller ohne Namen ist die Anrede zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Staatsangehörigkeit] Für den Antragsteller ohne Namen ist die Staatsangehörigkeit zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Familienstand] Für den Antragsteller ohne Namen ist der Familienstand zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Geburtsort] Für den Antragsteller ohne Namen ist der Geburtsort zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Geburtsdatum] Für den Antragsteller ohne Namen ist das Geburtsdatum zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Anschrift] Für den Antragsteller ohne Namen ist die komplette Anschrift (Strasse, PLZ, Ort) zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Branche] Für den Antragsteller ohne Namen ist die Branche vollständig zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Arbeitgeberland / Land Firmensitz] Für den Antragsteller ohne Namen ist das Arbeitgeberland, bei Selbständigen das Land des Firmensitzes zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Datum der Beschäftigung] Bitte erfassen Sie den Beginn der Beschäftigung, bei Rentnern das Renteneintrittstdatum und bei Selbständigen den Beginn der Selbstständigkeit.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Dauer des Vertragsverhältnisses] Für den Antragsteller ohne Namen ist die Dauer der Beschäftigungsstatus zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Anzahl Personen im Haushalt] Für jeden Haushalt ist die Anzahl der Personen zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Anzahl unterhaltsberechtigter Kinder] Für den Antragsteller ohne Namen ist die Anzahl unterhaltsberechtigter Kinder zu erfassen.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Der Provisionswunsch wurde angepasst.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Die Laufzeit wurde angepasst.",
          "code": null
        }
      ],
      "unterlagen": [
        {
          "code": null,
          "text": "Baufinanzierungsvertrag von allen unterzeichnet zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Unterzeichneter, vollständiger Darlehensantrag",
          "referenz": null
        },
        {
          "code": null,
          "text": "Auszahlungsanweisung inkl. ausgefülltes und vom Kontoinhaber unterschriebenes SEPA-Lastschriftmandat",
          "referenz": null
        },
        {
          "code": null,
          "text": "Abschluss des entsprechenden Bausparvertrages im Tarif AL_Neo Klassik in Höhe des Vorausdarlehens",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollwirksame Verpfändung für diesen Bausparvertrag, d.h. vom Sicherungsgeber unterzeichnetes Formular zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollmacht zur Einholung eines Grundbuchauszuges durch die ALTE LEIPZIGER Bauspar AG",
          "referenz": null
        },
        {
          "code": null,
          "text": "Kopien der Personalausweise oder Reisepässe aller Darlehensnehmer (Vorder- und Rückseite)",
          "referenz": null
        },
        {
          "code": null,
          "text": "Letzte Gehaltsabrechnung sowie Dezember Gehaltsabrechnung des Vorjahres mit kumulierten Jahreswerten bzw. Nachweise über Renteneinkünfte aller Darlehensnehmer",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollständige Legitimationsprüfung aller Darlehensnehmer auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Bestätigung der wohnwirtschaftlichen Verwendung des Darlehens auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vorlage der Darlehensverträge für Ratenkredite und für Immobiliardarlehen, soweit vorhanden",
          "referenz": null
        }
      ],
      "bonitaetscheck": {
        "name": "Haushaltsrechnung",
        "ueberschrift": "Alte Leipziger Bauspar AG",
        "ueberschuss": 1622.17,
        "bloecke": [
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Unselbständiges Nettoeinkommen",
                "wert": 3000.0
              }
            ],
            "titel": "Einnahmen",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Einnahmen",
                  "wert": 3000.0
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Lebenshaltungskosten",
                "wert": 1200.0
              },
              {
                "hervorgehoben": false,
                "label": "Rate der Finanzierung",
                "wert": 177.83
              }
            ],
            "titel": "Ausgaben",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Ausgaben",
                  "wert": 1377.83
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": null,
            "titel": "Überschuss / Fehlbetrag",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Überschuss",
                  "wert": 1622.17
                }
              ],
              "hervorgehoben": true
            }
          }
        ]
      },
      "tilgungsplanBausparvertragMitVorausdarlehen": {
        "sparphase": {
          "eintraege": [
            {
              "jahr": 2019,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": -400.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -286.75
            },
            {
              "jahr": 2019,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -173.5
            },
            {
              "jahr": 2019,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -60.25
            },
            {
              "jahr": 2020,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 1.14,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 1284.89
            },
            {
              "jahr": 2021,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 3.79,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 2632.68
            },
            {
              "jahr": 2022,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 6.48,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 3983.16
            },
            {
              "jahr": 2023,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 9.18,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 5336.34
            },
            {
              "jahr": 2024,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 11.89,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 6692.23
            },
            {
              "jahr": 2025,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 14.6,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 8050.83
            },
            {
              "jahr": 2026,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 17.32,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 9412.15
            },
            {
              "jahr": 2027,
              "monat": null,
              "gesamtrate": 1131.56,
              "vorausdarlehenSollzinsen": -452.06,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": 679.5,
              "bausparvertragGuthabenzinsen": 11.36,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16602.77,
            "vorausdarlehenSollzinsen": -6070.52,
            "vorausdarlehenSaldo": -25000.0,
            "bausparvertragEinzahlungen": 10532.25,
            "bausparvertragGuthabenzinsen": 75.76,
            "bausparvertragGebuehren": -520.0,
            "bausparvertragTilgung": null,
            "bausparvertragSollzinsen": null,
            "bausparvertragSaldo": 10088.01
          }
        },
        "darlehensphase": {
          "eintraege": [
            {
              "jahr": 2027,
              "monat": 7,
              "gesamtrate": 0.0,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 0.0,
              "bausparvertragSollzinsen": 0.0,
              "bausparvertragSaldo": -14911.99
            },
            {
              "jahr": 2027,
              "monat": 8,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.38,
              "bausparvertragSollzinsen": -30.45,
              "bausparvertragSaldo": -14764.61
            },
            {
              "jahr": 2027,
              "monat": 9,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.69,
              "bausparvertragSollzinsen": -30.14,
              "bausparvertragSaldo": -14616.92
            },
            {
              "jahr": 2027,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.99,
              "bausparvertragSollzinsen": -29.84,
              "bausparvertragSaldo": -14468.93
            },
            {
              "jahr": 2027,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.29,
              "bausparvertragSollzinsen": -29.54,
              "bausparvertragSaldo": -14320.64
            },
            {
              "jahr": 2027,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.59,
              "bausparvertragSollzinsen": -29.24,
              "bausparvertragSaldo": -14172.05
            },
            {
              "jahr": 2028,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1806.94,
              "bausparvertragSollzinsen": -327.02,
              "bausparvertragSaldo": -12365.11
            },
            {
              "jahr": 2029,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1851.71,
              "bausparvertragSollzinsen": -282.25,
              "bausparvertragSaldo": -10513.4
            },
            {
              "jahr": 2030,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1897.59,
              "bausparvertragSollzinsen": -236.37,
              "bausparvertragSaldo": -8615.81
            },
            {
              "jahr": 2031,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1944.61,
              "bausparvertragSollzinsen": -189.35,
              "bausparvertragSaldo": -6671.2
            },
            {
              "jahr": 2032,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1992.78,
              "bausparvertragSollzinsen": -141.18,
              "bausparvertragSaldo": -4678.42
            },
            {
              "jahr": 2033,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2042.19,
              "bausparvertragSollzinsen": -91.77,
              "bausparvertragSaldo": -2636.23
            },
            {
              "jahr": 2034,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2092.77,
              "bausparvertragSollzinsen": -41.19,
              "bausparvertragSaldo": -543.46
            },
            {
              "jahr": 2035,
              "monat": null,
              "gesamtrate": 545.73,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 543.46,
              "bausparvertragSollzinsen": -2.27,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16372.6,
            "vorausdarlehenSollzinsen": null,
            "vorausdarlehenSaldo": null,
            "bausparvertragEinzahlungen": null,
            "bausparvertragGuthabenzinsen": null,
            "bausparvertragGebuehren": null,
            "bausparvertragTilgung": 14911.99,
            "bausparvertragSollzinsen": -1460.61,
            "bausparvertragSaldo": 0.0
          }
        }
      },
      "maximalerAuszahlungsbetrag": null
    },
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "referenznummerProduktanbieter": null,
      "referenznummerDienstleister": null,
      "produktbezeichnung": "Modernisierungsdarlehen",
      "produktart": "MODERNISIERUNGSKREDIT",
      "angebotsvariantentyp": "ZinsGarant15_Mod_Neo",
      "gesamtkonditionen": {
        "effektivzinssatz": 0.0372,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32713.55,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 185,
        "rateProMonat": 177.83,
        "vertragsbeginn": "2019-10-01"
      },
      "kredit": {
        "effektivzinssatz": 0.0372,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32713.55,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 92,
        "rateProMonat": 64.58,
        "letzteRate": 64.58,
        "provisionsbetrag": 375.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "vorlaufzinsenProTag": 0.0,
        "versicherung": null
      },
      "bausparvertrag": {
        "tarifname": "AL_Neo Klassik (1.0 %)",
        "bausparsumme": 25000.0,
        "gesamtlaufzeitInMonaten": 185,
        "zuteilungsZeitpunkt": "2027-05-31",
        "provision": 300.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "jahresentgelt": 15.0,
        "abschlussgebuehr": 250.0,
        "sparphase": {
          "sparbeitragMonatlich": 113.25,
          "dauerInMonaten": 92,
          "guthabenBeiZuteilung": 10010.37,
          "guthabenZinssatz": 0.002
        },
        "darlehensphase": {
          "darlehenssumme": 14989.63,
          "rateMonatlich": 177.83,
          "dauerInMonaten": 93,
          "sollzinsSatz": 0.0245,
          "effektivzinsSatz": 0.0275,
          "letzteRate": 106.08,
          "tilgungsende": "2035-02-28"
        }
      },
      "status": {
        "machbarkeitsstatus": "MACHBAR",
        "angepasst": true
      },
      "meldungen": [
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Vorname] Für den Antragsteller ohne Namen ist der Vorname zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Nachname] Für den Antragsteller ohne Namen ist der Nachname zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Anrede] Für den Antragsteller ohne Namen ist die Anrede zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Staatsangehörigkeit] Für den Antragsteller ohne Namen ist die Staatsangehörigkeit zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Familienstand] Für den Antragsteller ohne Namen ist der Familienstand zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Geburtsort] Für den Antragsteller ohne Namen ist der Geburtsort zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Geburtsdatum] Für den Antragsteller ohne Namen ist das Geburtsdatum zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Anschrift] Für den Antragsteller ohne Namen ist die komplette Anschrift (Strasse, PLZ, Ort) zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Branche] Für den Antragsteller ohne Namen ist die Branche vollständig zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Arbeitgeberland / Land Firmensitz] Für den Antragsteller ohne Namen ist das Arbeitgeberland, bei Selbständigen das Land des Firmensitzes zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Datum der Beschäftigung] Bitte erfassen Sie den Beginn der Beschäftigung, bei Rentnern das Renteneintrittstdatum und bei Selbständigen den Beginn der Selbstständigkeit.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Dauer des Vertragsverhältnisses] Für den Antragsteller ohne Namen ist die Dauer der Beschäftigungsstatus zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Anzahl Personen im Haushalt] Für jeden Haushalt ist die Anzahl der Personen zu erfassen.",
          "code": null
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Anzahl unterhaltsberechtigter Kinder] Für den Antragsteller ohne Namen ist die Anzahl unterhaltsberechtigter Kinder zu erfassen.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Der Provisionswunsch wurde angepasst.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Die Laufzeit wurde angepasst.",
          "code": null
        }
      ],
      "unterlagen": [
        {
          "code": null,
          "text": "Baufinanzierungsvertrag von allen unterzeichnet zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Unterzeichneter, vollständiger Darlehensantrag",
          "referenz": null
        },
        {
          "code": null,
          "text": "Auszahlungsanweisung inkl. ausgefülltes und vom Kontoinhaber unterschriebenes SEPA-Lastschriftmandat",
          "referenz": null
        },
        {
          "code": null,
          "text": "Abschluss des entsprechenden Bausparvertrages im Tarif AL_Neo Klassik in Höhe des Vorausdarlehens",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollwirksame Verpfändung für diesen Bausparvertrag, d.h. vom Sicherungsgeber unterzeichnetes Formular zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollmacht zur Einholung eines Grundbuchauszuges durch die ALTE LEIPZIGER Bauspar AG",
          "referenz": null
        },
        {
          "code": null,
          "text": "Kopien der Personalausweise oder Reisepässe aller Darlehensnehmer (Vorder- und Rückseite)",
          "referenz": null
        },
        {
          "code": null,
          "text": "Letzte Gehaltsabrechnung sowie Dezember Gehaltsabrechnung des Vorjahres mit kumulierten Jahreswerten bzw. Nachweise über Renteneinkünfte aller Darlehensnehmer",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollständige Legitimationsprüfung aller Darlehensnehmer auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Bestätigung der wohnwirtschaftlichen Verwendung des Darlehens auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vorlage der Darlehensverträge für Ratenkredite und für Immobiliardarlehen, soweit vorhanden",
          "referenz": null
        }
      ],
      "bonitaetscheck": {
        "name": "Haushaltsrechnung",
        "ueberschrift": "Alte Leipziger Bauspar AG",
        "ueberschuss": 1622.17,
        "bloecke": [
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Unselbständiges Nettoeinkommen",
                "wert": 3000.0
              }
            ],
            "titel": "Einnahmen",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Einnahmen",
                  "wert": 3000.0
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Lebenshaltungskosten",
                "wert": 1200.0
              },
              {
                "hervorgehoben": false,
                "label": "Rate der Finanzierung",
                "wert": 177.83
              }
            ],
            "titel": "Ausgaben",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Ausgaben",
                  "wert": 1377.83
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": null,
            "titel": "Überschuss / Fehlbetrag",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Überschuss",
                  "wert": 1622.17
                }
              ],
              "hervorgehoben": true
            }
          }
        ]
      },
      "tilgungsplanBausparvertragMitVorausdarlehen": {
        "sparphase": {
          "eintraege": [
            {
              "jahr": 2019,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": -250.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -136.75
            },
            {
              "jahr": 2019,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -23.5
            },
            {
              "jahr": 2019,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 89.75
            },
            {
              "jahr": 2020,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 1.4,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 1435.15
            },
            {
              "jahr": 2021,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 4.09,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 2783.24
            },
            {
              "jahr": 2022,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 6.78,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 4134.02
            },
            {
              "jahr": 2023,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 9.49,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 5487.51
            },
            {
              "jahr": 2024,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 12.19,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 6843.7
            },
            {
              "jahr": 2025,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 14.9,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 8202.6
            },
            {
              "jahr": 2026,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 17.62,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 9564.22
            },
            {
              "jahr": 2027,
              "monat": null,
              "gesamtrate": 775.9,
              "vorausdarlehenSollzinsen": -322.9,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": 453.0,
              "bausparvertragGuthabenzinsen": 8.15,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16247.11,
            "vorausdarlehenSollzinsen": -5941.36,
            "vorausdarlehenSaldo": -25000.0,
            "bausparvertragEinzahlungen": 10305.75,
            "bausparvertragGuthabenzinsen": 74.62,
            "bausparvertragGebuehren": -370.0,
            "bausparvertragTilgung": null,
            "bausparvertragSollzinsen": null,
            "bausparvertragSaldo": 10010.37
          }
        },
        "darlehensphase": {
          "eintraege": [
            {
              "jahr": 2027,
              "monat": 5,
              "gesamtrate": 0.0,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 0.0,
              "bausparvertragSollzinsen": 0.0,
              "bausparvertragSaldo": -14989.63
            },
            {
              "jahr": 2027,
              "monat": 6,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.23,
              "bausparvertragSollzinsen": -30.6,
              "bausparvertragSaldo": -14842.4
            },
            {
              "jahr": 2027,
              "monat": 7,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.53,
              "bausparvertragSollzinsen": -30.3,
              "bausparvertragSaldo": -14694.87
            },
            {
              "jahr": 2027,
              "monat": 8,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.83,
              "bausparvertragSollzinsen": -30.0,
              "bausparvertragSaldo": -14547.04
            },
            {
              "jahr": 2027,
              "monat": 9,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.13,
              "bausparvertragSollzinsen": -29.7,
              "bausparvertragSaldo": -14398.91
            },
            {
              "jahr": 2027,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.43,
              "bausparvertragSollzinsen": -29.4,
              "bausparvertragSaldo": -14250.48
            },
            {
              "jahr": 2027,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.74,
              "bausparvertragSollzinsen": -29.09,
              "bausparvertragSaldo": -14101.74
            },
            {
              "jahr": 2027,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 149.04,
              "bausparvertragSollzinsen": -28.79,
              "bausparvertragSaldo": -13952.7
            },
            {
              "jahr": 2028,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1812.37,
              "bausparvertragSollzinsen": -321.59,
              "bausparvertragSaldo": -12140.33
            },
            {
              "jahr": 2029,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1857.29,
              "bausparvertragSollzinsen": -276.67,
              "bausparvertragSaldo": -10283.04
            },
            {
              "jahr": 2030,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1903.32,
              "bausparvertragSollzinsen": -230.64,
              "bausparvertragSaldo": -8379.72
            },
            {
              "jahr": 2031,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1950.47,
              "bausparvertragSollzinsen": -183.49,
              "bausparvertragSaldo": -6429.25
            },
            {
              "jahr": 2032,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1998.77,
              "bausparvertragSollzinsen": -135.19,
              "bausparvertragSaldo": -4430.48
            },
            {
              "jahr": 2033,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2048.29,
              "bausparvertragSollzinsen": -85.67,
              "bausparvertragSaldo": -2382.19
            },
            {
              "jahr": 2034,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2099.06,
              "bausparvertragSollzinsen": -34.9,
              "bausparvertragSaldo": -283.13
            },
            {
              "jahr": 2035,
              "monat": null,
              "gesamtrate": 283.91,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 283.13,
              "bausparvertragSollzinsen": -0.78,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16466.44,
            "vorausdarlehenSollzinsen": null,
            "vorausdarlehenSaldo": null,
            "bausparvertragEinzahlungen": null,
            "bausparvertragGuthabenzinsen": null,
            "bausparvertragGebuehren": null,
            "bausparvertragTilgung": 14989.63,
            "bausparvertragSollzinsen": -1476.81,
            "bausparvertragSaldo": 0.0
          }
        }
      },
      "maximalerAuszahlungsbetrag": null
    }
  ]
}
```

</p>
</details>

### Vollständiges Angebot (ein Antragsteller)

<details><summary>Request</summary>
<p>

```json
{
  "antragsteller": [
    {
      "id": "552a2e18-b407-44ce-8af5-f6334cc64f80",
      "persoenlicheAngaben": {
        "anrede": "HERR",
        "vorname": "Beispiel Vorname",
        "nachname": "Beispiel Nachname",
        "geburtsdatum": "1970-01-01",
        "geburtsort": "Berlin",
        "staatsangehoerigkeit": "DE",
        "familienstand": "LEDIG",
        "anzahlPersonenImHaushalt": 1
      },
      "derzeitigeBeschaeftigung": {
        "beschaeftigungsverhaeltnis": "ANGESTELLT",
        "befristet": "UNBEFRISTET",
        "beschaeftigtSeit": "2010-01-01",
        "beruf": "Angestellter",
        "branche": "HANDEL",
        "anschrift": {
          "strasse": "Beispielstr.",
          "hausnummer": "43",
          "postleitzahl": "10179",
          "ort": "Berlin",
          "land": "DE"
        },
        "arbeitgebername": "Beispiel AG"
      },
      "vorherigeBeschaeftigung": {
        "anschrift": {}
      },
      "derzeitigeWohnsituation": {
        "wohnart": "IM_EIGENEN_HAUS",
        "wohnhaftSeit": "2000-01-01",
        "anschrift": {
          "strasse": "Beispielstr.",
          "hausnummer": "42",
          "postleitzahl": "10179",
          "ort": "Berlin",
          "land": "DE"
        }
      },
      "kontakt": {
        "telefonPrivat": "030 123456",
        "telefonGeschaeftlich": "030 123456",
        "email": "beispiel@beispiel.de"
      },
      "herkunft": {
        "aufenthaltstitel": {}
      },
      "kinder": [],
      "rentenversicherung": {
        "anschrift": {}
      },
      "bonitaetsangaben": {
        "ausgaben": {},
        "einnahmen": {
          "monatlicheEinnahmen": {
            "regelmaessigesUnselbstaendigesEinkommen": 3000,
            "mietUndPachteinnahmen": {}
          },
          "jaehrlicheEinnahmen": {
            "einkommenAusSelbstaendigkeit": {
              "zuVersteuerndesEinkommen": {},
              "einkommenssteuer": {},
              "abschreibungen": {}
            }
          }
        },
        "vermoegen": {
          "immobilien": []
        },
        "verbindlichkeiten": {
          "ratenkredite": [],
          "sonstigeVerbindlichkeiten": [],
          "leasings": [],
          "kreditkarten": [],
          "dispositionskredite": [],
          "immobiliendarlehen": [],
          "geschaeftskredite": [],
          "kontokorrentkredite": []
        }
      }
    }
  ],
  "gemeinsameAntragstellerangaben": {
    "bonitaetsangaben": {}
  },
  "finanzierungswunsch": {
    "kreditwunsch": {
      "finanzierungszweck": "MODERNISIERUNG_UND_WOHNEN",
      "auszahlungsbetrag": 25000,
      "ratenzahlungstermin": "ULTIMO",
      "laufzeitInMonaten": 60
    },
    "versicherungsWunsch": [],
    "konto": {
      "kontoinhaberIds": []
    },
    "abzuloesendeVerbindlichkeiten": {
      "ratenkredite": [],
      "sonstigeVerbindlichkeiten": [],
      "kreditkarten": [],
      "dispositionskredite": [],
      "geschaeftskredite": []
    },
    "fahrzeug": {}
  },
  "kundenbetreuer": {
    "partnerId": "ABC12",
    "firmenname": "Beispiel AG",
    "vorname": "Beispiel Vorname",
    "nachname": "Beispiel Nachname",
    "anschrift": {
      "strasse": "Beispielstr.",
      "hausnummer": "42",
      "postleitzahl": "10179",
      "ort": "Berlin"
    },
    "telefon": "030 123456",
    "email": "beispiel@beispiel.de",
    "iban": "DE75201207003100124444",
    "anrede": "HERR"
  },
  "metadaten": {
    "traceId": "ks-55f5f45b",
    "vorgangsnummer": "Q32CU4"
  },
  "featureToggles": [
    {
      "id": "MOD_DARLEHEN",
      "aktiv": true
    }
  ],
  "handelsbeziehungen": [
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "kreditProvisionswunsch": 0.02,
      "vertriebsgruppe": "creditfair"
    }
  ]
}
```

</p>
</details>


<details><summary>Response</summary>
<p>

```json
{
  "supportMeldung": null,
  "angebote": [
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "referenznummerProduktanbieter": null,
      "referenznummerDienstleister": null,
      "produktbezeichnung": "Modernisierungsdarlehen",
      "produktart": "MODERNISIERUNGSKREDIT",
      "angebotsvariantentyp": "ZinsGarant15_Mod_Neo_16",
      "gesamtkonditionen": {
        "effektivzinssatz": 0.038,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32975.37,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 187,
        "rateProMonat": 177.83,
        "vertragsbeginn": "2019-10-01"
      },
      "kredit": {
        "effektivzinssatz": 0.038,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32975.37,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 94,
        "rateProMonat": 64.58,
        "letzteRate": 64.58,
        "provisionsbetrag": 375.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "vorlaufzinsenProTag": 0.0,
        "versicherung": null
      },
      "bausparvertrag": {
        "tarifname": "AL_Neo Klassik (1.6 %)",
        "bausparsumme": 25000.0,
        "gesamtlaufzeitInMonaten": 187,
        "zuteilungsZeitpunkt": "2027-07-31",
        "provision": 450.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "jahresentgelt": 15.0,
        "abschlussgebuehr": 400.0,
        "sparphase": {
          "sparbeitragMonatlich": 113.25,
          "dauerInMonaten": 94,
          "guthabenBeiZuteilung": 10088.01,
          "guthabenZinssatz": 0.002
        },
        "darlehensphase": {
          "darlehenssumme": 14911.99,
          "rateMonatlich": 177.83,
          "dauerInMonaten": 93,
          "sollzinsSatz": 0.0245,
          "effektivzinsSatz": 0.0292,
          "letzteRate": 12.24,
          "tilgungsende": "2035-04-30"
        }
      },
      "status": {
        "machbarkeitsstatus": "MACHBAR",
        "angepasst": true
      },
      "meldungen": [
        {
          "kategorie": "ANPASSUNG",
          "text": "Der Provisionswunsch wurde angepasst.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Die Laufzeit wurde angepasst.",
          "code": null
        }
      ],
      "unterlagen": [
        {
          "code": null,
          "text": "Baufinanzierungsvertrag von allen unterzeichnet zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Unterzeichneter, vollständiger Darlehensantrag",
          "referenz": null
        },
        {
          "code": null,
          "text": "Auszahlungsanweisung inkl. ausgefülltes und vom Kontoinhaber unterschriebenes SEPA-Lastschriftmandat",
          "referenz": null
        },
        {
          "code": null,
          "text": "Abschluss des entsprechenden Bausparvertrages im Tarif AL_Neo Klassik in Höhe des Vorausdarlehens",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollwirksame Verpfändung für diesen Bausparvertrag, d.h. vom Sicherungsgeber unterzeichnetes Formular zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollmacht zur Einholung eines Grundbuchauszuges durch die ALTE LEIPZIGER Bauspar AG",
          "referenz": null
        },
        {
          "code": null,
          "text": "Kopien der Personalausweise oder Reisepässe aller Darlehensnehmer (Vorder- und Rückseite)",
          "referenz": null
        },
        {
          "code": null,
          "text": "Letzte Gehaltsabrechnung sowie Dezember Gehaltsabrechnung des Vorjahres mit kumulierten Jahreswerten bzw. Nachweise über Renteneinkünfte aller Darlehensnehmer",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollständige Legitimationsprüfung aller Darlehensnehmer auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Bestätigung der wohnwirtschaftlichen Verwendung des Darlehens auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vorlage der Darlehensverträge für Ratenkredite und für Immobiliardarlehen, soweit vorhanden",
          "referenz": null
        }
      ],
      "bonitaetscheck": {
        "name": "Haushaltsrechnung",
        "ueberschrift": "Alte Leipziger Bauspar AG",
        "ueberschuss": 1622.17,
        "bloecke": [
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Unselbständiges Nettoeinkommen",
                "wert": 3000.0
              }
            ],
            "titel": "Einnahmen",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Einnahmen",
                  "wert": 3000.0
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Lebenshaltungskosten",
                "wert": 1200.0
              },
              {
                "hervorgehoben": false,
                "label": "Rate der Finanzierung",
                "wert": 177.83
              }
            ],
            "titel": "Ausgaben",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Ausgaben",
                  "wert": 1377.83
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": null,
            "titel": "Überschuss / Fehlbetrag",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Überschuss",
                  "wert": 1622.17
                }
              ],
              "hervorgehoben": true
            }
          }
        ]
      },
      "tilgungsplanBausparvertragMitVorausdarlehen": {
        "sparphase": {
          "eintraege": [
            {
              "jahr": 2019,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": -400.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -286.75
            },
            {
              "jahr": 2019,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -173.5
            },
            {
              "jahr": 2019,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -60.25
            },
            {
              "jahr": 2020,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 1.14,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 1284.89
            },
            {
              "jahr": 2021,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 3.79,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 2632.68
            },
            {
              "jahr": 2022,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 6.48,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 3983.16
            },
            {
              "jahr": 2023,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 9.18,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 5336.34
            },
            {
              "jahr": 2024,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 11.89,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 6692.23
            },
            {
              "jahr": 2025,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 14.6,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 8050.83
            },
            {
              "jahr": 2026,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 17.32,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 9412.15
            },
            {
              "jahr": 2027,
              "monat": null,
              "gesamtrate": 1131.56,
              "vorausdarlehenSollzinsen": -452.06,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": 679.5,
              "bausparvertragGuthabenzinsen": 11.36,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16602.77,
            "vorausdarlehenSollzinsen": -6070.52,
            "vorausdarlehenSaldo": -25000.0,
            "bausparvertragEinzahlungen": 10532.25,
            "bausparvertragGuthabenzinsen": 75.76,
            "bausparvertragGebuehren": -520.0,
            "bausparvertragTilgung": null,
            "bausparvertragSollzinsen": null,
            "bausparvertragSaldo": 10088.01
          }
        },
        "darlehensphase": {
          "eintraege": [
            {
              "jahr": 2027,
              "monat": 7,
              "gesamtrate": 0.0,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 0.0,
              "bausparvertragSollzinsen": 0.0,
              "bausparvertragSaldo": -14911.99
            },
            {
              "jahr": 2027,
              "monat": 8,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.38,
              "bausparvertragSollzinsen": -30.45,
              "bausparvertragSaldo": -14764.61
            },
            {
              "jahr": 2027,
              "monat": 9,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.69,
              "bausparvertragSollzinsen": -30.14,
              "bausparvertragSaldo": -14616.92
            },
            {
              "jahr": 2027,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.99,
              "bausparvertragSollzinsen": -29.84,
              "bausparvertragSaldo": -14468.93
            },
            {
              "jahr": 2027,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.29,
              "bausparvertragSollzinsen": -29.54,
              "bausparvertragSaldo": -14320.64
            },
            {
              "jahr": 2027,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.59,
              "bausparvertragSollzinsen": -29.24,
              "bausparvertragSaldo": -14172.05
            },
            {
              "jahr": 2028,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1806.94,
              "bausparvertragSollzinsen": -327.02,
              "bausparvertragSaldo": -12365.11
            },
            {
              "jahr": 2029,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1851.71,
              "bausparvertragSollzinsen": -282.25,
              "bausparvertragSaldo": -10513.4
            },
            {
              "jahr": 2030,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1897.59,
              "bausparvertragSollzinsen": -236.37,
              "bausparvertragSaldo": -8615.81
            },
            {
              "jahr": 2031,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1944.61,
              "bausparvertragSollzinsen": -189.35,
              "bausparvertragSaldo": -6671.2
            },
            {
              "jahr": 2032,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1992.78,
              "bausparvertragSollzinsen": -141.18,
              "bausparvertragSaldo": -4678.42
            },
            {
              "jahr": 2033,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2042.19,
              "bausparvertragSollzinsen": -91.77,
              "bausparvertragSaldo": -2636.23
            },
            {
              "jahr": 2034,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2092.77,
              "bausparvertragSollzinsen": -41.19,
              "bausparvertragSaldo": -543.46
            },
            {
              "jahr": 2035,
              "monat": null,
              "gesamtrate": 545.73,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 543.46,
              "bausparvertragSollzinsen": -2.27,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16372.6,
            "vorausdarlehenSollzinsen": null,
            "vorausdarlehenSaldo": null,
            "bausparvertragEinzahlungen": null,
            "bausparvertragGuthabenzinsen": null,
            "bausparvertragGebuehren": null,
            "bausparvertragTilgung": 14911.99,
            "bausparvertragSollzinsen": -1460.61,
            "bausparvertragSaldo": 0.0
          }
        }
      },
      "maximalerAuszahlungsbetrag": null
    },
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "referenznummerProduktanbieter": null,
      "referenznummerDienstleister": null,
      "produktbezeichnung": "Modernisierungsdarlehen",
      "produktart": "MODERNISIERUNGSKREDIT",
      "angebotsvariantentyp": "ZinsGarant15_Mod_Neo",
      "gesamtkonditionen": {
        "effektivzinssatz": 0.0372,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32713.55,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 185,
        "rateProMonat": 177.83,
        "vertragsbeginn": "2019-10-01"
      },
      "kredit": {
        "effektivzinssatz": 0.0372,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32713.55,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 92,
        "rateProMonat": 64.58,
        "letzteRate": 64.58,
        "provisionsbetrag": 375.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "vorlaufzinsenProTag": 0.0,
        "versicherung": null
      },
      "bausparvertrag": {
        "tarifname": "AL_Neo Klassik (1.0 %)",
        "bausparsumme": 25000.0,
        "gesamtlaufzeitInMonaten": 185,
        "zuteilungsZeitpunkt": "2027-05-31",
        "provision": 300.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "jahresentgelt": 15.0,
        "abschlussgebuehr": 250.0,
        "sparphase": {
          "sparbeitragMonatlich": 113.25,
          "dauerInMonaten": 92,
          "guthabenBeiZuteilung": 10010.37,
          "guthabenZinssatz": 0.002
        },
        "darlehensphase": {
          "darlehenssumme": 14989.63,
          "rateMonatlich": 177.83,
          "dauerInMonaten": 93,
          "sollzinsSatz": 0.0245,
          "effektivzinsSatz": 0.0275,
          "letzteRate": 106.08,
          "tilgungsende": "2035-02-28"
        }
      },
      "status": {
        "machbarkeitsstatus": "MACHBAR",
        "angepasst": true
      },
      "meldungen": [
        {
          "kategorie": "ANPASSUNG",
          "text": "Der Provisionswunsch wurde angepasst.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Die Laufzeit wurde angepasst.",
          "code": null
        }
      ],
      "unterlagen": [
        {
          "code": null,
          "text": "Baufinanzierungsvertrag von allen unterzeichnet zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Unterzeichneter, vollständiger Darlehensantrag",
          "referenz": null
        },
        {
          "code": null,
          "text": "Auszahlungsanweisung inkl. ausgefülltes und vom Kontoinhaber unterschriebenes SEPA-Lastschriftmandat",
          "referenz": null
        },
        {
          "code": null,
          "text": "Abschluss des entsprechenden Bausparvertrages im Tarif AL_Neo Klassik in Höhe des Vorausdarlehens",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollwirksame Verpfändung für diesen Bausparvertrag, d.h. vom Sicherungsgeber unterzeichnetes Formular zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollmacht zur Einholung eines Grundbuchauszuges durch die ALTE LEIPZIGER Bauspar AG",
          "referenz": null
        },
        {
          "code": null,
          "text": "Kopien der Personalausweise oder Reisepässe aller Darlehensnehmer (Vorder- und Rückseite)",
          "referenz": null
        },
        {
          "code": null,
          "text": "Letzte Gehaltsabrechnung sowie Dezember Gehaltsabrechnung des Vorjahres mit kumulierten Jahreswerten bzw. Nachweise über Renteneinkünfte aller Darlehensnehmer",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollständige Legitimationsprüfung aller Darlehensnehmer auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Bestätigung der wohnwirtschaftlichen Verwendung des Darlehens auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vorlage der Darlehensverträge für Ratenkredite und für Immobiliardarlehen, soweit vorhanden",
          "referenz": null
        }
      ],
      "bonitaetscheck": {
        "name": "Haushaltsrechnung",
        "ueberschrift": "Alte Leipziger Bauspar AG",
        "ueberschuss": 1622.17,
        "bloecke": [
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Unselbständiges Nettoeinkommen",
                "wert": 3000.0
              }
            ],
            "titel": "Einnahmen",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Einnahmen",
                  "wert": 3000.0
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Lebenshaltungskosten",
                "wert": 1200.0
              },
              {
                "hervorgehoben": false,
                "label": "Rate der Finanzierung",
                "wert": 177.83
              }
            ],
            "titel": "Ausgaben",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Ausgaben",
                  "wert": 1377.83
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": null,
            "titel": "Überschuss / Fehlbetrag",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Überschuss",
                  "wert": 1622.17
                }
              ],
              "hervorgehoben": true
            }
          }
        ]
      },
      "tilgungsplanBausparvertragMitVorausdarlehen": {
        "sparphase": {
          "eintraege": [
            {
              "jahr": 2019,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": -250.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -136.75
            },
            {
              "jahr": 2019,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -23.5
            },
            {
              "jahr": 2019,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 89.75
            },
            {
              "jahr": 2020,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 1.4,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 1435.15
            },
            {
              "jahr": 2021,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 4.09,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 2783.24
            },
            {
              "jahr": 2022,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 6.78,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 4134.02
            },
            {
              "jahr": 2023,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 9.49,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 5487.51
            },
            {
              "jahr": 2024,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 12.19,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 6843.7
            },
            {
              "jahr": 2025,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 14.9,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 8202.6
            },
            {
              "jahr": 2026,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 17.62,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 9564.22
            },
            {
              "jahr": 2027,
              "monat": null,
              "gesamtrate": 775.9,
              "vorausdarlehenSollzinsen": -322.9,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": 453.0,
              "bausparvertragGuthabenzinsen": 8.15,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16247.11,
            "vorausdarlehenSollzinsen": -5941.36,
            "vorausdarlehenSaldo": -25000.0,
            "bausparvertragEinzahlungen": 10305.75,
            "bausparvertragGuthabenzinsen": 74.62,
            "bausparvertragGebuehren": -370.0,
            "bausparvertragTilgung": null,
            "bausparvertragSollzinsen": null,
            "bausparvertragSaldo": 10010.37
          }
        },
        "darlehensphase": {
          "eintraege": [
            {
              "jahr": 2027,
              "monat": 5,
              "gesamtrate": 0.0,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 0.0,
              "bausparvertragSollzinsen": 0.0,
              "bausparvertragSaldo": -14989.63
            },
            {
              "jahr": 2027,
              "monat": 6,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.23,
              "bausparvertragSollzinsen": -30.6,
              "bausparvertragSaldo": -14842.4
            },
            {
              "jahr": 2027,
              "monat": 7,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.53,
              "bausparvertragSollzinsen": -30.3,
              "bausparvertragSaldo": -14694.87
            },
            {
              "jahr": 2027,
              "monat": 8,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.83,
              "bausparvertragSollzinsen": -30.0,
              "bausparvertragSaldo": -14547.04
            },
            {
              "jahr": 2027,
              "monat": 9,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.13,
              "bausparvertragSollzinsen": -29.7,
              "bausparvertragSaldo": -14398.91
            },
            {
              "jahr": 2027,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.43,
              "bausparvertragSollzinsen": -29.4,
              "bausparvertragSaldo": -14250.48
            },
            {
              "jahr": 2027,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.74,
              "bausparvertragSollzinsen": -29.09,
              "bausparvertragSaldo": -14101.74
            },
            {
              "jahr": 2027,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 149.04,
              "bausparvertragSollzinsen": -28.79,
              "bausparvertragSaldo": -13952.7
            },
            {
              "jahr": 2028,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1812.37,
              "bausparvertragSollzinsen": -321.59,
              "bausparvertragSaldo": -12140.33
            },
            {
              "jahr": 2029,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1857.29,
              "bausparvertragSollzinsen": -276.67,
              "bausparvertragSaldo": -10283.04
            },
            {
              "jahr": 2030,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1903.32,
              "bausparvertragSollzinsen": -230.64,
              "bausparvertragSaldo": -8379.72
            },
            {
              "jahr": 2031,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1950.47,
              "bausparvertragSollzinsen": -183.49,
              "bausparvertragSaldo": -6429.25
            },
            {
              "jahr": 2032,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1998.77,
              "bausparvertragSollzinsen": -135.19,
              "bausparvertragSaldo": -4430.48
            },
            {
              "jahr": 2033,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2048.29,
              "bausparvertragSollzinsen": -85.67,
              "bausparvertragSaldo": -2382.19
            },
            {
              "jahr": 2034,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2099.06,
              "bausparvertragSollzinsen": -34.9,
              "bausparvertragSaldo": -283.13
            },
            {
              "jahr": 2035,
              "monat": null,
              "gesamtrate": 283.91,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 283.13,
              "bausparvertragSollzinsen": -0.78,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16466.44,
            "vorausdarlehenSollzinsen": null,
            "vorausdarlehenSaldo": null,
            "bausparvertragEinzahlungen": null,
            "bausparvertragGuthabenzinsen": null,
            "bausparvertragGebuehren": null,
            "bausparvertragTilgung": 14989.63,
            "bausparvertragSollzinsen": -1476.81,
            "bausparvertragSaldo": 0.0
          }
        }
      },
      "maximalerAuszahlungsbetrag": null
    }
  ]
}
```

</p>
</details>

### Vollständiges Angebot (mehrere Antragsteller im gemeinsamen Haushalt)

<details><summary>Request</summary>
<p>

```json
{
  "antragsteller": [
    {
      "id": "552a2e18-b407-44ce-8af5-f6334cc64f80",
      "haushaltspartnerId": "21794c8f-ad7c-442f-9bd5-1449951acd82",
      "persoenlicheAngaben": {
        "anrede": "HERR",
        "vorname": "Beispiel Vorname",
        "nachname": "Beispiel Nachname",
        "geburtsdatum": "1970-01-01",
        "geburtsort": "Berlin",
        "staatsangehoerigkeit": "DE",
        "familienstand": "VERHEIRATET",
        "anzahlPersonenImHaushalt": 2
      },
      "derzeitigeBeschaeftigung": {
        "beschaeftigungsverhaeltnis": "ANGESTELLT",
        "befristet": "UNBEFRISTET",
        "beschaeftigtSeit": "2010-01-01",
        "beruf": "Angestellter",
        "branche": "HANDEL",
        "anschrift": {
          "strasse": "Beispielstr.",
          "hausnummer": "43",
          "postleitzahl": "10179",
          "ort": "Berlin",
          "land": "DE"
        },
        "arbeitgebername": "Beispiel AG"
      },
      "vorherigeBeschaeftigung": {
        "anschrift": {}
      },
      "derzeitigeWohnsituation": {
        "wohnart": "IM_EIGENEN_HAUS",
        "wohnhaftSeit": "2000-01-01",
        "anschrift": {
          "strasse": "Beispielstr.",
          "hausnummer": "42",
          "postleitzahl": "10179",
          "ort": "Berlin",
          "land": "DE"
        }
      },
      "kontakt": {
        "telefonPrivat": "030 123456",
        "telefonGeschaeftlich": "030 123456",
        "email": "beispiel@beispiel.de"
      },
      "herkunft": {
        "aufenthaltstitel": {}
      },
      "kinder": [],
      "rentenversicherung": {
        "anschrift": {}
      },
      "bonitaetsangaben": {
        "ausgaben": {},
        "einnahmen": {
          "monatlicheEinnahmen": {
            "regelmaessigesUnselbstaendigesEinkommen": 3000,
            "mietUndPachteinnahmen": {}
          },
          "jaehrlicheEinnahmen": {
            "einkommenAusSelbstaendigkeit": {
              "zuVersteuerndesEinkommen": {},
              "einkommenssteuer": {},
              "abschreibungen": {}
            }
          }
        },
        "vermoegen": {
          "immobilien": []
        },
        "verbindlichkeiten": {
          "ratenkredite": [],
          "sonstigeVerbindlichkeiten": [],
          "leasings": [],
          "kreditkarten": [],
          "dispositionskredite": [],
          "immobiliendarlehen": [],
          "geschaeftskredite": [],
          "kontokorrentkredite": []
        }
      }
    },
    {
      "id": "21794c8f-ad7c-442f-9bd5-1449951acd82",
      "haushaltspartnerId": "552a2e18-b407-44ce-8af5-f6334cc64f80",
      "persoenlicheAngaben": {
        "anrede": "FRAU",
        "vorname": "Beispiel Vorname 2",
        "nachname": "Beispiel Nachname",
        "geburtsdatum": "1970-07-01",
        "geburtsort": "Berlin",
        "staatsangehoerigkeit": "DE",
        "familienstand": "VERHEIRATET"
      },
      "derzeitigeBeschaeftigung": {
        "beschaeftigungsverhaeltnis": "ANGESTELLT",
        "befristet": "UNBEFRISTET",
        "beschaeftigtSeit": "2010-01-01",
        "beruf": "Angestellter",
        "branche": "HANDEL",
        "anschrift": {
          "strasse": "Beispielstr",
          "hausnummer": "43",
          "postleitzahl": "10179",
          "ort": "Berlin",
          "land": "DE"
        },
        "arbeitgebername": "Beispiel AG"
      },
      "vorherigeBeschaeftigung": {
        "anschrift": {}
      },
      "derzeitigeWohnsituation": {
        "wohnart": "IM_EIGENEN_HAUS",
        "wohnhaftSeit": "2000-01-01",
        "anschrift": {
          "strasse": "Beispielstr.",
          "hausnummer": "42",
          "postleitzahl": "10179",
          "ort": "Berlin",
          "land": "DE"
        }
      },
      "kontakt": {
        "telefonPrivat": "030 123456",
        "telefonGeschaeftlich": "030 123456",
        "email": "beispiel2@beispiel.de"
      },
      "herkunft": {
        "aufenthaltstitel": {}
      },
      "kinder": [],
      "rentenversicherung": {
        "anschrift": {}
      },
      "bonitaetsangaben": {
        "ausgaben": {},
        "einnahmen": {
          "monatlicheEinnahmen": {
            "regelmaessigesUnselbstaendigesEinkommen": 3000,
            "mietUndPachteinnahmen": {}
          },
          "jaehrlicheEinnahmen": {
            "einkommenAusSelbstaendigkeit": {
              "zuVersteuerndesEinkommen": {},
              "einkommenssteuer": {},
              "abschreibungen": {}
            }
          }
        },
        "vermoegen": {
          "immobilien": []
        },
        "verbindlichkeiten": {
          "ratenkredite": [],
          "sonstigeVerbindlichkeiten": [],
          "leasings": [],
          "kreditkarten": [],
          "dispositionskredite": [],
          "immobiliendarlehen": [],
          "geschaeftskredite": [],
          "kontokorrentkredite": []
        }
      }
    }
  ],
  "gemeinsameAntragstellerangaben": {
    "bonitaetsangaben": {
      "ausgaben": {},
      "einnahmen": {
        "monatlicheEinnahmen": {
          "mietUndPachteinnahmen": {}
        }
      },
      "vermoegen": {
        "immobilien": []
      },
      "verbindlichkeiten": {
        "ratenkredite": [],
        "sonstigeVerbindlichkeiten": [],
        "leasings": [],
        "kreditkarten": [],
        "dispositionskredite": [],
        "immobiliendarlehen": [],
        "geschaeftskredite": [],
        "kontokorrentkredite": []
      }
    },
    "kinder": []
  },
  "finanzierungswunsch": {
    "kreditwunsch": {
      "finanzierungszweck": "MODERNISIERUNG_UND_WOHNEN",
      "auszahlungsbetrag": 25000,
      "ratenzahlungstermin": "ULTIMO",
      "laufzeitInMonaten": 60
    },
    "versicherungsWunsch": [],
    "konto": {
      "kontoinhaberIds": []
    },
    "abzuloesendeVerbindlichkeiten": {
      "ratenkredite": [],
      "sonstigeVerbindlichkeiten": [],
      "kreditkarten": [],
      "dispositionskredite": [],
      "geschaeftskredite": []
    },
    "fahrzeug": {}
  },
  "kundenbetreuer": {
    "partnerId": "ABC12",
    "firmenname": "Beispiel AG",
    "vorname": "Beispiel Vorname",
    "nachname": "Beispiel Nachname",
    "anschrift": {
      "strasse": "Beispielstr.",
      "hausnummer": "42",
      "postleitzahl": "10179",
      "ort": "Berlin"
    },
    "telefon": "030 123456",
    "email": "beispiel@beispiel.de",
    "iban": "DE75201207003100124444",
    "anrede": "HERR"
  },
  "metadaten": {
    "traceId": "ks-84d56ccf",
    "vorgangsnummer": "Q32CU4"
  },
  "featureToggles": [
    {
      "id": "MOD_DARLEHEN",
      "aktiv": true
    }
  ],
  "handelsbeziehungen": [
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "kreditProvisionswunsch": 0.02,
      "vertriebsgruppe": "creditfair"
    }
  ]
}
```

</p>
</details>

<details><summary>Response</summary>
<p>

```json
{
  "supportMeldung": null,
  "angebote": [
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "referenznummerProduktanbieter": null,
      "referenznummerDienstleister": null,
      "produktbezeichnung": "Modernisierungsdarlehen",
      "produktart": "MODERNISIERUNGSKREDIT",
      "angebotsvariantentyp": "ZinsGarant15_Mod_Neo_16",
      "gesamtkonditionen": {
        "effektivzinssatz": 0.038,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32975.37,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 187,
        "rateProMonat": 177.83,
        "vertragsbeginn": "2019-10-01"
      },
      "kredit": {
        "effektivzinssatz": 0.038,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32975.37,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 94,
        "rateProMonat": 64.58,
        "letzteRate": 64.58,
        "provisionsbetrag": 375.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "vorlaufzinsenProTag": 0.0,
        "versicherung": null
      },
      "bausparvertrag": {
        "tarifname": "AL_Neo Klassik (1.6 %)",
        "bausparsumme": 25000.0,
        "gesamtlaufzeitInMonaten": 187,
        "zuteilungsZeitpunkt": "2027-07-31",
        "provision": 450.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "jahresentgelt": 15.0,
        "abschlussgebuehr": 400.0,
        "sparphase": {
          "sparbeitragMonatlich": 113.25,
          "dauerInMonaten": 94,
          "guthabenBeiZuteilung": 10088.01,
          "guthabenZinssatz": 0.002
        },
        "darlehensphase": {
          "darlehenssumme": 14911.99,
          "rateMonatlich": 177.83,
          "dauerInMonaten": 93,
          "sollzinsSatz": 0.0245,
          "effektivzinsSatz": 0.0292,
          "letzteRate": 12.24,
          "tilgungsende": "2035-04-30"
        }
      },
      "status": {
        "machbarkeitsstatus": "MACHBAR",
        "angepasst": true
      },
      "meldungen": [
        {
          "kategorie": "ANPASSUNG",
          "text": "Der Provisionswunsch wurde angepasst.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Die Laufzeit wurde angepasst.",
          "code": null
        }
      ],
      "unterlagen": [
        {
          "code": null,
          "text": "Baufinanzierungsvertrag von allen unterzeichnet zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Unterzeichneter, vollständiger Darlehensantrag",
          "referenz": null
        },
        {
          "code": null,
          "text": "Auszahlungsanweisung inkl. ausgefülltes und vom Kontoinhaber unterschriebenes SEPA-Lastschriftmandat",
          "referenz": null
        },
        {
          "code": null,
          "text": "Abschluss des entsprechenden Bausparvertrages im Tarif AL_Neo Klassik in Höhe des Vorausdarlehens",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollwirksame Verpfändung für diesen Bausparvertrag, d.h. vom Sicherungsgeber unterzeichnetes Formular zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollmacht zur Einholung eines Grundbuchauszuges durch die ALTE LEIPZIGER Bauspar AG",
          "referenz": null
        },
        {
          "code": null,
          "text": "Kopien der Personalausweise oder Reisepässe aller Darlehensnehmer (Vorder- und Rückseite)",
          "referenz": null
        },
        {
          "code": null,
          "text": "Letzte Gehaltsabrechnung sowie Dezember Gehaltsabrechnung des Vorjahres mit kumulierten Jahreswerten bzw. Nachweise über Renteneinkünfte aller Darlehensnehmer",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollständige Legitimationsprüfung aller Darlehensnehmer auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Bestätigung der wohnwirtschaftlichen Verwendung des Darlehens auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vorlage der Darlehensverträge für Ratenkredite und für Immobiliardarlehen, soweit vorhanden",
          "referenz": null
        }
      ],
      "bonitaetscheck": {
        "name": "Haushaltsrechnung",
        "ueberschrift": "Alte Leipziger Bauspar AG",
        "ueberschuss": 3422.17,
        "bloecke": [
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Unselbständiges Nettoeinkommen",
                "wert": 6000.0
              }
            ],
            "titel": "Einnahmen",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Einnahmen",
                  "wert": 6000.0
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Lebenshaltungskosten",
                "wert": 2400.0
              },
              {
                "hervorgehoben": false,
                "label": "Rate der Finanzierung",
                "wert": 177.83
              }
            ],
            "titel": "Ausgaben",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Ausgaben",
                  "wert": 2577.83
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": null,
            "titel": "Überschuss / Fehlbetrag",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Überschuss",
                  "wert": 3422.17
                }
              ],
              "hervorgehoben": true
            }
          }
        ]
      },
      "tilgungsplanBausparvertragMitVorausdarlehen": {
        "sparphase": {
          "eintraege": [
            {
              "jahr": 2019,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": -400.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -286.75
            },
            {
              "jahr": 2019,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -173.5
            },
            {
              "jahr": 2019,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -60.25
            },
            {
              "jahr": 2020,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 1.14,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 1284.89
            },
            {
              "jahr": 2021,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 3.79,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 2632.68
            },
            {
              "jahr": 2022,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 6.48,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 3983.16
            },
            {
              "jahr": 2023,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 9.18,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 5336.34
            },
            {
              "jahr": 2024,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 11.89,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 6692.23
            },
            {
              "jahr": 2025,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 14.6,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 8050.83
            },
            {
              "jahr": 2026,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 17.32,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 9412.15
            },
            {
              "jahr": 2027,
              "monat": null,
              "gesamtrate": 1131.56,
              "vorausdarlehenSollzinsen": -452.06,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": 679.5,
              "bausparvertragGuthabenzinsen": 11.36,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16602.77,
            "vorausdarlehenSollzinsen": -6070.52,
            "vorausdarlehenSaldo": -25000.0,
            "bausparvertragEinzahlungen": 10532.25,
            "bausparvertragGuthabenzinsen": 75.76,
            "bausparvertragGebuehren": -520.0,
            "bausparvertragTilgung": null,
            "bausparvertragSollzinsen": null,
            "bausparvertragSaldo": 10088.01
          }
        },
        "darlehensphase": {
          "eintraege": [
            {
              "jahr": 2027,
              "monat": 7,
              "gesamtrate": 0.0,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 0.0,
              "bausparvertragSollzinsen": 0.0,
              "bausparvertragSaldo": -14911.99
            },
            {
              "jahr": 2027,
              "monat": 8,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.38,
              "bausparvertragSollzinsen": -30.45,
              "bausparvertragSaldo": -14764.61
            },
            {
              "jahr": 2027,
              "monat": 9,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.69,
              "bausparvertragSollzinsen": -30.14,
              "bausparvertragSaldo": -14616.92
            },
            {
              "jahr": 2027,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.99,
              "bausparvertragSollzinsen": -29.84,
              "bausparvertragSaldo": -14468.93
            },
            {
              "jahr": 2027,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.29,
              "bausparvertragSollzinsen": -29.54,
              "bausparvertragSaldo": -14320.64
            },
            {
              "jahr": 2027,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.59,
              "bausparvertragSollzinsen": -29.24,
              "bausparvertragSaldo": -14172.05
            },
            {
              "jahr": 2028,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1806.94,
              "bausparvertragSollzinsen": -327.02,
              "bausparvertragSaldo": -12365.11
            },
            {
              "jahr": 2029,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1851.71,
              "bausparvertragSollzinsen": -282.25,
              "bausparvertragSaldo": -10513.4
            },
            {
              "jahr": 2030,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1897.59,
              "bausparvertragSollzinsen": -236.37,
              "bausparvertragSaldo": -8615.81
            },
            {
              "jahr": 2031,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1944.61,
              "bausparvertragSollzinsen": -189.35,
              "bausparvertragSaldo": -6671.2
            },
            {
              "jahr": 2032,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1992.78,
              "bausparvertragSollzinsen": -141.18,
              "bausparvertragSaldo": -4678.42
            },
            {
              "jahr": 2033,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2042.19,
              "bausparvertragSollzinsen": -91.77,
              "bausparvertragSaldo": -2636.23
            },
            {
              "jahr": 2034,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2092.77,
              "bausparvertragSollzinsen": -41.19,
              "bausparvertragSaldo": -543.46
            },
            {
              "jahr": 2035,
              "monat": null,
              "gesamtrate": 545.73,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 543.46,
              "bausparvertragSollzinsen": -2.27,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16372.6,
            "vorausdarlehenSollzinsen": null,
            "vorausdarlehenSaldo": null,
            "bausparvertragEinzahlungen": null,
            "bausparvertragGuthabenzinsen": null,
            "bausparvertragGebuehren": null,
            "bausparvertragTilgung": 14911.99,
            "bausparvertragSollzinsen": -1460.61,
            "bausparvertragSaldo": 0.0
          }
        }
      },
      "maximalerAuszahlungsbetrag": null
    },
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "referenznummerProduktanbieter": null,
      "referenznummerDienstleister": null,
      "produktbezeichnung": "Modernisierungsdarlehen",
      "produktart": "MODERNISIERUNGSKREDIT",
      "angebotsvariantentyp": "ZinsGarant15_Mod_Neo",
      "gesamtkonditionen": {
        "effektivzinssatz": 0.0372,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32713.55,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 185,
        "rateProMonat": 177.83,
        "vertragsbeginn": "2019-10-01"
      },
      "kredit": {
        "effektivzinssatz": 0.0372,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32713.55,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 92,
        "rateProMonat": 64.58,
        "letzteRate": 64.58,
        "provisionsbetrag": 375.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "vorlaufzinsenProTag": 0.0,
        "versicherung": null
      },
      "bausparvertrag": {
        "tarifname": "AL_Neo Klassik (1.0 %)",
        "bausparsumme": 25000.0,
        "gesamtlaufzeitInMonaten": 185,
        "zuteilungsZeitpunkt": "2027-05-31",
        "provision": 300.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "jahresentgelt": 15.0,
        "abschlussgebuehr": 250.0,
        "sparphase": {
          "sparbeitragMonatlich": 113.25,
          "dauerInMonaten": 92,
          "guthabenBeiZuteilung": 10010.37,
          "guthabenZinssatz": 0.002
        },
        "darlehensphase": {
          "darlehenssumme": 14989.63,
          "rateMonatlich": 177.83,
          "dauerInMonaten": 93,
          "sollzinsSatz": 0.0245,
          "effektivzinsSatz": 0.0275,
          "letzteRate": 106.08,
          "tilgungsende": "2035-02-28"
        }
      },
      "status": {
        "machbarkeitsstatus": "MACHBAR",
        "angepasst": true
      },
      "meldungen": [
        {
          "kategorie": "ANPASSUNG",
          "text": "Der Provisionswunsch wurde angepasst.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Die Laufzeit wurde angepasst.",
          "code": null
        }
      ],
      "unterlagen": [
        {
          "code": null,
          "text": "Baufinanzierungsvertrag von allen unterzeichnet zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Unterzeichneter, vollständiger Darlehensantrag",
          "referenz": null
        },
        {
          "code": null,
          "text": "Auszahlungsanweisung inkl. ausgefülltes und vom Kontoinhaber unterschriebenes SEPA-Lastschriftmandat",
          "referenz": null
        },
        {
          "code": null,
          "text": "Abschluss des entsprechenden Bausparvertrages im Tarif AL_Neo Klassik in Höhe des Vorausdarlehens",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollwirksame Verpfändung für diesen Bausparvertrag, d.h. vom Sicherungsgeber unterzeichnetes Formular zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollmacht zur Einholung eines Grundbuchauszuges durch die ALTE LEIPZIGER Bauspar AG",
          "referenz": null
        },
        {
          "code": null,
          "text": "Kopien der Personalausweise oder Reisepässe aller Darlehensnehmer (Vorder- und Rückseite)",
          "referenz": null
        },
        {
          "code": null,
          "text": "Letzte Gehaltsabrechnung sowie Dezember Gehaltsabrechnung des Vorjahres mit kumulierten Jahreswerten bzw. Nachweise über Renteneinkünfte aller Darlehensnehmer",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollständige Legitimationsprüfung aller Darlehensnehmer auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Bestätigung der wohnwirtschaftlichen Verwendung des Darlehens auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vorlage der Darlehensverträge für Ratenkredite und für Immobiliardarlehen, soweit vorhanden",
          "referenz": null
        }
      ],
      "bonitaetscheck": {
        "name": "Haushaltsrechnung",
        "ueberschrift": "Alte Leipziger Bauspar AG",
        "ueberschuss": 3422.17,
        "bloecke": [
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Unselbständiges Nettoeinkommen",
                "wert": 6000.0
              }
            ],
            "titel": "Einnahmen",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Einnahmen",
                  "wert": 6000.0
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Lebenshaltungskosten",
                "wert": 2400.0
              },
              {
                "hervorgehoben": false,
                "label": "Rate der Finanzierung",
                "wert": 177.83
              }
            ],
            "titel": "Ausgaben",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Ausgaben",
                  "wert": 2577.83
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": null,
            "titel": "Überschuss / Fehlbetrag",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Überschuss",
                  "wert": 3422.17
                }
              ],
              "hervorgehoben": true
            }
          }
        ]
      },
      "tilgungsplanBausparvertragMitVorausdarlehen": {
        "sparphase": {
          "eintraege": [
            {
              "jahr": 2019,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": -250.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -136.75
            },
            {
              "jahr": 2019,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -23.5
            },
            {
              "jahr": 2019,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 89.75
            },
            {
              "jahr": 2020,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 1.4,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 1435.15
            },
            {
              "jahr": 2021,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 4.09,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 2783.24
            },
            {
              "jahr": 2022,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 6.78,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 4134.02
            },
            {
              "jahr": 2023,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 9.49,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 5487.51
            },
            {
              "jahr": 2024,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 12.19,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 6843.7
            },
            {
              "jahr": 2025,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 14.9,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 8202.6
            },
            {
              "jahr": 2026,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 17.62,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 9564.22
            },
            {
              "jahr": 2027,
              "monat": null,
              "gesamtrate": 775.9,
              "vorausdarlehenSollzinsen": -322.9,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": 453.0,
              "bausparvertragGuthabenzinsen": 8.15,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16247.11,
            "vorausdarlehenSollzinsen": -5941.36,
            "vorausdarlehenSaldo": -25000.0,
            "bausparvertragEinzahlungen": 10305.75,
            "bausparvertragGuthabenzinsen": 74.62,
            "bausparvertragGebuehren": -370.0,
            "bausparvertragTilgung": null,
            "bausparvertragSollzinsen": null,
            "bausparvertragSaldo": 10010.37
          }
        },
        "darlehensphase": {
          "eintraege": [
            {
              "jahr": 2027,
              "monat": 5,
              "gesamtrate": 0.0,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 0.0,
              "bausparvertragSollzinsen": 0.0,
              "bausparvertragSaldo": -14989.63
            },
            {
              "jahr": 2027,
              "monat": 6,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.23,
              "bausparvertragSollzinsen": -30.6,
              "bausparvertragSaldo": -14842.4
            },
            {
              "jahr": 2027,
              "monat": 7,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.53,
              "bausparvertragSollzinsen": -30.3,
              "bausparvertragSaldo": -14694.87
            },
            {
              "jahr": 2027,
              "monat": 8,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.83,
              "bausparvertragSollzinsen": -30.0,
              "bausparvertragSaldo": -14547.04
            },
            {
              "jahr": 2027,
              "monat": 9,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.13,
              "bausparvertragSollzinsen": -29.7,
              "bausparvertragSaldo": -14398.91
            },
            {
              "jahr": 2027,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.43,
              "bausparvertragSollzinsen": -29.4,
              "bausparvertragSaldo": -14250.48
            },
            {
              "jahr": 2027,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.74,
              "bausparvertragSollzinsen": -29.09,
              "bausparvertragSaldo": -14101.74
            },
            {
              "jahr": 2027,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 149.04,
              "bausparvertragSollzinsen": -28.79,
              "bausparvertragSaldo": -13952.7
            },
            {
              "jahr": 2028,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1812.37,
              "bausparvertragSollzinsen": -321.59,
              "bausparvertragSaldo": -12140.33
            },
            {
              "jahr": 2029,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1857.29,
              "bausparvertragSollzinsen": -276.67,
              "bausparvertragSaldo": -10283.04
            },
            {
              "jahr": 2030,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1903.32,
              "bausparvertragSollzinsen": -230.64,
              "bausparvertragSaldo": -8379.72
            },
            {
              "jahr": 2031,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1950.47,
              "bausparvertragSollzinsen": -183.49,
              "bausparvertragSaldo": -6429.25
            },
            {
              "jahr": 2032,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1998.77,
              "bausparvertragSollzinsen": -135.19,
              "bausparvertragSaldo": -4430.48
            },
            {
              "jahr": 2033,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2048.29,
              "bausparvertragSollzinsen": -85.67,
              "bausparvertragSaldo": -2382.19
            },
            {
              "jahr": 2034,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2099.06,
              "bausparvertragSollzinsen": -34.9,
              "bausparvertragSaldo": -283.13
            },
            {
              "jahr": 2035,
              "monat": null,
              "gesamtrate": 283.91,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 283.13,
              "bausparvertragSollzinsen": -0.78,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16466.44,
            "vorausdarlehenSollzinsen": null,
            "vorausdarlehenSaldo": null,
            "bausparvertragEinzahlungen": null,
            "bausparvertragGuthabenzinsen": null,
            "bausparvertragGebuehren": null,
            "bausparvertragTilgung": 14989.63,
            "bausparvertragSollzinsen": -1476.81,
            "bausparvertragSaldo": 0.0
          }
        }
      },
      "maximalerAuszahlungsbetrag": null
    }
  ]
}
```

</p>
</details>

### Vollständiges Angebot (mehrere Antragsteller in getrennten Haushalt)

<details><summary>Request</summary>
<p>

```json
{
  "antragsteller": [
    {
      "id": "552a2e18-b407-44ce-8af5-f6334cc64f80",
      "persoenlicheAngaben": {
        "anrede": "HERR",
        "vorname": "Beispiel Vorname",
        "nachname": "Beispiel Nachname",
        "geburtsdatum": "1970-01-01",
        "geburtsort": "Berlin",
        "staatsangehoerigkeit": "DE",
        "familienstand": "VERHEIRATET",
        "anzahlPersonenImHaushalt": 1
      },
      "derzeitigeBeschaeftigung": {
        "beschaeftigungsverhaeltnis": "ANGESTELLT",
        "befristet": "UNBEFRISTET",
        "beschaeftigtSeit": "2010-01-01",
        "beruf": "Angestellter",
        "branche": "HANDEL",
        "anschrift": {
          "strasse": "Beispielstr.",
          "hausnummer": "43",
          "postleitzahl": "10179",
          "ort": "Berlin",
          "land": "DE"
        },
        "arbeitgebername": "Beispiel AG"
      },
      "vorherigeBeschaeftigung": {
        "anschrift": {}
      },
      "derzeitigeWohnsituation": {
        "wohnart": "IM_EIGENEN_HAUS",
        "wohnhaftSeit": "2000-01-01",
        "anschrift": {
          "strasse": "Beispielstr.",
          "hausnummer": "42",
          "postleitzahl": "10179",
          "ort": "Berlin",
          "land": "DE"
        }
      },
      "kontakt": {
        "telefonPrivat": "030 123456",
        "telefonGeschaeftlich": "030 123456",
        "email": "beispiel@beispiel.de"
      },
      "herkunft": {
        "aufenthaltstitel": {}
      },
      "kinder": [],
      "rentenversicherung": {
        "anschrift": {}
      },
      "bonitaetsangaben": {
        "ausgaben": {},
        "einnahmen": {
          "monatlicheEinnahmen": {
            "regelmaessigesUnselbstaendigesEinkommen": 3000,
            "mietUndPachteinnahmen": {}
          },
          "jaehrlicheEinnahmen": {
            "einkommenAusSelbstaendigkeit": {
              "zuVersteuerndesEinkommen": {},
              "einkommenssteuer": {},
              "abschreibungen": {}
            }
          }
        },
        "vermoegen": {
          "immobilien": []
        },
        "verbindlichkeiten": {
          "ratenkredite": [],
          "sonstigeVerbindlichkeiten": [],
          "leasings": [],
          "kreditkarten": [],
          "dispositionskredite": [],
          "immobiliendarlehen": [],
          "geschaeftskredite": [],
          "kontokorrentkredite": []
        }
      }
    },
    {
      "id": "21794c8f-ad7c-442f-9bd5-1449951acd82",
      "persoenlicheAngaben": {
        "anrede": "FRAU",
        "vorname": "Beispiel Vorname 2",
        "nachname": "Beispiel Nachname",
        "geburtsdatum": "1970-07-01",
        "geburtsort": "Berlin",
        "staatsangehoerigkeit": "DE",
        "familienstand": "VERHEIRATET",
        "anzahlPersonenImHaushalt": 1
      },
      "derzeitigeBeschaeftigung": {
        "beschaeftigungsverhaeltnis": "ANGESTELLT",
        "befristet": "UNBEFRISTET",
        "beschaeftigtSeit": "2010-01-01",
        "beruf": "Angestellter",
        "branche": "HANDEL",
        "anschrift": {
          "strasse": "Beispielstr",
          "hausnummer": "43",
          "postleitzahl": "10179",
          "ort": "Berlin",
          "land": "DE"
        },
        "arbeitgebername": "Beispiel AG"
      },
      "vorherigeBeschaeftigung": {
        "anschrift": {}
      },
      "derzeitigeWohnsituation": {
        "wohnart": "ZUR_MIETE",
        "wohnhaftSeit": "2000-01-01",
        "anschrift": {
          "strasse": "Beispielstr",
          "hausnummer": "44",
          "postleitzahl": "10179",
          "ort": "Berlin",
          "land": "DE"
        }
      },
      "kontakt": {
        "telefonPrivat": "030 123456",
        "telefonGeschaeftlich": "030 123456",
        "email": "beispiel2@beispiel.de"
      },
      "herkunft": {
        "aufenthaltstitel": {}
      },
      "kinder": [],
      "rentenversicherung": {
        "anschrift": {}
      },
      "bonitaetsangaben": {
        "ausgaben": {},
        "einnahmen": {
          "monatlicheEinnahmen": {
            "regelmaessigesUnselbstaendigesEinkommen": 3000,
            "mietUndPachteinnahmen": {}
          },
          "jaehrlicheEinnahmen": {
            "einkommenAusSelbstaendigkeit": {
              "zuVersteuerndesEinkommen": {},
              "einkommenssteuer": {},
              "abschreibungen": {}
            }
          }
        },
        "vermoegen": {
          "immobilien": []
        },
        "verbindlichkeiten": {
          "ratenkredite": [],
          "sonstigeVerbindlichkeiten": [],
          "leasings": [],
          "kreditkarten": [],
          "dispositionskredite": [],
          "immobiliendarlehen": [],
          "geschaeftskredite": [],
          "kontokorrentkredite": []
        }
      }
    }
  ],
  "gemeinsameAntragstellerangaben": {
    "bonitaetsangaben": {
      "ausgaben": {},
      "einnahmen": {
        "monatlicheEinnahmen": {
          "mietUndPachteinnahmen": {}
        }
      },
      "vermoegen": {
        "immobilien": []
      },
      "verbindlichkeiten": {
        "ratenkredite": [],
        "sonstigeVerbindlichkeiten": [],
        "leasings": [],
        "kreditkarten": [],
        "dispositionskredite": [],
        "immobiliendarlehen": [],
        "geschaeftskredite": [],
        "kontokorrentkredite": []
      }
    },
    "kinder": []
  },
  "finanzierungswunsch": {
    "kreditwunsch": {
      "finanzierungszweck": "MODERNISIERUNG_UND_WOHNEN",
      "auszahlungsbetrag": 25000,
      "ratenzahlungstermin": "ULTIMO",
      "laufzeitInMonaten": 60
    },
    "versicherungsWunsch": [],
    "konto": {
      "kontoinhaberIds": []
    },
    "abzuloesendeVerbindlichkeiten": {
      "ratenkredite": [],
      "sonstigeVerbindlichkeiten": [],
      "kreditkarten": [],
      "dispositionskredite": [],
      "geschaeftskredite": []
    },
    "fahrzeug": {}
  },
  "kundenbetreuer": {
    "partnerId": "ABC12",
    "firmenname": "Beispiel AG",
    "vorname": "Beispiel Vorname",
    "nachname": "Beispiel Nachname",
    "anschrift": {
      "strasse": "Beispielstr.",
      "hausnummer": "42",
      "postleitzahl": "10179",
      "ort": "Berlin"
    },
    "telefon": "030 123456",
    "email": "beispiel@beispiel.de",
    "iban": "DE75201207003100124444",
    "anrede": "HERR"
  },
  "metadaten": {
    "traceId": "ks-194ecf3e",
    "vorgangsnummer": "Q32CU4"
  },
  "featureToggles": [
    {
      "id": "MOD_DARLEHEN",
      "aktiv": true
    }
  ],
  "handelsbeziehungen": [
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "kreditProvisionswunsch": 0.02,
      "vertriebsgruppe": "creditfair"
    }
  ]
}
```

</p>
</details>

<details><summary>Response</summary>
<p>

```json
{
  "supportMeldung": null,
  "angebote": [
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "referenznummerProduktanbieter": null,
      "referenznummerDienstleister": null,
      "produktbezeichnung": "Modernisierungsdarlehen",
      "produktart": "MODERNISIERUNGSKREDIT",
      "angebotsvariantentyp": "ZinsGarant15_Mod_Neo_16",
      "gesamtkonditionen": {
        "effektivzinssatz": 0.038,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32975.37,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 187,
        "rateProMonat": 177.83,
        "vertragsbeginn": "2019-10-01"
      },
      "kredit": {
        "effektivzinssatz": 0.038,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32975.37,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 94,
        "rateProMonat": 64.58,
        "letzteRate": 64.58,
        "provisionsbetrag": 375.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "vorlaufzinsenProTag": 0.0,
        "versicherung": null
      },
      "bausparvertrag": {
        "tarifname": "AL_Neo Klassik (1.6 %)",
        "bausparsumme": 25000.0,
        "gesamtlaufzeitInMonaten": 187,
        "zuteilungsZeitpunkt": "2027-07-31",
        "provision": 450.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "jahresentgelt": 15.0,
        "abschlussgebuehr": 400.0,
        "sparphase": {
          "sparbeitragMonatlich": 113.25,
          "dauerInMonaten": 94,
          "guthabenBeiZuteilung": 10088.01,
          "guthabenZinssatz": 0.002
        },
        "darlehensphase": {
          "darlehenssumme": 14911.99,
          "rateMonatlich": 177.83,
          "dauerInMonaten": 93,
          "sollzinsSatz": 0.0245,
          "effektivzinsSatz": 0.0292,
          "letzteRate": 12.24,
          "tilgungsende": "2035-04-30"
        }
      },
      "status": {
        "machbarkeitsstatus": "NICHT_MACHBAR",
        "angepasst": true
      },
      "meldungen": [
        {
          "kategorie": "MACHBARKEIT",
          "text": "Beide Antragsteller müssen in einem Haushalt leben.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Der Provisionswunsch wurde angepasst.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Die Laufzeit wurde angepasst.",
          "code": null
        }
      ],
      "unterlagen": [
        {
          "code": null,
          "text": "Baufinanzierungsvertrag von allen unterzeichnet zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Unterzeichneter, vollständiger Darlehensantrag",
          "referenz": null
        },
        {
          "code": null,
          "text": "Auszahlungsanweisung inkl. ausgefülltes und vom Kontoinhaber unterschriebenes SEPA-Lastschriftmandat",
          "referenz": null
        },
        {
          "code": null,
          "text": "Abschluss des entsprechenden Bausparvertrages im Tarif AL_Neo Klassik in Höhe des Vorausdarlehens",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollwirksame Verpfändung für diesen Bausparvertrag, d.h. vom Sicherungsgeber unterzeichnetes Formular zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollmacht zur Einholung eines Grundbuchauszuges durch die ALTE LEIPZIGER Bauspar AG",
          "referenz": null
        },
        {
          "code": null,
          "text": "Kopien der Personalausweise oder Reisepässe aller Darlehensnehmer (Vorder- und Rückseite)",
          "referenz": null
        },
        {
          "code": null,
          "text": "Letzte Gehaltsabrechnung sowie Dezember Gehaltsabrechnung des Vorjahres mit kumulierten Jahreswerten bzw. Nachweise über Renteneinkünfte aller Darlehensnehmer",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollständige Legitimationsprüfung aller Darlehensnehmer auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Bestätigung der wohnwirtschaftlichen Verwendung des Darlehens auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vorlage der Darlehensverträge für Ratenkredite und für Immobiliardarlehen, soweit vorhanden",
          "referenz": null
        }
      ],
      "bonitaetscheck": {
        "name": "Haushaltsrechnung",
        "ueberschrift": "Alte Leipziger Bauspar AG",
        "ueberschuss": 3422.17,
        "bloecke": [
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Unselbständiges Nettoeinkommen",
                "wert": 6000.0
              }
            ],
            "titel": "Einnahmen",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Einnahmen",
                  "wert": 6000.0
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Lebenshaltungskosten",
                "wert": 2400.0
              },
              {
                "hervorgehoben": false,
                "label": "Rate der Finanzierung",
                "wert": 177.83
              }
            ],
            "titel": "Ausgaben",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Ausgaben",
                  "wert": 2577.83
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": null,
            "titel": "Überschuss / Fehlbetrag",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Überschuss",
                  "wert": 3422.17
                }
              ],
              "hervorgehoben": true
            }
          }
        ]
      },
      "tilgungsplanBausparvertragMitVorausdarlehen": {
        "sparphase": {
          "eintraege": [
            {
              "jahr": 2019,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": -400.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -286.75
            },
            {
              "jahr": 2019,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -173.5
            },
            {
              "jahr": 2019,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -60.25
            },
            {
              "jahr": 2020,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 1.14,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 1284.89
            },
            {
              "jahr": 2021,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 3.79,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 2632.68
            },
            {
              "jahr": 2022,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 6.48,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 3983.16
            },
            {
              "jahr": 2023,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 9.18,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 5336.34
            },
            {
              "jahr": 2024,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 11.89,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 6692.23
            },
            {
              "jahr": 2025,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 14.6,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 8050.83
            },
            {
              "jahr": 2026,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 17.32,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 9412.15
            },
            {
              "jahr": 2027,
              "monat": null,
              "gesamtrate": 1131.56,
              "vorausdarlehenSollzinsen": -452.06,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": 679.5,
              "bausparvertragGuthabenzinsen": 11.36,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16602.77,
            "vorausdarlehenSollzinsen": -6070.52,
            "vorausdarlehenSaldo": -25000.0,
            "bausparvertragEinzahlungen": 10532.25,
            "bausparvertragGuthabenzinsen": 75.76,
            "bausparvertragGebuehren": -520.0,
            "bausparvertragTilgung": null,
            "bausparvertragSollzinsen": null,
            "bausparvertragSaldo": 10088.01
          }
        },
        "darlehensphase": {
          "eintraege": [
            {
              "jahr": 2027,
              "monat": 7,
              "gesamtrate": 0.0,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 0.0,
              "bausparvertragSollzinsen": 0.0,
              "bausparvertragSaldo": -14911.99
            },
            {
              "jahr": 2027,
              "monat": 8,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.38,
              "bausparvertragSollzinsen": -30.45,
              "bausparvertragSaldo": -14764.61
            },
            {
              "jahr": 2027,
              "monat": 9,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.69,
              "bausparvertragSollzinsen": -30.14,
              "bausparvertragSaldo": -14616.92
            },
            {
              "jahr": 2027,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.99,
              "bausparvertragSollzinsen": -29.84,
              "bausparvertragSaldo": -14468.93
            },
            {
              "jahr": 2027,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.29,
              "bausparvertragSollzinsen": -29.54,
              "bausparvertragSaldo": -14320.64
            },
            {
              "jahr": 2027,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.59,
              "bausparvertragSollzinsen": -29.24,
              "bausparvertragSaldo": -14172.05
            },
            {
              "jahr": 2028,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1806.94,
              "bausparvertragSollzinsen": -327.02,
              "bausparvertragSaldo": -12365.11
            },
            {
              "jahr": 2029,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1851.71,
              "bausparvertragSollzinsen": -282.25,
              "bausparvertragSaldo": -10513.4
            },
            {
              "jahr": 2030,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1897.59,
              "bausparvertragSollzinsen": -236.37,
              "bausparvertragSaldo": -8615.81
            },
            {
              "jahr": 2031,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1944.61,
              "bausparvertragSollzinsen": -189.35,
              "bausparvertragSaldo": -6671.2
            },
            {
              "jahr": 2032,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1992.78,
              "bausparvertragSollzinsen": -141.18,
              "bausparvertragSaldo": -4678.42
            },
            {
              "jahr": 2033,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2042.19,
              "bausparvertragSollzinsen": -91.77,
              "bausparvertragSaldo": -2636.23
            },
            {
              "jahr": 2034,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2092.77,
              "bausparvertragSollzinsen": -41.19,
              "bausparvertragSaldo": -543.46
            },
            {
              "jahr": 2035,
              "monat": null,
              "gesamtrate": 545.73,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 543.46,
              "bausparvertragSollzinsen": -2.27,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16372.6,
            "vorausdarlehenSollzinsen": null,
            "vorausdarlehenSaldo": null,
            "bausparvertragEinzahlungen": null,
            "bausparvertragGuthabenzinsen": null,
            "bausparvertragGebuehren": null,
            "bausparvertragTilgung": 14911.99,
            "bausparvertragSollzinsen": -1460.61,
            "bausparvertragSaldo": 0.0
          }
        }
      },
      "maximalerAuszahlungsbetrag": null
    },
    {
      "produktanbieter": "ALTE_LEIPZIGER_BAUSPAR",
      "referenznummerProduktanbieter": null,
      "referenznummerDienstleister": null,
      "produktbezeichnung": "Modernisierungsdarlehen",
      "produktart": "MODERNISIERUNGSKREDIT",
      "angebotsvariantentyp": "ZinsGarant15_Mod_Neo",
      "gesamtkonditionen": {
        "effektivzinssatz": 0.0372,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32713.55,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 185,
        "rateProMonat": 177.83,
        "vertragsbeginn": "2019-10-01"
      },
      "kredit": {
        "effektivzinssatz": 0.0372,
        "sollzinssatz": 0.031,
        "gesamtbetrag": 32713.55,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 92,
        "rateProMonat": 64.58,
        "letzteRate": 64.58,
        "provisionsbetrag": 375.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "vorlaufzinsenProTag": 0.0,
        "versicherung": null
      },
      "bausparvertrag": {
        "tarifname": "AL_Neo Klassik (1.0 %)",
        "bausparsumme": 25000.0,
        "gesamtlaufzeitInMonaten": 185,
        "zuteilungsZeitpunkt": "2027-05-31",
        "provision": 300.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "jahresentgelt": 15.0,
        "abschlussgebuehr": 250.0,
        "sparphase": {
          "sparbeitragMonatlich": 113.25,
          "dauerInMonaten": 92,
          "guthabenBeiZuteilung": 10010.37,
          "guthabenZinssatz": 0.002
        },
        "darlehensphase": {
          "darlehenssumme": 14989.63,
          "rateMonatlich": 177.83,
          "dauerInMonaten": 93,
          "sollzinsSatz": 0.0245,
          "effektivzinsSatz": 0.0275,
          "letzteRate": 106.08,
          "tilgungsende": "2035-02-28"
        }
      },
      "status": {
        "machbarkeitsstatus": "NICHT_MACHBAR",
        "angepasst": true
      },
      "meldungen": [
        {
          "kategorie": "MACHBARKEIT",
          "text": "Beide Antragsteller müssen in einem Haushalt leben.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Der Provisionswunsch wurde angepasst.",
          "code": null
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Die Laufzeit wurde angepasst.",
          "code": null
        }
      ],
      "unterlagen": [
        {
          "code": null,
          "text": "Baufinanzierungsvertrag von allen unterzeichnet zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Unterzeichneter, vollständiger Darlehensantrag",
          "referenz": null
        },
        {
          "code": null,
          "text": "Auszahlungsanweisung inkl. ausgefülltes und vom Kontoinhaber unterschriebenes SEPA-Lastschriftmandat",
          "referenz": null
        },
        {
          "code": null,
          "text": "Abschluss des entsprechenden Bausparvertrages im Tarif AL_Neo Klassik in Höhe des Vorausdarlehens",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollwirksame Verpfändung für diesen Bausparvertrag, d.h. vom Sicherungsgeber unterzeichnetes Formular zurück",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollmacht zur Einholung eines Grundbuchauszuges durch die ALTE LEIPZIGER Bauspar AG",
          "referenz": null
        },
        {
          "code": null,
          "text": "Kopien der Personalausweise oder Reisepässe aller Darlehensnehmer (Vorder- und Rückseite)",
          "referenz": null
        },
        {
          "code": null,
          "text": "Letzte Gehaltsabrechnung sowie Dezember Gehaltsabrechnung des Vorjahres mit kumulierten Jahreswerten bzw. Nachweise über Renteneinkünfte aller Darlehensnehmer",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vollständige Legitimationsprüfung aller Darlehensnehmer auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Bestätigung der wohnwirtschaftlichen Verwendung des Darlehens auf beiliegendem Formular durch den Geschäftspartner",
          "referenz": null
        },
        {
          "code": null,
          "text": "Vorlage der Darlehensverträge für Ratenkredite und für Immobiliardarlehen, soweit vorhanden",
          "referenz": null
        }
      ],
      "bonitaetscheck": {
        "name": "Haushaltsrechnung",
        "ueberschrift": "Alte Leipziger Bauspar AG",
        "ueberschuss": 3422.17,
        "bloecke": [
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Unselbständiges Nettoeinkommen",
                "wert": 6000.0
              }
            ],
            "titel": "Einnahmen",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Einnahmen",
                  "wert": 6000.0
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": [
              {
                "hervorgehoben": false,
                "label": "Lebenshaltungskosten",
                "wert": 2400.0
              },
              {
                "hervorgehoben": false,
                "label": "Rate der Finanzierung",
                "wert": 177.83
              }
            ],
            "titel": "Ausgaben",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Ausgaben",
                  "wert": 2577.83
                }
              ],
              "hervorgehoben": true
            }
          },
          {
            "zeilen": null,
            "titel": "Überschuss / Fehlbetrag",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Überschuss",
                  "wert": 3422.17
                }
              ],
              "hervorgehoben": true
            }
          }
        ]
      },
      "tilgungsplanBausparvertragMitVorausdarlehen": {
        "sparphase": {
          "eintraege": [
            {
              "jahr": 2019,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": -250.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -136.75
            },
            {
              "jahr": 2019,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -23.5
            },
            {
              "jahr": 2019,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": -64.58,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 113.25,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 89.75
            },
            {
              "jahr": 2020,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 1.4,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 1435.15
            },
            {
              "jahr": 2021,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 4.09,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 2783.24
            },
            {
              "jahr": 2022,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 6.78,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 4134.02
            },
            {
              "jahr": 2023,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 9.49,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 5487.51
            },
            {
              "jahr": 2024,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 12.19,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 6843.7
            },
            {
              "jahr": 2025,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 14.9,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 8202.6
            },
            {
              "jahr": 2026,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": -774.96,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 1359.0,
              "bausparvertragGuthabenzinsen": 17.62,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": 9564.22
            },
            {
              "jahr": 2027,
              "monat": null,
              "gesamtrate": 775.9,
              "vorausdarlehenSollzinsen": -322.9,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": 453.0,
              "bausparvertragGuthabenzinsen": 8.15,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16247.11,
            "vorausdarlehenSollzinsen": -5941.36,
            "vorausdarlehenSaldo": -25000.0,
            "bausparvertragEinzahlungen": 10305.75,
            "bausparvertragGuthabenzinsen": 74.62,
            "bausparvertragGebuehren": -370.0,
            "bausparvertragTilgung": null,
            "bausparvertragSollzinsen": null,
            "bausparvertragSaldo": 10010.37
          }
        },
        "darlehensphase": {
          "eintraege": [
            {
              "jahr": 2027,
              "monat": 5,
              "gesamtrate": 0.0,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 0.0,
              "bausparvertragSollzinsen": 0.0,
              "bausparvertragSaldo": -14989.63
            },
            {
              "jahr": 2027,
              "monat": 6,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.23,
              "bausparvertragSollzinsen": -30.6,
              "bausparvertragSaldo": -14842.4
            },
            {
              "jahr": 2027,
              "monat": 7,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.53,
              "bausparvertragSollzinsen": -30.3,
              "bausparvertragSaldo": -14694.87
            },
            {
              "jahr": 2027,
              "monat": 8,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 147.83,
              "bausparvertragSollzinsen": -30.0,
              "bausparvertragSaldo": -14547.04
            },
            {
              "jahr": 2027,
              "monat": 9,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.13,
              "bausparvertragSollzinsen": -29.7,
              "bausparvertragSaldo": -14398.91
            },
            {
              "jahr": 2027,
              "monat": 10,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.43,
              "bausparvertragSollzinsen": -29.4,
              "bausparvertragSaldo": -14250.48
            },
            {
              "jahr": 2027,
              "monat": 11,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 148.74,
              "bausparvertragSollzinsen": -29.09,
              "bausparvertragSaldo": -14101.74
            },
            {
              "jahr": 2027,
              "monat": 12,
              "gesamtrate": 177.83,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 149.04,
              "bausparvertragSollzinsen": -28.79,
              "bausparvertragSaldo": -13952.7
            },
            {
              "jahr": 2028,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1812.37,
              "bausparvertragSollzinsen": -321.59,
              "bausparvertragSaldo": -12140.33
            },
            {
              "jahr": 2029,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1857.29,
              "bausparvertragSollzinsen": -276.67,
              "bausparvertragSaldo": -10283.04
            },
            {
              "jahr": 2030,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1903.32,
              "bausparvertragSollzinsen": -230.64,
              "bausparvertragSaldo": -8379.72
            },
            {
              "jahr": 2031,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1950.47,
              "bausparvertragSollzinsen": -183.49,
              "bausparvertragSaldo": -6429.25
            },
            {
              "jahr": 2032,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 1998.77,
              "bausparvertragSollzinsen": -135.19,
              "bausparvertragSaldo": -4430.48
            },
            {
              "jahr": 2033,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2048.29,
              "bausparvertragSollzinsen": -85.67,
              "bausparvertragSaldo": -2382.19
            },
            {
              "jahr": 2034,
              "monat": null,
              "gesamtrate": 2133.96,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 2099.06,
              "bausparvertragSollzinsen": -34.9,
              "bausparvertragSaldo": -283.13
            },
            {
              "jahr": 2035,
              "monat": null,
              "gesamtrate": 283.91,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 283.13,
              "bausparvertragSollzinsen": -0.78,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16466.44,
            "vorausdarlehenSollzinsen": null,
            "vorausdarlehenSaldo": null,
            "bausparvertragEinzahlungen": null,
            "bausparvertragGuthabenzinsen": null,
            "bausparvertragGebuehren": null,
            "bausparvertragTilgung": 14989.63,
            "bausparvertragSollzinsen": -1476.81,
            "bausparvertragSaldo": 0.0
          }
        }
      },
      "maximalerAuszahlungsbetrag": null
    }
  ]
}
```

</p>
</details>