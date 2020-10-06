# Uitgewerkte voorbeelden

Voorbeelden van de coverage response volgens de DD-GRID-API van de OGC API Coverages:
- dd-grid-regular-ogc-api-coverage.json:<br>
raster, drie grootheden
- dd-grid-displacement-ogc-api-coverage.json:<br>
curvilineair grid, zelfde envelope, zelfde drie grootheden; curvilinear (i.e. 'displaced'grid).

Beide voorbeelden valideren tegen het schema voor de specificatie van de response [./voorstel/dd-grid-api-coverage-schema.json].  

De response bevat alleen de metadata van een coverage (json). De daadwerkelijke data wordt in netcdf-cf formaat geleverd. Zie [../dd-grid-api-documentation.md] voor beschrijving van de DD-GRID-API.
