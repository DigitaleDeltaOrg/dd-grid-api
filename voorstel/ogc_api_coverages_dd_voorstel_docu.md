# Voorstel DD-GRID-API

## Inleiding

Deze pagina bevat de beschrijving van een voorstel voor Digitale Delta Roosterdata API. Deze DD API voor grid data is gebaseerd op de [OGC API Coverages]. Over een goede naam van de API moet worden nagedacht; voorlopig wordt hij DD-GRID-API genoemd.
De DD-GRID-API-specificatie ([./ogc_api_coverages_dd_voorstel_oas3.json](./ogc_api_coverages_dd_voorstel_oas3.json)) is opgesteld conform OAS3, m.a.w. de specificatie valideert tegen het [OAS3-schema](https://github.com/OAI/OpenAPI-Specification/blob/master/schemas/v3.0/schema.json), dat voor de volledigheid ook hier bij de DD-GRID-API-specificatie is opgenomen (./oas3-schema.json).
De resource objects van de DD-GRID-API-specificatie zijn nog niet uitgewerkt in deze OAS3 specificatie. Hier wordt aan gewerkt. Zie voorlopig [../voorbeelden/voorbeelden.md](../voorbeelden/voorbeelden.md) voor enkele uitwerkingen van de response.

In eerste instantie was door de DD-werkgroep een eigen roosterdata-API uitgewerkt. De documentatie van deze eerste opzet is te vinden in [./oud/dd-grid-api-voorstel.md](./oud/dd-grid-api-voorstel.md).  
Deze bleek qua naamgeving enorm af te wijken van de OGC-terminologie, maar bleek qua structuur zeer vergelijkbaar. Daarom is besloten om te onderzoeken of we met de OGC API Coverages uit de voeten zouden kunnen.  
Voor de _resource objects_ in de response is dat zonder meer het geval, al hebben we wel het een en ander vereenvoudigd; zie bovengenoemde voorbeelden.  
Ook qua _end points_ blijkt er veel overeenstemming te zijn, maar ook daarbij hebben we vereenvoudigingen toegepast.

## Vertrekpunten

Onderstaande documentatie heeft als basis gediend voor wat er nu ligt:
* _OGC API Coverage_ specifatie voor de resource objects: https://github.com/opengeospatial/ogc_api_coverages/blob/master/standard/openapi/coverage-schema.json
* _OGC API Coverage_ specifatie voor de urls van de end points: https://github.com/opengeospatial/ogc_api_coverages/blob/master/standard/openapi/openapi.json

Omdat deze OGC specificatie nog in ontwikkeling is hebben we besloten om hem niet volledig te hanteren, maar om daar waar nuttig wijzingingen aan te brengen. Daarmee lopen we het risico dat we t.z.t. gaan afwijken van de definitieve OGC-specificatie, maar we schatten in dat de afwijkende specificatie-onderdelen relatief eenvoudig zijn om te zetten naar de dan geldende standard, of dat de afwijking goed te beargumenteren zijn en wel binnen het algemene stramien passsen.
De wijzigingen die we hebben aangebracht laten zich samenvatten als:
* Als een tussenniveau in de object-structuur altijd hetzelfde is en evident is, is dit tussenniveau verwijderd (geldt zowel voor de _response_ als voor de _end point_ paden).
* Object-type benamingen zijn weggelaten, tenzij de aanduiding van het object-type daadwerkelijk van belang is, omdat er meerdere varianten van het object zijn.
* In een aantal gevallen, met name bij de assen van de _envelope_ en de _domainset_ is in plaats van een lijst een dictionary gebruikt.

## Conceptversie DD-OGC-GRID-API end points

| **End point** | **parameters** | **omschrijving** |
| --- | --- | --- |
| **/dataformats** | | Ondersteunde data formats. Minimaal "netcdf-cf" |
| **/outputCrss** | | Welke projecties ondersteunt het systeem?<br>Response: lijst van projecties waar bij het opvragen van data naar toe kan worden getransformeerd |
| **/quantities** | | Welke quantities kent de provider?<br>Response: lijst met quantity objecten |
| | _pageSize_ | Gewenst aantal #items in de response. Zie ['pageable' mechanisme in de DD-API](https://github.com/DigitaleDeltaOrg/dd-api/blob/master/libraries/dd-traits.raml) |
| | _page_ | Gewenste subpagina. Zie ['pageable' mechanisme in de de DD-API](https://github.com/DigitaleDeltaOrg/dd-api/blob/master/libraries/dd-traits.raml) |
| | _boundingBox_ | Gebied van interesse |
| | _time_ | Periode van interesse |
| **/coverages** | | Welke coverages kent de provider?<br>Response: lijst met metadata-objecten van de coverages (kan mengeling van rasters en curvilineair zijn) |
| | _pageSize_ | Gewenst aantal #items in de response. Zie ['pageable' mechanisme in de DD-API](https://github.com/DigitaleDeltaOrg/dd-api/blob/master/libraries/dd-traits.raml) |
| | _page_ | Gewenste subpagina. Zie ['pageable' mechanisme in de de DD-API](https://github.com/DigitaleDeltaOrg/dd-api/blob/master/libraries/dd-traits.raml) |
| | _boundingBox_ | Gebied van interesse |
| | _time_ | Periode van interesse |
| | _quantity_ | Geef alleen coverage die data voor _quantity_ bevatten |
| **/coverages/{coverageId}** | | Alle informatie over een coverage, behalve de data |
| **/coverages/{coverageId}/data** | | Vraag data op van de coverage|
| | _boundingBox_ | Rechthoekig deelgebied uit de domainset |
| | _areaOfInterest_ | WKT-string die het gewenste (willekeurige) deelgebied beschrijft |
| | _outputCrs_ | Gewenste projectie. (Tevens projectie van de areaOfInterest.) |
| | _rangeSubset_ | Selectie van de gewenste quantities|
| | _startTime_ | Data vanaf (inclusief) |
| | _endTime_ | Data tot en met (inclusief) |
| | _analysisTime_ | Productietijd van de data set |
| | _realization_ | Realization index, in geval van resultaten van een ensemble run |
| | _point[]_ | X,Y-punt(en) Response is dan een json file met een lijst van tijdseries conform de response van de DD-API. (De lijst is 1 lang als er om 1 punt is gevraagd |
