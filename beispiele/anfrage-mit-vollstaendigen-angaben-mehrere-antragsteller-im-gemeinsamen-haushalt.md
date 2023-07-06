## Anfrage mit vollständigen Angaben (mehrere Antragsteller im gemeinsamen Haushalt)

Die aufgelisteten Beispielanfragen und -antworten dienen zum besseren Verständnis der API. 

Die Beispielantworten sind fiktiv und gekürzt, sodass die Konditionen bspw. nicht mit dem Tilgungsplan übereinstimmen.   

Anmerkung zum Tilgungsplan:
- i.d.R. wird das erste Jahr monatsweise aufgelistet
- i.d.R. werden alle weiteren Jahre jeweils zu einem einzelnen Eintrag pro Jahr aggregiert
- die Beispielantworten enthalten lediglich die ersten beiden und den letzten Eintrag - die Dazwischenliegenden wurden entfernt  

### Request

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
          "immobiliendarlehen": []
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
          "immobiliendarlehen": []
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
        "immobiliendarlehen": []
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
      "dispositionskredite": []
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
        "gesamtbetrag": 30000.0,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 187,
        "rateProMonat": 150.0,
        "vertragsbeginn": "2019-10-01"
      },
      "kredit": {
        "effektivzinssatz": 0.0132,
        "sollzinssatz": 0.0123,
        "gesamtbetrag": 30000.0,
        "nettokreditbetrag": 25000.0,
        "auszahlungsbetrag": 25000.0,
        "laufzeitInMonaten": 94,
        "rateProMonat": 60.0,
        "letzteRate": 60.0,
        "provisionsbetrag": 300.0,
        "basisbetragFuerDieProvisionsermittlung": 25000.0,
        "vorlaufzinsenProTag": 0.0,
        "versicherung": null
      },
      "bausparvertrag": {
        "tarifname": "Beispieltarif",
        "bausparsumme": 25000.0,
        "gesamtlaufzeitInMonaten": 187,
        "zuteilungsZeitpunkt": "2027-07-31",
        "provision": 400.0,
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
          "rateMonatlich": 170.0,
          "dauerInMonaten": 93,
          "sollzinsSatz": 0.0123,
          "effektivzinsSatz": 0.0132,
          "letzteRate": 10.0,
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
          "text": "Unterzeichneter Baufinanzierungsvertrag",
          "referenz": null
        },
        {
          "code": null,
          "text": "Unterzeichneter Darlehensantrag",
          "referenz": null
        }
      ],
      "bonitaetscheck": {
        "name": "Haushaltsrechnung",
        "ueberschrift": "Beispielbank",
        "ueberschuss": 3500.0,
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
                "wert": 150.0
              }
            ],
            "titel": "Ausgaben",
            "innerBlock": {
              "zeilen": [
                {
                  "hervorgehoben": true,
                  "label": "Summe Ausgaben",
                  "wert": 2500.0
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
                  "wert": 3000.0
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
              "gesamtrate": 150.0,
              "vorausdarlehenSollzinsen": -50.0,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 100.0,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": -400.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -300.0
            },
            {
              "jahr": 2019,
              "monat": 11,
              "gesamtrate": 150.0,
              "vorausdarlehenSollzinsen": -50.0,
              "vorausdarlehenSaldo": -25000.0,
              "bausparvertragEinzahlungen": 100.0,
              "bausparvertragGuthabenzinsen": 0.0,
              "bausparvertragGebuehren": 0.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": -150.0
            },
            {
              "jahr": 2027,
              "monat": null,
              "gesamtrate": 1000.0,
              "vorausdarlehenSollzinsen": -450.0,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": 700.0,
              "bausparvertragGuthabenzinsen": 10.0,
              "bausparvertragGebuehren": -10.0,
              "bausparvertragTilgung": null,
              "bausparvertragSollzinsen": null,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 15000.0,
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
              "gesamtrate": 150.0,
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
              "gesamtrate": 50.0,
              "vorausdarlehenSollzinsen": null,
              "vorausdarlehenSaldo": null,
              "bausparvertragEinzahlungen": null,
              "bausparvertragGuthabenzinsen": null,
              "bausparvertragGebuehren": null,
              "bausparvertragTilgung": 550.0,
              "bausparvertragSollzinsen": -2.0,
              "bausparvertragSaldo": null
            }
          ],
          "werteBeiPhasenEnde": {
            "gesamtrate": 15000.0,
            "vorausdarlehenSollzinsen": null,
            "vorausdarlehenSaldo": null,
            "bausparvertragEinzahlungen": null,
            "bausparvertragGuthabenzinsen": null,
            "bausparvertragGebuehren": null,
            "bausparvertragTilgung": 15000.0,
            "bausparvertragSollzinsen": -1500.0,
            "bausparvertragSaldo": 0.0
          }
        }
      },
      "maximalerAuszahlungsbetrag": null
    }
  ]
}
```
