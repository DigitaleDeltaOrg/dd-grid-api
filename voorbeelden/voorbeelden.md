# Uitgewerkte voorbeelden

Voorbeelden van de metadata response volgens OGC API Coverages:
- dd-grid-regular-ogc-api-coverage.json:<br>
raster, drie grootheden
- dd-grid-displacement-ogc-api-coverage.json:<br>
curvilineair grid; x- en y-coordinaten niet uitgewerkt, omdat dat niet paste in het OGC schema.

Beide voorbeelden valideren tegen het schema _ogc-schema-dd.json_. Dit bevat slechts één wijziging t.o.v. het [originale ogc schema](https://github.com/opengeospatial/ogc_api_coverages/blob/master/standard/openapi/coverage-schema.json), namelijk het niet langer verplicht stellen van het “coordinates”-element in het “displacement” element (n.a.v. het bovengenoemde niet geschikt zijn van de co&#246;rdinaten).
