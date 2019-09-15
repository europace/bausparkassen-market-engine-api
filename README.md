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

<details><summary>Request</summary>
<p>

```json
{"foo":  "bar"}
```

</p>
</details>

Response

### Angebot mit Tilgungsplan

Request

Response

### Angebot mit Haushaltsrechnung

Request

Response

Dies ist ein einfaches Beispiel, wie eine Haushaltsrechnung in der API aussehen kann.

```
  "bonitaetscheck": {
    "name": "Haushaltsrechnung",
    "ueberschrift": "Beispielbank",
    "ueberschuss": 2342.19,
    "bloecke": [
      {
        "titel": "Einnahmen",
        "zeilen": [
          {
            "label": "Unselbst\u00e4ndiges Nettoeinkommen",
            "wert": 4000.00
          },
          {
            "label": "Eink\u00fcnfte aus Nebent\u00e4tigkeit",
            "wert": 200.00
          }
        ],
        "innerBlock": {
          "zeilen": [
            {
              "label": "Summe Einnahmen",
              "wert": 4200.00,
              "hervorgehoben": true
            }
          ],
          "hervorgehoben": true
        }
      },
      {
        "titel": "Ausgaben",
        "zeilen": [
          {
            "label": "Lebenshaltungskosten",
            "wert": 857.81
          },
          {
            "label": "Mietausgaben",
            "wert": 1000.00
          }
        ],
        "innerBlock": {
          "zeilen": [
            {
              "label": "Summe Ausgaben",
              "wert": 1857.81,
              "hervorgehoben": true
            }
          ],
          "hervorgehoben": true
        }
      },
      {
        "titel": "\u00dcberschuss / Fehlbetrag",
        "innerBlock": {
          "zeilen": [
            {
              "label": "\u00dcberschuss",
              "wert": 2342.19,
              "hervorgehoben": true
            }
          ],
          "hervorgehoben": true
        }
      }
    ]
  }
  ```

## Beispiel `tilgungsplanBausparvertragMitVorausdarlehen`

Dies ist ein einfaches Beispiel (gekürzte Version mit fiktiven Zahlen), wie ein Tilgungsplan von Vorausdarlehen und Bausparvertrag in der API aussehen kann.

```
  "tilgungsplanBausparvertragMitVorausdarlehen": {
    "sparphase": {
      "eintraege": [
        {
          "monat": 9,
          "jahr": 2019,
          "vorausdarlehenSaldo": -30000
        },
        {
          "monat": 10,
          "jahr": 2019,
          "gesamtrate": 119.02,
          "vorausdarlehenSollzinsen": -49.87,
          "vorausdarlehenSaldo": -2930.85,
          "bausparvertragEinzahlungen": 69.15,
          "bausparvertragGuthabenzinsen": 0.12,
          "bausparvertragGebuehren": -487.5,
          "bausparvertragSaldo": -418.23
        },
        ...
        {
          "jahr": 2027,
          "gesamtrate": 1666.35,
          "vorausdarlehenSollzinsen": -237.65,
          "bausparvertragEinzahlungen": 968.10,
          "bausparvertragGuthabenzinsen": 18.23,
          "bausparvertragGebuehren": -15
        }
      ],
      "werteBeiPhasenEnde": {
        "gesamtrate": 23090.85,
        "vorausdarlehenSollzinsen": 9675.75,
        "vorausdarlehenSaldo": -30000,
        "bausparvertragEinzahlungen": 13415.10,
        "bausparvertragGuthabenzinsen": 126.67,
        "bausparvertragGebuehren": 607.50,
        "bausparvertragSaldo": 12934.27
      }
    },
    "darlehensphase": {
      "eintraege": [
        {
          "jahr": 2027,
          "gesamtrate": 1190.25,
          "bausparvertragTilgung": 1190.25,
          "bausparvertragSollzinsen": -171.05,
          "bausparvertragSaldo": -16046.53
        },
        ...
        {
          "jahr": 2034,
          "gesamtrate": 130.89,
          "bausparvertragTilgung": 130.89
        }
      ],
      "werteBeiPhasenEnde": {
        "gesamtrate": 18460.74,
        "bausparvertragTilgung": 17236.78,
        "bausparvertragSollzinsen": -1395.01,
        "bausparvertragSaldo": 0
      }
    }
  }
```
