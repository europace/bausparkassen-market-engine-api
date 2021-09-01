# Bausparkassen Market Engine API
Die API ermöglicht es Bausparkassen im Ratenkreditgeschäft, ihr Kreditangebot über Services mit standardisierten Schnittstellen an die Europace Plattform anzubinden.

## API Version

Die Version der API orientiert sich am [Semantic Versioning](https://semver.org/) und hat das Format

`MAJOR.MINOR.PATCH`

und ist in der [Swagger Definition](https://github.com/europace/bausparkassen-market-engine-api/blob/master/swagger.yml) enthalten (`info.version`).

1. die `MAJOR` Version wird erhöht bei API inkompatiblen Änderungen (z.B. neue Pflichtangaben)
2. die `MINOR` Version wird erhöht bei abwärtskompatiblen API Änderungen (z.B. neue optionale Angaben)
3. die `PATCH` Version wird erhöht, wenn die API gleich bleibt, jedoch die Swagger Definition angepasst wird (z.B. Erweiterung oder Anpassung von Beschreibungen in der API)

Die aktuelle Version der API ist jeweils in den [Releases](https://github.com/europace/bausparkassen-market-engine-api/releases) zu finden.

## API Spezifikation

Requests und Responses sind in der [Swagger Definition](https://github.com/europace/bausparkassen-market-engine-api/blob/master/swagger.yml) dokumentiert.

## Dokumentation

### API Referenz

Die implementierte Schnittstelle akzeptiert Daten mit Content-Type **application/json**.  

### Ermittlung
Die Ermittlung dient der Erzeugung von 1..n Angeboten. 

Dabei werden die im Vorgang erfassten Daten zum Finanzierungswunsch sowie die Antragstellerdaten an den Produktanbieter übermittelt.

Der Produktanbieter 
- prüft die Vollständigkeit des Vorgangs
- prüft die Machbarkeit des Wunsches 
- nimmt gegebenenfalls Anpassungen am Wunsch vor
- ermittelt die (2/3-) Konditionen. 

##### Anpassung des Kundenwunsches

- Ist die Herausgabe eines Angebots zu den gewünschten Finanzierungskriterien nicht möglich, sollte eine Anpassung erfolgen, um ein machbares Angebot zu erzeugen
- Folgende Vorgaben können angepasst werden
    - Laufzeitvorgabe
    - Ratenvorgabe
    - Kreditbeträge
    - Versicherungskombinationen
    - Provisionen
- Zu jeder Anpassung muss eine Anpassungsmeldung generiert werden, um den Vermittler über die Anpassung zu informieren.
- siehe Felder <code>status.angepasst</code> und <code>meldungen</code>

#### Request

Services, die die API implementieren, erwarten einen POST-Request mit einem JSON-Dokument als Request-Body.

#### Response

Antworten werden als JSON im Body der Response erwartet.

Grundsätzlich wird eine Antwort mit HTTP-Statuscode **200 SUCCESS** erwartet. Werden keine Angebote gefunden, wird eine leere Liste zurückgegeben. Im Falle eines technischen Fehlers wird eine Antwort mit HTTP-Statuscode 500 erwartet. 
Die Antwort sollte als <code>supportMeldung</code> einen Hinweis auf die Fehlerursache enthalten. 

Bei unvollständigen Anfragen werden Angebote mit Machbarkeitsstatus **NICHT_MACHBAR** erwartet. Es sind Vollständigkeitsmeldungen vorhanden, die auf die fehlenden Angaben hinweisen.

### Annahme
Wenn alle notwendigen Daten vorhanden sind und die Vorprüfung im Rahmen der Ermittlung erfolgreich war, kann die Annahme des Vorgangs erfolgen. Dabei werden die vom Vermittler <b>erfassten (nicht
angepassten)</b> Daten zum Finanzierungswunsch sowie die Antragstellerdaten an den Produktanbieter übermittelt.

Der Produktanbieter führt dann seinerseits alle für die Annahme des Angebots notwendigen Schritte durch:

#### Vollständigkeitsprüfung
- Während der Angebotsermittlung wird bereits sichergestellt, dass die Antragsdaten vollständig sind. Dessen ungeachtet muss der Service mit fehlenden Daten umgehen können. Sie dürfen nicht zu einem technischen Fehler führen.

#### Anpassung des Kundenwunsches
- Ist die Herausgabe eines Angebots zu den gewünschten Finanzierungskriterien nicht möglich, sollte eine Anpassung analog der Ermittlung erfolgen.

#### Bonitätsprüfung der Antragsteller

- inklusive Übersicht der angerechneten Einnahmen sowie Ausgaben und des ermittelten Überschusses/Unterdeckung
- siehe Feld <code>bonitaetscheck</code>

#### Ermittlung der finalen Konditionen

- inklusive Tilgungsplan
- siehe Felder <code>kredit</code>, <code>bausparvertrag</code> und <code>tilgungsplanBausparvertragMitVorausdarlehen</code>

#### Votum über die Machbarkeit des Antrags

- inklusive Berücksichtigung der Scorings externer Anbieter z.B. Schufa
- Im Falle der Ablehnung, generierung einer Meldung mit Ablehnungsgrund
- siehe Felder <code>status</code> und <code>meldungen</code>

#### Ermittlung einzureichender Unterlagen
- siehe Feld <code>unterlagen</code>

#### Erstellung der Vertragsdokumente
- siehe Feld <code>dokumente</code>

#### Request

Services, die die API implementieren, erwarten einen POST-Request mit einem JSON-Dokument als Request-Body.

#### Response

Antworten werden als JSON im Body der Response erwartet.

Grundsätzlich wird eine Antwort mit einem vollständigen Angebot und HTTP-Statuscode **200 SUCCESS** erwartet. Wenn das Angebot **MACHBAR** ist, wird mindestens ein Dokument erwartet.
Im Falle eines technischen Fehlers wird eine Antwort mit HTTP-Statuscode 500 erwartet. Die Antwort muss kein Angebot enthalten, aber einen Hinweis auf die Fehlerursache als supportMeldung.

Es wird ein vollständiges Angebot ohne Dokument(e) erwartet. Der Machbarkeitsstatus ist **NICHT_MACHBAR**. Es sind Vollständigkeitsmeldungen vorhanden, die auf die fehlenden Angaben hinweisen.

Ist der Antrag aufgrund einer Haushaltsunterdeckung nicht machbar, erfolgt im Idealfall eine Verlängerung der Laufzeit. Ist dies nicht möglich, kann ein Downselling des Auszahlungsbetrags erfolgen.

Führt das Downselling zu einem machbaren Angebot, wird dieses als angepasst = true markiert und enthält entsprechende Anpassungsmeldungen, um den Vermittler über die Anpassung zu informieren. 

Ist ein Downselling nicht möglich, wird ein Angebot ohne Dokument(e) mit dem Status **NICHT_MACHBAR** und mindestens einer entsprechenden Machbarkeitsmeldung erwartet. Laufzeit und Kreditbetrag sollten in diesem Fall der ursprünglichen Anfrage entsprechen.

#### Meldungen

Meldungen werden erzeugt, um den Vermittler Hinweise zur Durchführung und Machbarkeit des Antrags zu geben. Es werden folgende Kategorien unterschieden.

##### <code>meldungskategorie</code>

| Meldungskategorie  | Beschreibung | <code>machbarkeitsstatus</code>| <code>angepasst</code> |
|--------|--------|--------|--------|
| <code>MACHBARKEIT</code> | Der Antrag wird abgelehnt. | NICHT_MACHBAR| <i>kein Einfluß<i> |
| <code>VOLLSTAENDIGKEIT</code> | Der Antrag ist unvollständig und muss zur abschließenden Prüfung um fehlende Angaben ergänzt werden. | NICHT_MACHBAR| <i>kein Einfluß<i> | 
| <code>HINWEIS</code> | Hinweis an den Vermittler. | <i>kein Einfluß<i> | <i>kein Einfluß<i>|
| <code>ANPASSUNG</code> | Information über eine Anpassung des Kundenwunsches, z.B. Rate, Auszahlungsbetrag oder Versicherungswunsch. | MACHBAR | true | 

#### Status

##### <code>machbarkeitsstatus</code>

| Machbarkeitsstatus  | Beschreibung |
|--------|--------|
| MACHBAR | Dem Antrag kann entsprochen werden. |
| MACHBAR_UNTER_VORBEHALT_PRODUKTANBIETER | Der Antrag konnte nicht abschließend geprüft werden. Produktanbieter und Vermittler müssen den Antrag nachverhandeln.| 
| NICHT_MACHBAR | Der Antrag wurde abgelehnt. |

## Authentifizierung

Die Art und Weise der Authentifizierung wird zwischen dem Produktanbieter und Europace abgestimmt. 

## Performance

Die Ermittlungsantwort muss innerhalb von 4 Sekunden erfolgen, langsamere Antworten werden verworfen. Die Annahme-Antwort sollte innerhalb von 20 Sekunden erfolgen,
jedoch können Antworten hier bei gewissen Überschreitungen noch verarbeitet werden.
Bei einem deutlich höherem Wert, verschlechtert sich die Funktionalität unserer Plattform für andere Partner, z.B. Vertriebe.

## Beispiele

* [Anfrage mit minimalen Angaben](https://github.com/europace/bausparkassen-market-engine-api/blob/master/beispiele/anfrage-mit-minimalen-angaben.md)
* [Anfrage mit vollständigen Angaben (ein Antragsteller)](https://github.com/europace/bausparkassen-market-engine-api/blob/master/beispiele/anfrage-mit-vollstaendigen-angaben-ein-antragsteller.md)
* [Anfrage mit vollständigen Angaben (mehrere Antragsteller im gemeinsamen Haushalt)](https://github.com/europace/bausparkassen-market-engine-api/blob/master/beispiele/anfrage-mit-vollstaendigen-angaben-mehrere-antragsteller-im-gemeinsamen-haushalt.md)
* [Anfrage mit vollständigen Angaben (mehrere Antragsteller in getrennten Haushalten)](https://github.com/europace/bausparkassen-market-engine-api/blob/master/beispiele/anfrage-mit-vollstaendigen-angaben-mehrere-antragsteller-in-getrennten-haushalten.md)
* [Annahme mit vollständigen Angaben (ein Antragsteller)](https://github.com/europace/bausparkassen-market-engine-api/blob/master/beispiele/annahme-mit-vollstaendigen-angaben-ein-antragsteller.md)

## Nutzungsbedingungen
Die APIs werden unter folgenden [Nutzungsbedingungen](https://docs.api.europace.de/nutzungsbedingungen/) zur Verfügung gestellt.
