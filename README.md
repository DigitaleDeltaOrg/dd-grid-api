# dd-grid-api

Achtergrond
-----------

Binnen het Digitale Delta project (zie www.digitaledelta.org) is een web service API ontwikkeld voor het zoeken, vinden een opvragen van tijdseries, de DD-API.  
Zie www.digitaledelta.org/dd.v201.html voor de specifities van de DD-API, en zie https://github.com/DigitaleDeltaOrg/dd-api voor de verdere ontwikkelingen aan de DD-API.

De DD-GRID-API is een vervolg op dit traject, en richt zich op het zoeken, vinden en opvragen van roosterdata: statische en/of tijdafhankelijke data op een raster en/of een curvilineair grid.

Zowel de DD-API als de DD-GRID-API worden ontwikkeld door de Digitale Delta Werkgroep, een samenwerking van een tiental bedrijven en instanties die allemaal betrokken zijn bij het waterbeheer in Nederland (lijst volgt).
De werkgroep opereert sinds 2020 onder de vlag van het [InformatieHuis Water](https://www.ihw.nl/).

Werkwijze
---------

In 2019 is de gewenste functionaliteit voor een web service voor roosterdata in kaart gebracht, hetgeen in een aantal iteraties heeft geleid tot een eerste [eerste voorstel voor de DD-GRID-API](./voorstel/oud/dd-grid-api-voorstel.md).

Een vergelijking van dit eerste voorstel met vergelijkbare ontwikkelingen bij OGC, de [OGC API Coverages](https://github.com/opengeospatial/ogc_api_coverages), leerde dat de voorgestelde response qua terminologie zeer verschillend maar qua structuur zeer vergelijkbaar is.  
Daarom is besloten om de OGC API Coverages als basis te nemen, en te kijken in hoeverre we daarmee de beoogde functionaliteit kunnen realiseren. Deze slag is ondertussen uitgevoerd, heeft geleid tot versie 0.9 van de DD-GRID-API:
- zie [dd-grid-api-documenation-nl.md](./voorstel/dd-grid-api-documenation-nl.md) voor een (Nederlandstalige) beschrijving van de de DD-GRID-API.<br>Deze is handmatig opgesteld. Een uit de OAS3-specificatie gegenereerde versie verschijnt binnenkort; daartoe moet eerst de documentatie in de specificatie worden uitgebreid.
- zie [voorstel/dd-grid-api-oas3.json](./voorstel/dd-grid-api-oas3.md) voor de OAS3-specificatie.<br>In deze specificatie wordt verwezen naar het schema voor de specificatie van de response [./voorstel/dd-grid-api-coverage-schema.json]. Van deze response zijn een tweetal [voorbeelden](./voorbeelden/voorbeelden.md) gegeven.

Bij het uitwerken van de DD-GRID-API hebben we t.o.v. de OGC API Coverages nogal wat aanpassingen en uitbreidingen aangebracht. Deze zullen hier binnenkort worden beschreven.

Status
------

_**Oktober 2020**_:
- Versie 0.9 opgesteld.
- Docu nog toevoegen.
- Over een aantal punten nog een besluit nemen.

_**September 2020**_:
- Reponse voorbeelden op aantal punten verbeterd.
- Concept-uitwerking van de end points besproken.

_**Juli 2020**_:

- OGC API Coverage reponse voorbeelden uitgewerkt.
- Voorbeelden zijn uitgewerkt worden in json dictionary representatie; worden nog toegevoegd.
- Als volgende actie worden de end points uitgewerkt.
- Eerstvolgende inhoudelijke bijeenkomst: september.
