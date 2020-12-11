# Beschrijving DD-GRID-API versie 0.95

## Inleiding

Deze pagina bevat de beschrijving versie 0.95 (binnenkort om te zetten in versie 1.0) van de Digitale Delta API voor roosterdata (grid data).  
Deze DD-GRID-API is afgeleid van de [OGC API Coverages](https://github.com/opengeospatial/ogc_api_coverages).
De specificatie van de DD-GRID-API is opgesteld in OAS3 (OpenAPI Specification 3), en staat in ([dd-grid-api-oas3.json](./dd-grid-api-oas3.json)). De DD-GRID-API specificatie valideert dus tegen het [OAS3-schema](https://github.com/OAI/OpenAPI-Specification/blob/master/schemas/v3.0/schema.json).

## Uitgangspunten

### OGC API Coverages
Bij het opstellen van de DD-GRID-API is zoals gezet uitgegaan van de _OGC API Coverages_. Daarbij is de volgende documentatie gebruikt:
* _OGC API Coverage_ specifatie voor de resource objects: https://github.com/opengeospatial/ogc_api_coverages/blob/master/standard/openapi/coverage-schema.json
* _OGC API Coverage_ specifatie voor de urls van de end points: https://github.com/opengeospatial/ogc_api_coverages/blob/master/standard/openapi/openapi.json

Bij de uitwerking constateerden we dat op sommige onderdelen de OGC-opzet slecht past bij wat we functioneel nodig hebben. En aangezien de OGC-specificatie nog in ontwikkeling is hebben we besloten om in die gevallen niet &#233;&#233;n op &#233;&#233;n de OGC-specificatie te hanteren, maar daarin wijzingingen aan te brengen.  
Daarmee lopen we het risico dat we t.z.t. gaan afwijken van de definitieve OGC-specificatie, maar we schatten in dat de afwijkende specificatie-onderdelen relatief eenvoudig zijn om te zetten naar de dan geldende standard, of dat de afwijkingen goed te beargumenteren zijn.

De wijzigingen die we hebben aangebracht laten zich als volgt samenvatten:
* Als een tussenniveau in de object-structuur altijd hetzelfde is en daarom evident is, is dit tussenniveau verwijderd (geldt zowel voor de _response_ als voor de _end point_ paden).
* Object-type benamingen die maar &#233;&#233;n mogelijke waarde voor die benaming hebben zijn weggelaten.
* In een aantal gevallen, met name bij de assen van de _envelope_ en de _domainset_ is in plaats van een lijst een dictionary gebruikt.
Deze aangebrachte wijzingingen zullen hier binnenkort in meer detail worden beschreven (in het Engels, zodat ze met de OGC gecommuniceerd kunnen worden).

### Functionele eisen en randvoorwaarden.

Als voorbereiding op het opstellen van de specificatie is de gewenste functionaliteit in kaart gebracht, hetgeen leidde tot een set van functionele eisen (wat moet de DD-GRID-API kunnen?) en aantal randvoorwaarden waaraan de resulterende DD-GRID-API-specificatie moet voldoen, b.v.:
- Het waar mogelijk volgen van de [URI/API-strategie van de DSO](https://aandeslagmetdeomgevingswet.nl/digitaal-stelsel/aansluiten/standaarden/api-en-uri-strategie/) en de daarvan afgeleide [API Design Rules (Nederlandse API Strategie IIa)](https://docs.geostandaarden.nl/api/API-Strategie/#api-designrules-nederlandse-api-strategie-iia).
- Het qua structuur en syntax zo weinig mogelijk afwijken van die bij de [DD-API](https://digitaledeltaorg.github.io/dd.v201.html).

Binnenkort verschijnt hier een uitgebreidere beschrijving van de randvoorwaarden en met name de daaruit voortgekomen keuzes.

## Overzicht van de DD-GRID-API end points

Onderstaande tabel bevat een compacte beschrijving van de end points en de bijbehorende filter parameters.  
Zie [dd-grid-api-oas3.json](./dd-grid-api-oas3.json) voor de volledige specificatie in OAS3.  
Zie _(volgt zeer binnenkort)_ voor de uit de OAS3-specificatie gegenereerde documentatie.

| **End point** | **parameters** | **omschrijving** |
| --- | --- | --- |
| **/dataformats** | | Welke data formats worden door de provider ondersteund?<br>_Response_: lijst van file formaten waar de grid data kan worden geleverd; minimaal "netcdf-cf". |
| **/projection** | | Welke projecties ondersteunt het systeem?<br>_Response_: lijst van projecties (EPSG-codes) waar de opgevraagde data naartoe kan worden getransformeerd. |
| **/quantities** | | Welke quantities (grootheden kent de provider?<br>Response: lijst met 'rangeType' objecten, die de binnen het systeem bekende grootheden beschrijven |
| | _pageSize_ | Gewenst aantal items in de response. |
| | _page_ | Gewenste subpagina van de totale lijst met items. |
| | _boundingBox_ | Retourneer alleen de quantities waarvoor grid data aanwezig is binnen het bounding box gebied. De bounding box is uitgedrukt in wgs84 (EPSG:4326) |
| | _startTime_ | Retourneer alleen de quantities waarvoor grid data aanwezig is vanaf het opgegeven start-tijdstip. |
| | _endTime_ | Retourneer alleen de quantities waarvoor grid data aanwezig tot en met het opgegeven eind-tijdstip. |
| **/coverages** | | Welke coverages (grid data) kent de provider?<br>_Response_: lijst met de beschrijving van de aanwezige coverages, zonder de daadwerkelijke data. Dit kan een mengeling van rasters en curvilineaire grids zijn. |
| | _pageSize_ | Gewenst aantal items in de response. |
| | _page_ | Gewenste subpagina van de totale lijst met items. |
| | _boundingBox_ | Retourneer alleen de coverages die geheel of gedeeltelijk binnen het bounding box gebied vallen. De bounding box is uitgedrukt in wgs84 (EPSG:4326) |
| | _startTime_ | Retourneer alleen de coverages met data vanaf het opgegeven start-tijdstip. |
| | _endTime_ | Retourneer alleen de coverages met data tot en met het opgegeven eind-tijdstip. |
| | _quantityId_ | Retourneer alleen de coverages die data voor de grootheid met id _quantityId_ bevatten. |
| | _quantityName_ | Retourneer alleen de coverages die data voor de grootheid met name  _quantityName_ bevatten. |
| | _analysisTime_ |  Retourneer alleen de coverages die geproduceerd zijn (d.w.z. door een model berekend zijn) op het genoemde tijdstip. |
| **/coverages/{coverageId}** | | _Response_: Volledige beschrijving van de coverage met id _coverageId_, zonder de daadwerkelijke data. |
| **/coverages/{coverageId}/data** | | Vraag de data op van de coverage met id _coverageId_.<br>_Response_: Een netcdf-file met daarin van een of meer variabelen de tijdhankelijke waarden op het hele rooster. |
| | _boundingBox_ |  Lever alleen de data die binnen het rechthoekige deelgebied valt (zie volgende regel voor de projectie van de _boundingBox_)  |
| | _projection_ | Projectie waarin de gevraagde data moet worden geleverd. Dit is tevens de projectie van de _boundingBox_. |
| | _quantityId[]_ | Lever alleen data voor een of meer quantities, gespecificeerd door _quantityId[]_. Meerdere quantities worden opgegeven door een komma-gescheiden string. Bij weglating van deze parameter worden alle quantities in de coverage geleverd. |
| | _quantityName[]_ | Lever alleen data voor een of meer quantities, gespecificeerd door _quantityName[]_. Meerdere quantities worden opgegeven door een komma-gescheiden string. Bij weglating van deze parameter worden alle quantities in de coverage geleverd. |
| | _startTime_ | Lever alleen de data vanaf het opgegeven start-tijdstip. |
| | _endTime_ | Lever alleen de data tot en met het opgegeven eind-tijdstip. |
| | _realization_ | Lever, als de coverage het resultaat is van een ensemble run, het resultaat van het ensemble member met als index _realization_. Bij weglating worden de resutaten van alle ensemble members teruggegeven (de ensemble member index vormt dan een extra dimensie in de netcdf-file) |
**/coverages/{coverageId}/point-data** | | Vraag tijdseries op van een of meer grootheden op een of meer punten in de coverage met id _coverageId_.<br>Response: een json string met een lijst van tijdseries, conform de response van het _/timeseries_ end point van de [DD-API](https://digitaledeltaorg.github.io/dd.v201.html). De lijst is &#233;&#233;n lang als er om &#233;&#233;n punt is gevraagd. |
| | _x[]_ en _y_[] | Lever tijdseries op een of meer X,Y-punt(en) in het grid. (Meerdere punten worden opgegeven door in zowel de _x_ als de _y_ parameter meerdere waarden op te geven, gescheiden door een komma.) |
| | _quantityId[]_ | Lever alleen data voor een of meer quantities, gespecificeerd door _quantityId[]_. Meerdere quantities worden opgegeven door een komma-gescheiden string. Bij weglating van deze parameter worden alle quantities in de coverage geleverd. |
| | _quantityName[]_ | Lever alleen data voor een of meer quantities, gespecificeerd door _quantityName[]_. Meerdere quantities worden opgegeven door een komma-gescheiden string. Bij weglating van deze parameter worden alle quantities in de coverage geleverd. |
| | _startTime_ | Lever alleen de data vanaf het opgegeven start-tijdstip. |
| | _endTime_ | Lever alleen de data tot en met het opgegeven eind-tijdstip. |
| | _realization_ | Lever, als de coverage het resultaat is van een ensemble run, het resultaat van het ensemble member met als index _realization_. Bij weglating worden de resutaten van alle ensemble members teruggegeven. |

## Voorbeelden van de response

Zie [voorbeelden](./voorbeelden/voorbeelden.md) voor een aantal voorbeelden van de response.

