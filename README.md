# dd-grid-api

Achtergrond
-----------

Binnen het Digitale Delta project (zie www.digitaledelta.org) is een web service API ontwikkeld voor het zoeken, vinden een opvragen van tijdseries, de DD-API.  
Zie www.digitaledelta.org/dd.v201.html voor de specifities van de DD-API, en zie https://github.com/DigitaleDeltaOrg/dd-api voor de verdere ontwikkelingen aan de DD-API.

De DD-GRID-API is een vervolg op dit traject, en richt zich op het zoeken, vinden en opvragen van roosterdata: statische en/of tijdafhankelijke data op een raster en/of een curvilineair grid.

Zowel de DD-API als de DD-GRID-API worden ontwikkeld door de Digitale Delta Werkgroep, een samenwerking van een tiental bedrijven en instanties die allemaal betrokken zijn bij het waterbeheer in Nederland (lijst volgt).
De werkgroep opereert sinds 2020 onder de vlag van het [Informatie Water](https://www.ihw.nl/).

Werkwijze
---------

In 2019 is de gewenste functionaliteit voor een web service voor roosterdata in kaart gebracht, hetgeen in eerste instantie in twee iteraties heeft geleid tot een [voorstel voor de DD-GRID-API](./voorstel/oud/dd-grid-api-voorstel.md).

Een vergelijking van dit voorstel met vergelijkbare ontwikkelingen bij OGC, de [OGC API Coverages](https://github.com/opengeospatial/ogc_api_coverages), leerde dat de voorgestelde response qua terminologie zeer verschillend maar qua structuur zeer vergelijkbaar is.  
Daarom is besloten om de OGC API Coverages als basis te nemen, en te kijken in hoeverre we daarmee de beoogde functionaliteit kunnen realiseren. Daar waar noodzakelijk zullen we dan (hopelijk kleine) aanpassingen en uitbreidingen aanbrengen.

Status
------

_**Juli 2020**_:

- OGC API Coverage reponse voorbeelden uitgewerkt (zie [voorbeelden](./voorbeelden/voorbeelden.md)).
- Voorbeelden zijn uitgewerkt worden in json dictionary representatie; worden nog toegevoegd.
- Als volgende actie worden de end points uitgewerkt; eerste opzet staat in [./voorstel/ogc_api_coverages_dd_voorstel_docu.md](./voorstel/ogc_api_coverages_dd_voorstel_docu.md).
- Eerstvolgende inhoudelijke bijeenkomst: september.
