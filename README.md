# dd-grid-api

Achtergrond
-----------

Binnen het Digitale Delta project (zie www.digitaledelta.org) is een web service API ontwikkeld voor het zoeken, vinden een opvragen van tijdseries, de DD-API.  
Zie www.digitaledelta.org/dd.v201.html voor de specifities van de DD-API, en zie https://github.com/DigitaleDeltaOrg/dd-api voor de verdere ontwikkelingen aan de DD-API.

De DD-GRID-API is een vervolg op dit traject, en richt zich op het zoeken, vinden en opvragen van roosterdata: statische en/of tijdafhankelijke data op een raster en/of een curvilineair grid.

Zowel de DD-API als de DD-GRID-API worden ontwikkelingd door de Digitale Delta Werkgroep, een samenwerking van een tiental bedrijven en instanties die allemaal betrokken zijn bij het waterbeheer in Nederland (lijst volgt).
De werkgroep opereert sinds 2020 onder de vlag van het [Informatie Water](https://www.ihw.nl/).

Werkwijze
---------

In 2019 is de gewenste functionaliteit voor een web service voor roosterdata in kaart gebracht, hetgeen heeft geleid tot een in twee iteraties tot stand gekomen [voorstel voor de DD-GRID-API](./voorstel/dd-grid-api-voorstel.md).

Een vergelijking van dit voorstel met vergelijkbare ontwikkelingen bij OGC, de [OGC API Coverages](https://github.com/opengeospatial/ogc_api_coverages), leerde dat de voorgestelde response qua terminologie zeer verschillend maar qua structuur zeer vergelijkbaar is.  
Daarom besloten om over de OGC API Coverages als basis te nemen, en te kijken in hoeverre we daarmee de beoogde functionaliteit kunnen realiseren. Daar waar noodzakelijk zullen we dan (hopelijk kleine) aanpassingen en uitbreidingen aanbrengen.

Status
------

_**Juli 2020**_:

- OGC API Coverage reponse voorbeelden uitgewerkt (zie [voorbeelden](./voorbeelden/voorbeelden.md)).
- Voorbeelden gaan nog uitgewerkt worden in json dictionary representatie.
- Als volgende actie worden de end points uitgewerkt.
- Eerstvolgende inhoudelijke bijeenkomst: september.
