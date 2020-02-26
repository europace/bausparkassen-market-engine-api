## Anfrage mit minimalen Angaben

Die aufgelisteten Beispielanfragen und -antworten dienen zum besseren Verständnis der API. 

Die Beispielantworten sind fiktiv und gekürzt, sodass die Konditionen bspw. nicht mit dem Tilgungsplan übereinstimmen.   

Anmerkung zum Tilgungsplan:
- i.d.R. wird das erste Jahr monatsweise aufgelistet
- i.d.R. werden alle weiteren Jahre jeweils zu einem einzelnen Eintrag pro Jahr aggregiert
- die Beispielantworten enthalten lediglich die ersten beiden und den letzten Eintrag - die Dazwischenliegenden wurden entfernt  

### Request

Angabe von Kreditbetrag und Laufzeit
 
```json
{
  "antragsteller": [
    {
      "id": "f7de4f47-340e-4b1d-9e6f-45fc22fcc06e",
      "persoenlicheAngaben": {},
      "derzeitigeBeschaeftigung": {},
      "vorherigeBeschaeftigung": {},
      "derzeitigeWohnsituation": {
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
    "traceId": "ks-107bf09f",
    "vorgangsnummer": "AB1234"
  },
  "featureToggles": [],
  "handelsbeziehungen": [
    {
      "produktanbieter": "BEISPIEL_BANK",
      "kreditProvisionswunsch": 0.0123,
      "vertriebsgruppe": "Beispielgruppe"
    }
  ]
}
```

### Response

:warning: Die Beispielantworten sind fiktiv und gekürzt, sodass die Konditionen bspw. nicht mit dem Tilgungsplan übereinstimmen.

```json
{
  "supportMeldung": null,
  "angebote": [
    {
      "produktanbieter": "BEISPIEL_BANK",
      "referenznummerProduktanbieter": null,
      "referenznummerDienstleister": null,
      "produktbezeichnung": "Modernisierungsdarlehen",
      "produktart": "MODERNISIERUNGSKREDIT",
      "angebotsvariantentyp": "Beispielvariante",
      "gesamtkonditionen": {
        "effektivzinssatz": 0.0132,
        "sollzinssatz": 0.0123,
        "gesamtbetrag": 33000.0,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 187,
        "rateProMonat": 180.0,
        "vertragsbeginn": "2019-10-01"
      },
      "kredit": {
        "effektivzinssatz": 0.0132,
        "sollzinssatz": 0.0123,
        "gesamtbetrag": 33000.0,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 94,
        "rateProMonat": 60.0,
        "letzteRate": 60.0,
        "provisionsbetrag": 400.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "vorlaufzinsenProTag": 0.0,
        "versicherung": null
      },
      "bausparvertrag": {
        "tarifname": "Beispieltarif",
        "bausparsumme": 25000.0,
        "gesamtlaufzeitInMonaten": 187,
        "zuteilungsZeitpunkt": "2027-07-31",
        "provision": 500.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "jahresentgelt": 15.0,
        "abschlussgebuehr": 400.0,
        "sparphase": {
          "sparbeitragMonatlich": 100.0,
          "dauerInMonaten": 94,
          "guthabenBeiZuteilung": 10000.0,
          "guthabenZinssatz": 0.0123
        },
        "darlehensphase": {
          "darlehenssumme": 15000.0,
          "rateMonatlich": 180.0,
          "dauerInMonaten": 93,
          "sollzinsSatz": 0.0123,
          "effektivzinsSatz": 0.0132,
          "letzteRate": 12.0,
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
          "text": "[Vorname] Für den Antragsteller ohne Namen ist der Vorname zu erfassen."
        },
        {
          "kategorie": "VOLLSTAENDIGKEIT",
          "text": "[Nachname] Für den Antragsteller ohne Namen ist der Nachname zu erfassen."
        },
        {
          "kategorie": "ANPASSUNG",
          "text": "Die Laufzeit wurde angepasst."
        }
      ],
      "unterlagen": [
        {
          "text": "Unterzeichneter Baufinanzierungsvertrag"
        },
        {
          "text": "Unterzeichneter Darlehensantrag"
        }
      ],
      "bonitaetscheck": {
        "name": "Haushaltsrechnung",
        "ueberschrift": "Beispielbank",
        "ueberschuss": 1500.0,
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
                "wert": 180.0
              }
            ],
            "titel": "Ausgaben",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Ausgaben",
                  "wert": 1400.0
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
                  "wert": 1600.0
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
              "gesamtrate": 180.0,
              "vorausdarlehenSollzinsen": -60.0,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 110.0,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": -400.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -290.0
            },
            {
              "jahr": 2019,
              "monat": 11,
              "gesamtrate": 180.0,
              "vorausdarlehenSollzinsen": -60.0,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 110.0,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -170.0
            },
            {
              "jahr": 2027,
              "monat": null,
              "gesamtrate": 1000.0,
              "vorausdarlehenSollzinsen": -450.0,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": 650.0,
              "bausparvertragGuthabenzinsen": 10.0,
              "bausparvertragGebuehren": -15.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16000.0,
            "vorausdarlehenSollzinsen": -6000.0,
            "vorausdarlehenSaldo": -25000.0,
            "bausparvertragEinzahlungen": 10000.0,
            "bausparvertragGuthabenzinsen": 70.0,
            "bausparvertragGebuehren": -500.0,
            "bausparvertragTilgung": null,
            "bausparvertragSollzinsen": null,
            "bausparvertragSaldo": 10000.0
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
              "bausparvertragSaldo": -15000.0
            },
            {
              "jahr": 2027,
              "monat": 8,
              "gesamtrate": 180.0,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 150.0,
              "bausparvertragSollzinsen": -30.0,
              "bausparvertragSaldo": -15000.0
            },
            {
              "jahr": 2035,
              "monat": null,
              "gesamtrate": 550.0,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 540.0,
              "bausparvertragSollzinsen": -5.0,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 16000.0,
            "vorausdarlehenSollzinsen": null,
            "vorausdarlehenSaldo": null,
            "bausparvertragEinzahlungen": null,
            "bausparvertragGuthabenzinsen": null,
            "bausparvertragGebuehren": null,
            "bausparvertragTilgung": 15000.0,
            "bausparvertragSollzinsen": -1400.0,
            "bausparvertragSaldo": 0.0
          }
        }
      },
      "maximalerAuszahlungsbetrag": null
    }
  ]
}
```