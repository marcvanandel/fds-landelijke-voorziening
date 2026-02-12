# Patroon verstrekkingspunt cumulatie gelijkvormige bronnen

Als er meerdere bronnen zijn die gelijkvormige informatie bevatten, dan kunnen deze gecumuleerd
worden in één verstrekkingspunt; zie [Federatief.Datastelsel.nl | Data deel
concept](https://federatief.datastelsel.nl/kennisbank/datadeelconcept/#cumulatie-en-consolidatie).
Bij cumulatie worden de bronnen zonder integriteitscontroles samengevoegd en beschikbaar gesteld.
Als meerdere bronnen in de combinatie conflicterende informatie bevatten, wordt deze informatie ook
als zodanig gepubliceerd. Dit integenstelling tot consolidatie; zie [patroon verstrekkingspunt
consolidatie gelijkvormige
bronnen](./patroon-verstrekkingspunt-consolidatie-gelijkvormige-bronnen.md).

Cumulatie betekent:

- dat gelijkvormige informatie wordt samengevoegd tot één geheel
- dat conflicterende situatie als zodanig worden ontsloten
- dat het geheel één _bounded context_[^1] vormt als geheel (hoewel het samenvoegend
  verstrekkingspunt wel conflicten tussen bronnen kan bevatten)

![Enkelvoudige bounded
context](./patroon-verstrekkingspunt-cumulatie-gelijkvormige-bronnen.excalidraw.svg)

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
