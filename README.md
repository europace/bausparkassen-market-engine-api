# Bausparkassen Market Engine API
Die API ermöglicht es Bausparkassen im Ratenkreditgeschäft, ihr Kreditangebot über Services mit standardisierten Schnittstellen an die Europace Plattform anzubinden.

# Inhaltsverzeichnis

* [API Version](#api-version)
* [Dokumentation](#dokumentation)
  * [API Spezifikation](#api-spezifikation)
  * [API Referenz](#api-referenz)
    * [Ermittlung](#ermittlung)
      * [Request](#request)
      * [Response](#response)
    * [Annahme](#annahme)
      * [Request](#request-1)
      * [Response](#response-1)
    * [Meldungskategorie](#meldungskategorie)
    * [Machbarkeitsstatus](#machbarkeitsstatus)
* [Authentifizierung](#authentifizierung)
* [Performance](#performance)
* [Beispiele](#beispiele)
* [Nutzungsbedingungen](#nutzungsbedingungen)

## API Version

Die Version der API orientiert sich am [Semantic Versioning](https://semver.org/) und hat das Format

`MAJOR.MINOR.PATCH`

und ist in der [Swagger Definition](https://github.com/europace-privatkredit/bausparkassen-me-api/blob/master/swagger.yml) enthalten (`info.version`).

1. die `MAJOR` Version wird erhöht bei API inkompatiblen Änderungen (z.B. neue Pflichtangaben)
2. die `MINOR` Version wird erhöht bei abwärtskompatiblen API Änderungen (z.B. neue optionale Angaben)
3. die `PATCH` Version wird erhöht, wenn die API gleich bleibt, jedoch die Swagger Definition angepasst wird (z.B. Erweiterung oder Anpassung von Beschreibungen in der API)

Die aktuelle Version der API ist jeweils in den [Releases](https://github.com/europace-privatkredit/bausparkassen-me-api/releases) zu finden.

## Dokumentation

### API Spezifikation

Requests und Responses sind in der [Swagger Definition](https://github.com/europace-privatkredit/bausparkassen-me-api/blob/master/swagger.yml) dokumentiert.

### API Referenz

Die implementierte Schnittstelle akzeptiert Daten mit Content-Type **application/json**.  

#### Ermittlung

##### Request

Services, die die API implementieren, erwarten einen POST-Request mit einem JSON-Dokument als Request-Body.

##### Response

Antworten werden als JSON im Body der Response erwartet.

Grundsätzlich wird eine Antwort mit HTTP-Statuscode **200 SUCCESS** erwartet. Werden keine Angebote gefunden, wird eine leere Liste zurückgegeben. Im Falle eines technischen Fehlers wird eine Antwort mit HTTP-Statuscode 500 erwartet. 
Die Antwort muss als supportMeldung einen Hinweis auf die Fehlerursache enthalten. 

Bei unvollständigen Anfragen werden Angebote mit Machbarkeitsstatus **NICHT_MACHBAR** erwartet. Es sind Vollständigkeitsmeldungen vorhanden, die auf die fehlenden Angaben hinweisen.

Wird die Anfrage bspw. in der Laufzeit angepasst, müssen die Angebote mit angepasst = true markiert werden und entsprechende Anpassungsmeldungen enthalten, um den Vermittler über die Anpassung zu informieren.

#### Annahme

##### Request

Services, die die API implementieren, erwarten einen POST-Request mit einem JSON-Dokument als Request-Body.

Während der Angebotsermittlung wird bereits sichergestellt, dass die Antragsdaten vollständig sind. Dessen ungeachtet muss der Service mit fehlenden Daten umgehen können. Sie dürfen nicht zu einem technischen Fehler führen. 

##### Response

Antworten werden als JSON im Body der Response erwartet.

Grundsätzlich wird eine Antwort mit einem vollständigen Angebot und HTTP-Statuscode **200 SUCCESS** erwartet. Wenn das Angebot **MACHBAR** ist, wird mindestens ein Dokument erwartet.
Im Falle eines technischen Fehlers wird eine Antwort mit HTTP-Statuscode 500 erwartet. Die Antwort muss kein Angebot enthalten, aber einen Hinweis auf die Fehlerursache als supportMeldung.

Es wird ein vollständiges Angebot ohne Dokument(e) erwartet. Der Machbarkeitsstatus ist **NICHT_MACHBAR**. Es sind Vollständigkeitsmeldungen vorhanden, die auf die fehlenden Angaben hinweisen.

Ist der Antrag aufgrund einer Haushaltsunterdeckung nicht machbar, erfolgt im Idealfall eine Verlängerung der Laufzeit. Ist dies nicht möglich, kann ein Downselling des Auszahlungsbetrags erfolgen.

Führt das Downselling zu einem machbaren Angebot, wird dieses als angepasst = true markiert und enthält entsprechende Anpassungsmeldungen, um den Vermittler über die Anpassung zu informieren. 

Ist ein Downselling nicht möglich, wird ein Angebot ohne Dokument(e) mit dem Status **NICHT_MACHBAR** und mindestens einer entsprechenden Machbarkeitsmeldung erwartet. Laufzeit und Kreditbetrag sollten in diesem Fall der ursprünglichen Anfrage entsprechen.

#### Meldungskategorie

| Meldungskategorie  | Beschreibung |
|--------|--------|
| MACHBARKEIT | Der Antrag wird abgelehnt. | 
| VOLLSTAENDIGKEIT | Der Antrag ist unvollständig und muss zur abschließenden Prüfung um fehlende Angaben ergänzt werden. | 
| HINWEIS | Hinweis an den Vermittler. | 
| ANPASSUNG | Information über eine Anpassung des Kundenwunsches, z.B. Rate, Auszahlungsbetrag oder Versicherungswunsch. | 

#### Machbarkeitsstatus

| Machbarkeitsstatus  | Beschreibung |
|--------|--------|
| MACHBAR | Dem Antrag kann entsprochen werden. | 
| MACHBAR_UNTER_VORBEHALT_PRODUKTANBIETER | Der Antrag konnte nicht abschließend geprüft werden. Produktanbieter und Vermittler müssen den Antrag nachverhandeln.| 
| NICHT_MACHBAR | Der Antrag wurde abgelehnt. | 

## Authentifizierung

Die Art und Weise der Authentifizierung wird zwischen dem Produktanbieter und Europace abgestimmt. 

## Performance

Wir erwarten die Ermittlungsantwort innerhalb von 4 Sekunden, die Annahme-Antwort innerhalb von 20 Sekunden. 
Bei einem deutlich höherem Wert, verschlechtert sich die Funktionalität unserer Plattform für andere Partner, z.B. Vertriebe.

## Beispiele

* [Anfrage mit minimalen Angaben](beispiele/anfrage-mit-minimalen-angaben.md)
* [Anfrage mit vollständigen Angaben (ein Antragsteller)](beispiele/anfrage-mit-vollstaendigen-angaben-ein-antragsteller.md)
* [Anfrage mit vollständigen Angaben (mehrere Antragsteller im gemeinsamen Haushalt)](beispiele/anfrage-mit-vollstaendigen-angaben-mehrere-antragsteller-im-gemeinsamen-haushalt.md)
* [Anfrage mit vollständigen Angaben (mehrere Antragsteller in getrennten Haushalten)](beispiele/anfrage-mit-vollstaendigen-angaben-mehrere-antragsteller-in-getrennten-haushalten.md)
* [Annahme mit vollständigen Angaben (ein Antragsteller)](beispiele/annahme-mit-vollstaendigen-angaben-ein-antragsteller.md)

## Nutzungsbedingungen
Die APIs werden unter folgenden [Nutzungsbedingungen](https://developer.europace.de/terms/) zur Verfügung gestellt