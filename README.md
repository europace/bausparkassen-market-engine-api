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
            "zellen": [
              {
                "typ": "LABEL",
                "label": "Unselbst\u00e4ndiges Nettoeinkommen"
              },
              {
                "typ": "EURO",
                "euro": 4000.00
              }
            ]
          },
          {
            "zellen": [
              {
                "typ": "LABEL",
                "label": "Eink\u00fcnfte aus Nebent\u00e4tigkeit"
              },
              {
                "typ": "EURO",
                "euro": 200.00
              }
            ]
          }
        ],
        "innerBlock": {
          "zeilen": [
            {
              "zellen": [
                {
                  "typ": "LABEL",
                  "label": "Summe Einnahmen"
                },
                {
                  "typ": "EURO",
                  "euro": 4200.00
                }
              ],
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
            "zellen": [
              {
                "typ": "LABEL",
                "label": "Lebenshaltungskosten"
              },
              {
                "typ": "EURO",
                "euro": 857.81
              }
            ]
          },
          {
            "zellen": [
              {
                "typ": "LABEL",
                "label": "Mietausgaben"
              },
              {
                "typ": "EURO",
                "euro": 1000.00
              }
            ]
          }
        ],
        "innerBlock": {
          "zeilen": [
            {
              "zellen": [
                {
                  "typ": "LABEL",
                  "label": "Summe Ausgaben"
                },
                {
                  "typ": "EURO",
                  "euro": 1857.81
                }
              ],
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
              "zellen": [
                {
                  "typ": "LABEL",
                  "label": "\u00dcberschuss"
                },
                {
                  "typ": "EURO",
                  "euro": 2342.19
                }
              ],
              "hervorgehoben": true
            }
          ],
          "hervorgehoben": true
        }
      }
    ]
  }
```
