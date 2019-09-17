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

## Beispiele

* [Anfrage mit minimalen Angaben](beispiele.md#anfrage-mit-minimales-angaben)
* [Anfrage mit vollständigen Angaben (ein Antragsteller)](beispiele.md#anfrage-mit-vollständigen-angaben-ein-antragsteller)
* [Anfrage mit vollständigen Angaben (mehrere Antragsteller im gemeinsamen Haushalt)](beispiele.md#anfrage-mit-vollständigen-angaben-mehrere-antragsteller-im-gemeinsamen-haushalt)
* [Anfrage mit vollständigen Angaben (mehrere Antragsteller in getrennten Haushalten)](beispiele.md#anfrage-mit-vollständigen-angebot-mehrere-antragsteller-in-getrennten-haushalten)
* [Annahme mit vollständigen Angaben (ein Antragsteller)](beispiele.md#annahme-mit-vollständigen-angaben-ein-antragsteller)