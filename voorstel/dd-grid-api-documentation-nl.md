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
| **/dataformats** | | Welke data formats worden door de provider ondersteund?<br>Response: lijst van file formaten waar de grid data kan worden geleverd; minimaal "netcdf-cf". |
| **/outputCrss** | | Welke projecties ondersteunt het systeem?<br>Response: lijst van projecties waar de opgevraagde data naartoe kan worden getransformeerd. |
| **/quantities** | | Welke quantities (grootheden kent de provider?<br>Response: lijst met 'rangeType' objecten, die de binnen het systeem bekende grootheden beschrijven |
| | _pageSize_ | Gewenst aantal items in de response. |
| | _page_ | Gewenste subpagina van de totale lijst met items. |
| | _boundingBox_ | Retourneer alleen de quantities waarvoor grid data aanwezig is binnen het bounding box gebied. |
| | _startTime_ | Retourneer alleen de quantities waarvoor grid data aanwezig is vanaf het opgegeven start-tijdstip. |
| | _endTime_ | Retourneer alleen de quantities waarvoor grid data aanwezig tot en met het opgegeven eind-tijdstip. |
| **/coverages** | | Welke coverages (grid data) kent de provider?<br>Response: lijst met de beschrijving van de aanwezige coverages, zonder de daadwerkelijke data. Dit kan een mengeling van rasters en curvilineaire grids zijn. |
| | _pageSize_ | Gewenst aantal items in de response. |
| | _page_ | Gewenste subpagina van de totale lijst met items. |
| | _boundingBox_ | Retourneer alleen de coverages die geheel of gedeeltelijk binnen het bounding box gebied vallen. |
| | _startTime_ | Retourneer alleen de coverages met data vanaf het opgegeven start-tijdstip. |
| | _endTime_ | Retourneer alleen de coverages met data tot en met het opgegeven eind-tijdstip. |
| | _quantityId_ | Retourneer alleen de coverages die data voor de grootheid met id _quantityId_ bevatten. |
| | _quantityName_ | Retourneer alleen de coverages die data voor de grootheid met name  _quantityName_ bevatten. |
| | _analysisTime_ |  Retourneer alleen de coverages die geproduceerd zijn (d.w.z. door een model berekend zijn) op het genoemde tijdstip. |
| **/coverages/{coverageId}** | | Volledige beschrijving van de coverage met id _coverageId_, zonder de daadwerkelijke data. |
| **/coverages/{coverageId}/data** | | Vraag de data op van de coverage met id _coverageId_. |
| | _boundingBox_ |  Lever alleen de data die binnen het rechthoekige deelgebied valt. Bij het opvragen van _boundingBox_De boundingbox |
| | _areaOfInterest_ | Lever alleen data die het gewenste deelgebied valt dat beschreven wodt door de WKT-string, uitgedrukt  |
| | _outputCrs_ | Gewenste projectie van de geleverde data. Dit is tevensd de projectie van de _boundingBox_ of _areaOfInterest_. |
| | _quantityId[]_ | Lever alleen data voor een of meer quantities, gespecificeerd door _quantityId[]_. (Meerdere quantities worden opgegeven door een puntkomma-gescheiden string.) |
| | _quantityName[]_ | Lever alleen data voor een of meer quantities, gespecificeerd door _quantityName[]_. (Meerdere quantities worden opgegeven door een puntkomma-gescheiden string.) |
| | _startTime_ | Lever alleen de data vanaf het opgegeven start-tijdstip. |
| | _endTime_ | Lever alleen de data tot en met het opgegeven eind-tijdstip. |
| | _realization_ | Lever, als de coverage het resultaat is van een ensemble run, het resultaat van het ensemble member met als index _realization_. |
| | _point[]_ | Lever tijdseries op een of meer X,Y-punt(en) in het grid. (Meerdere punten worden opgegeven door een puntkomma-gescheiden string: 1203.6,142.0;1424.3,171.2;...)<br>Response: een json file met een lijst van tijdseries, conform de response van het _/timeseries_ end point van de @@@TODO: DD-API.<br>De lijst is &#233;&#233;n lang als er om &#233;&#233;n punt is gevraagd.<br>Als de coverage het resultaat is van een ensemble run, moet ook de _realization_ parameter worden meegegeven. |

## Voorbeelden van de response

Zie [voorbeelden](../voorbeelden/voorbeelden.md) voor een aantal voorbeelden van de response.

