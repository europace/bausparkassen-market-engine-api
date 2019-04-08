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
