# bausparkassen-me-api
Market Engine-API für Bausparkassen

## Beispiel `bonitaetscheck`

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

Dies ist ein einfaches Beispiel (gekürzte Version), wie ein Tilgungsplan von Vorausdarlehen und Bausparvertrag in der API aussehen kann.

```
  "tilgungsplanBausparvertragMitVorausdarlehen": {
    "sparphase": {
      "eintraege": [
        {
          "monat": 9,
          "jahr": 2019,
          "gesamtrate": 100,
          "vorausdarlehenSollzinsen": 100,
          "vorausdarlehenSaldo": -30000
        },
        {
          "monat": 10,
          "jahr": 2019,
          "gesamtrate": 1428.30,
          "vorausdarlehenSollzinsen": -598.50,
          "vorausdarlehenSaldo": -29170.20,
          "bausparvertragEinzahlungen": 829.80,
          "bausparvertragGuthabenzinsen": 0.12,
          "bausparvertragGebuehren": -487.5,
          "bausparvertragSaldo": 342.42
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
      "summe": {
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
      "summe": {
        "gesamtrate": 18460.74,
        "bausparvertragTilgung": 17236.78,
        "bausparvertragSollzinsen": -1395.01,
        "bausparvertragSaldo": 0
      }
    }
  }
```
