# Bausparkassen Market Engine API

> ⚠️ You'll find German domain-specific terms in the documentation, for translations and further explanations please refer to our [glossary](https://docs.api.europace.de/common/glossary/)

This API enables building societies within consumer loans to connect their loan offering to the Europace platform via services with standardized interfaces.

> ⚠️ This API is continuously developed. Therefore we expect
> all users to align with the "[Tolerant Reader Pattern](https://martinfowler.com/bliki/TolerantReader.html)", which requires clients to be
> tolerant towards compatible API changes when reading and processing the data. This means:
>
> 1. unknown properties must not result in errors
>
> 2. Strings with a restricted set of values (Enums) must support new unknown values
>
> 3. sensible usage of HTTP status codes, even if they are not explicitly documented
>

<!-- https://opensource.zalando.com/restful-api-guidelines/#108 -->

## API Version

The version of the API is based on [Semantic Versioning](https://semver.org/) and has the format

`MAJOR.MINOR.PATCH`

and is part of the [Swagger Definition](https://github.com/europace/bausparkassen-market-engine-api/blob/master/swagger.yml) (`info.version`).

1. The `MAJOR` version is incremented in case of API incompatible changes (e.g. new mandatory data)
2. The `MINOR` version is incremented for backward compatible API changes (e.g. new optional specifications)
3. The `PATCH` version is incremented if the API remains the same, but the Swagger definition is adapted (e.g. extension or adaptation of descriptions in the API)

You will find the current version of the API within the [Releases](https://github.com/europace/bausparkassen-market-engine-api/releases).

## API specification

Requests and responses are defined in the [Swagger Definition](https://github.com/europace/bausparkassen-market-engine-api/blob/master/swagger.yml).


### Calculation

The calculation serves to generate offers.

In the process, the data provided for the Finanzierungswunsch as well as the applicant data are transmitted to the product provider.

The product provider: 
- Checks the feasibility of the Vorgang
- Checks the completness of the request 
- May adjusts the request
- Calculates the 2/3 - conditions 

### Acceptance

If all the necessary data is available and the preliminary check was successful, the case can be accepted. In this process, the customer's request, i.e. the provided data of the Finanzierungswunsch, as well as the applicant data are transmitted to the product provider.

The product provider should then, in turn, carry out all steps necessary for accepting the offer:

#### Adaptation of the customer's request

- If it is not possible to issue an offer on the desired financing criteria, an adjustment should be made to generate a feasible offer
- The following specifications can be adjusted
    - Duration specification
    - Monthly payment specification
    - Loan amount specification
    - Insurance combinations
    - Commission
- An adjustment message must be generated for each adjustment to inform the broker of the adjustment.
- See fields <code>status.angepasst</code> and <code>meldungen</code>

#### Credit assessment of the applicant

- Including an overview of the accounted income and expenses and the calculated surplus/shortfall
- See field <code>bonitaetscheck</code>

#### Calculation of final conditions

- Including repayment plan
- See fields <code>kredit</code>, <code>bausparvertrag</code> and <code>tilgungsplanBausparvertragMitVorausdarlehen</code>

#### Vote on the feasibility of the application

- Including consideration of the scores of external providers e.g. Schufa
- In case of rejection, generating a message with the reason for rejection
- See fields <code>status</code> and <code>meldungen</code>

#### Identification of documents to be submitted
- See field <code>unterlagen</code>

#### Creation of the contract documents
- See field <code>dokumente</code>

### API reference

The implemented interface accepts data with content-type **application/json**.  

#### Request

Services that implement the API expect a POST request with a JSON document as request body.

During the offer calculation, it is already ensured that the application data is complete. Nevertheless, the service must be able to deal with missing data. This should not lead to a technical error.

#### Response

The response will be expected as JSON within the response body. 

In general a response with a complete offer and HTTP status code **200 SUCCESS** is expected. If the offer is `MACHBAR`, at least one document is expected.

In case of a technical error a response with HTTP status code **500** is expected. The response must not contain an offer, but should give an indication of the cause of the error as <code>supportMeldung</code>.

##### Handling incomplete requests

A complete offer without document(s) is expected. The feasibilty status is `NICHT_MACHBAR`. Completeness messages, that point out the missing data, must be available.

##### Handling shortfall in the Haushaltsrechnung

If the application is not feasible due to a shortfall in the Haushaltsrechnung, ideally the duration will be extended. If this is not possible, a downselling of the loan amount can take place.

If a downselling results in a feasible offer, this is marked as <code>"angepasst": true</code> and contains appropriate adjustment messages to inform the broker of the adjustment.

If a downselling is not possible, an offer without document(s) with the status `NICHT_MACHBAR` and at least one corresponding feasibility message is expected. Duration and loan amount should in this case correspond to the original request.

##### Messages

Messages are generated to provide guidance to the broker on the excecution and feasibility of the application. The following categories are distinguished.

| Message category  | Description | <code>machbarkeitsstatus</code>| <code>angepasst</code> |
|--------|--------|--------|--------|
| <code>MACHBARKEIT</code> | The application will be rejected. | `NICHT_MACHBAR`| <i>no influence<i> |
| <code>VOLLSTAENDIGKEIT</code> | The application is incomplete and must be completed with missing data. | `NICHT_MACHBAR`| <i>no influence<i> | 
| <code>HINWEIS</code> | Note to the broker. | <i>no influence<i> | <i>no influence<i>|
| <code>ANPASSUNG</code> | Information about adjustments of the customer's request, e.g. monthly payment, loan amount oder insurance. | `MACHBAR` | `true` | 

##### Status

| Machbarkeitsstatus  | Description |
|--------|--------|
| `MACHBAR` | The application is accepted. |
| `MACHBAR_UNTER_VORBEHALT_PRODUKTANBIETER` | The application could not be examined conclusively. Product provider and broker need to renegotiate.| 
| `NICHT_MACHBAR` | The application is rejected. |

## Authentication

The method of authentication has to be coordinated between the Produktanbieter and Europace.
    
## Performance

The calculation response must be within 4 seconds, slower responses will be discarded. The acceptance response should be within 20 seconds, but responses here may still be processed if certain overruns occur. If the response time is significantly higher, the functionality of our platform deteriorates for other partners, e.g. brokers.

## Examples

* [Request with minimal data](https://github.com/europace/bausparkassen-market-engine-api/blob/master/beispiele/anfrage-mit-minimalen-angaben.md)
* [Request with complete data (one applicant)](https://github.com/europace/bausparkassen-market-engine-api/blob/master/beispiele/anfrage-mit-vollstaendigen-angaben-ein-antragsteller.md)
* [Request with complete data (two applicants with joint household)](https://github.com/europace/bausparkassen-market-engine-api/blob/master/beispiele/anfrage-mit-vollstaendigen-angaben-mehrere-antragsteller-im-gemeinsamen-haushalt.md)
* [Request with complete data (two applicants with separate household)](https://github.com/europace/bausparkassen-market-engine-api/blob/master/beispiele/anfrage-mit-vollstaendigen-angaben-mehrere-antragsteller-in-getrennten-haushalten.md)
* [Accepting with complete data (one applicant)](https://github.com/europace/bausparkassen-market-engine-api/blob/master/beispiele/annahme-mit-vollstaendigen-angaben-ein-antragsteller.md)

## Terms of use

The APIs are made available under the following [Terms of Use](https://docs.api.europace.de/terms/)
