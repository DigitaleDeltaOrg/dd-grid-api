# Voorstel DD-OGC-GRID-API

## Inleiding

Deze pagina bevat de beschrijving van een voorstel voor DD-GRID-API. Deze Digitale Delta API voor roosterdata is gebaseerd op de [OGC API Coverages]. Over een goede naam van de API moet worden nagedacht; voorlopig wordt hij hier DD-OGC-GRID-API genoemd.
De DD-OGC-GRID-API-specificatie [./ogc_api_coverages_dd_voorstel_oas3.json](./ogc_api_coverages_dd_voorstel_oas3.json) is opgesteld conform OAS3, m.a.w. de specificatie valideert tegen het [OAS3-schema](https://github.com/OAI/OpenAPI-Specification/blob/master/schemas/v3.0/schema.json), dat voor de volledigheid ook hier bij de DD-OGC-GRID-API-specificatie is opgenomen (./oas3-schema.json).
De resource objects van de DD-OGC-GRID-API-specificatie zijn nog niet formeel gespecificeerd. Zie [../voorbeelden/voorbeelden.md](../voorbeelden/voorbeelden.md) voor enkele uitwerkingen van de response.

In eerste instantie was een door de DD-werkgroep eigen roosterdata-API uitgewerkt. De documentatie van deze eerste opzet is te vinden in [./oud/dd-grid-api-voorstel.md](./oud/dd-grid-api-voorstel.md).  
Deze bleek qua naamgeving enorm af te wijken van de OGC-terminologie, maar bleek qua structuur zeer vergelijkbaar. Daarom is besloten om te onderzoeken of we met de OGC API Coverages uit de voeten zouden kunnen.  
Voor de _resource objects_ in de response is dat zonder meer het geval, zie bovengenoemde voorbeelden. Ook qua _end points_ blijkt er grote overeenstemming te zijn.

## Vertrekpunten

Onderstaande documentatie heeft als basis gediend voor wat er nu ligt, waarbij de onder _Aanpassingen_ beschreven wijzigingen en toevoegingen zijn aangebracht.

### OGC API Coverage specifatie voor de resources objects

_Todo_

### OGC API Coverage specifatie voor de urls

_Todo_

### Aanpassingen

_Todo_

## Conceptversie DD-OGC-GRID-API end points

| **End point** | **parameters** | **omschrijving** |
| --- | --- | --- |
| **/dataformats** | | Ondersteunde data formats. Minimaal "netcdf-cf" |
| **/outputCrss** | | Welke projecties ondersteunt het systeem?<br>Response: lijst van projecties waar bij het opvragen van data naar toe kan worden getransformeerd |
| **/quantities** | | Welke quantities kent de provider?<br>Response: lijst met quantity objecten |
| | _limit_ | (OGC naam voor) max #items in de response. Wellicht beter: _pageSize_ |
| | _bbox_ | Gebied van interesse |
| | _time_ | Periode van interesse |
| | _f_ | Format voor de response (default: json) |
| **/coverages** | | Welke coverages kent de provider?<br>Response: lijst met metadata-objecten van de coverages (kan mengeling van rasters en curvilineair zijn) |
| | _limit_ | (OGC naam voor) max #items in de response. Wellicht beter: _pageSize_? |
| | _time_ | Periode van interesse |
| | _quantity_ | Geef alleen coverage die data voor _quantity_ bevatten |
| | _f_ | Format voor de response (default: json) |
| **/coverages/{coverageId}** | | lijst van sub end points van de coverage |
| **/coverages/{coverageId}/domainset** | | Domainset van de coverage |
| | _subset_ | Deelgebied van de volle domainset.  Wellicht beter: _bbox_?|
| **/coverages/{coverageId}/rangeType** | | Rangetype van (i.e. de grootheden op) de coverage |
| | _rangeSubset_ | Selectie van de gewenste quantities|
| **/coverages/{coverageId}/metaData** | | Metadata van de coverage |
| **/coverages/{coverageId}/rangeSet** | | (Verwijzing naar?) de daadwerkelijke data op de coverage |
| | _subset_ | Deelgebied van de volle coverage.  Wellicht beter: _bbox_?|
| | _rangeTypeSubset_ | Selectie van de gewenste quantities|
| **/coverages/{coverageId}/description** | | Beschrijving van een coverage (waarin verschilt dit van metadata?)|
| **/coverages/{coverageId}/all** | | Vraag data op van de coverage|
| | _subset_ | Deelgebied van de volle domainset.  Wellicht beter: _bbox_?|
| | _rangeSubset_ | Selectie van de gewenste quantities|
| | _areaOfInterest_ | WKT-string die de gewenste uitsnede beschrijft |
| | _outputCrs_ | Gewenste projectie. (Tevens projectie van de areaOfInterest.) |
| | _startTime_ | Data vanaf (inclusief) |
| | _endTime_ | Data tot en met |
| | _analysisTime_ | Productietijd van de data set |
| | _realization_ | Realization index |
| | _point[]_ | X,Y-punt(en) Response is dan een json file met een lijst van tijdseries conform de response van de DD-API. (De lijst is 1 lang als er om 1 grootheid op 1 punt is gevraagd.) |
