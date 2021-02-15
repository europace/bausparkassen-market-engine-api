## Annahme mit Downselling

Führt die Haushaltsrechnung zu einer Haushaltsunterdeckung, kann ein Downselling erfolgen. Dazu wird entweder die Laufzeit verlängert und oder der Kreditbetrag verringert, um die monatliche Belastung zu reduzieren. 
Wenn ein Downselling erfolgt, muss das Angebot in der Antwort den Block 
```
    "alternative": {
      "typ": "DOWNSELL"
    }
```
enthalten. Die Bezeichnung ist optional.

Die aufgelisteten Beispielanfragen und -antworten dienen zum besseren Verständnis der API. 

Die Beispielantworten sind fiktiv und gekürzt, sodass die Konditionen bspw. nicht mit dem Tilgungsplan übereinstimmen.   

### Request

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
      "auszahlungsbetrag": 35000.0,
      "ratenzahlungstermin": "ULTIMO",
      "laufzeitInMonaten": 72
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
    "traceId": "ks-d94c85a",
    "vorgangsnummer": "AB1234",
    "antragsnummer": "AB1234/1/1"
  },
  "featureToggles": [],
  "bearbeiter": {
    "vorname": "Daniel",
    "nachname": "Teske"
  },
  "handelsbeziehung": {
    "produktanbieter": "BEISPIEL_BANK",
    "kreditProvisionswunsch": 0.0123,
    "vertriebsgruppe": "Beispielgruppe"
  },
  "angebotsvariantentyp": "Beispielvariante",
  "beratungsart": "PRAESENZ_GESCHAEFT"
}
```

### Response

:warning: Die Beispielantworten sind fiktiv und gekürzt, sodass die Konditionen bspw. nicht mit dem Tilgungsplan übereinstimmen.

```json
{
  "angebot": {
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
      "laufzeitInMonaten": 180,
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
      "zuteilungsZeitpunkt": "2027-05-31",
      "provision": 450.0,
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
        "rateMonatlich": 150.0,
        "dauerInMonaten": 93,
        "sollzinsSatz": 0.0123,
        "effektivzinsSatz": 0.0132,
        "letzteRate": 10.0,
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
        "text": "Der Provisionswunsch wurde angepasst."
      },
      {
        "kategorie": "ANPASSUNG",
        "text": "Der Auszahlungsbetrag wurde angepasst."
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
              "wert": 150.0
            }
          ],
          "titel": "Ausgaben",
          "innerBlock": {
            "zeilen": [
              {
                "hervorgehoben": true,
                "label": "Summe Ausgaben",
                "wert": 1500.0
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
                "wert": 1500.0
              }
            ],
            "hervorgehoben": true
          }
        }
      ]
    },
    "maximalerAuszahlungsbetrag": null,
    "alternative": {
      "typ": "DOWNSELL"
    }
  },
  "dokumente": [
    {
      "bezeichnung": "Bausparantrag",
      "dateiname": "Bausparantrag.pdf",
      "base64pdf": "(pdf-als-base64)",
      "sichtbarkeit": {
        "sichtbarFuerVertrieb": true,
        "sichtbarFuerProduktanbieter": true
      }
    },
    {
      "bezeichnung": "Darlehensvertrag",
      "dateiname": "Darlehensvertrag.pdf",
      "base64pdf": "(pdf-als-base64)",
      "sichtbarkeit": {
        "sichtbarFuerVertrieb": true,
        "sichtbarFuerProduktanbieter": true
      }
    }
  ]
}
```
