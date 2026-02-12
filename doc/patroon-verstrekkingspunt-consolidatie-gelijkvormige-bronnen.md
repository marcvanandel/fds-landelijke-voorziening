# Patroon verstrekkingspunt consolidatie gelijkvormige bronnen

Als er meerdere bronnen zijn die gelijkvormige informatie bevatten, dan kunnen deze geconsolideerd
worden in één verstrekkingspunt; zie [Federatief.Datastelsel.nl | Data deel
concept](https://federatief.datastelsel.nl/kennisbank/datadeelconcept/#cumulatie-en-consolidatie).
Integenstelling tot cumulatie betekent consolidatie wel dat er eigen conclusies getrokken kunnen
worden in dit verstrekkingspunt in geval dat er conflicten bestaan tussen informatie uit
verschillende bronnen. Dit kan bijvoorbeeld het geval zijn als de bronnen regionaal aansluitend
dienen te zijn, maar er blijken tóch overlappende records / entiteiten voor te komen. Zie ook
[patroon verstrekkingspunt cumulatie gelijkvormige
bronnen](./patroon-verstrekkingspunt-cumulatie-gelijkvormige-bronnen.md)

Consolidatie betekent:

- dat gelijkvormige informatie in principe wordt samengevoegd tot één geheel
- dat er teruggemeld moet worden aan de bronnen waar conflicterende informatie zich voordoet en
- dat er in het verstrekkingspunt consolidatieregels worden toegepast om tot een resolutie te komen
- dat er mogelijk vanuit de bronnen herstellende acties worden ondernomen, waarbij de beslissingen
  in het consoliderende verstrekkingspunt moeten worden ingetrokken. Mogelijk is de eindsituatie
  anders dan eerder gepubliceerd vanuit het verstrekkingspunt omdat de bronnen tot andere
  oplossingen komen dan de consolidatieregels.
- dat het verstrekkingspunt _eigen verantwoording_ dient te geven over conflict resolutie en dus de
  consolidatieregels
- dat er meerdere _bounded contexts_[^1] bestaan, namelijk de bronnen en het samenvoegend
  verstrekkingspunt; dat zijn namelijk (opgeteld) niet volledig met elkaar gelijk, wel gerelateerd
  en gelijkvormig

![Meerdere bounded
contexten](./patroon-verstrekkingspunt-consolidatie-gelijkvormige-bronnen.excalidraw%20copy.svg)

// TODO

[^1]: Bounded context is een begrip uit Domain Driven Design en wordt ook in de [Handreiking van Uit
    betrouwbare
    bron](https://website-digilab-overheid-nl-research-uit-betrouw-e1f39021ce924c.gitlab.io/handreiking/handreiking.html#registergrenzen.md__bounded-context)
    scherp beschreven:

  > Binnen een domein kunnen meerdere subdomeinen of taakgebieden bestaan. Daarbij horen
  > verantwoordelijkheden, die zijn toegekend aan specifieke teams, afdelingen of bedrijfseenheden.
  > Zij worden ondersteund door eigen semantiek, processen en regels. Deze zaken kunnen worden
  > beschreven in een **model**: een systeem van abstracties dat beschrijft hoe men vanuit een
  > taakgebied naar de wereld kijkt en reageert op veranderingen in de buitenwereld. Zo’n model is
  > beschreven in **gemeenschappelijke taal** die binnen het hele taakgebied begrepen wordt. Model
  > en taal beschrijven dus een voor betrokkenen herkenbare ‘blauwdruk’ van het taakgebied, die
  > (onder andere) de basis kan vormen voor het ontwerp van een register. Een in gemeenschappelijke
  > taal ondubbelzinnig en samenhangend gemodelleerd taakgebied noemen we een **‘bounded context’**.
  >
  > Hier geldt (zoveel mogelijk) dat:
  > 
  > - dezelfde concepten eenduidig geïnterpreteerd worden (op basis van gemeenschappelijke taal),
  > - regels en gedrag consistent zijn, en
  > - bedrijfsprocessen op elkaar aansluiten.
