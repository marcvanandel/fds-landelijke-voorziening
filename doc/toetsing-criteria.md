# Toetsing criteria

## Inleiding

Dit document toetst het patroon **samenvoegend verstrekkingspunt** aan de criteria die zijn
gedefinieerd in de workshop "Data bij de bron" (slide 18, januari 2026). Het samenvoegend
verstrekkingspunt, ook wel _landelijke voorziening_ (LV), is een verstrekkingspunt dat gegevens uit
meerdere bronnen samenvoegt en als één geheel ontsluit aan afnemers.

Het [FDS datadeelconcept](https://federatief.datastelsel.nl/kennisbank/datadeelconcept/)
onderscheidt drie vormen van gegevens samenvoegen: cumulatie, consolidatie en compilatie. In deze
toetsing behandelen we de eerste twee, de varianten die gelden voor gelijkvormige bronnen:

- **Cumulatie**: bronnen worden samengevoegd zonder bronhouder-overstijgende integriteitscontroles;
  conflicten worden als zodanig gepubliceerd. Zie
  [patroon verstrekkingspunt cumulatie gelijkvormige bronnen](./patroon-verstrekkingspunt-cumulatie-gelijkvormige-bronnen.md).
- **Consolidatie**: er worden consolidatieregels toegepast om conflicten op te lossen, en er wordt
  teruggemeld aan de bronnen. Zie
  [patroon verstrekkingspunt consolidatie gelijkvormige bronnen](./patroon-verstrekkingspunt-consolidatie-gelijkvormige-bronnen.md).

Compilatie (het combineren van gegevens uit _ongelijkvormige_ bronnen voor specifieke doeleinden)
valt buiten de scope van deze toetsing.

## 1. Actualiteit

_"De actualiteit moet bij elke gegevensdeling en elk gegevensgebruik inzichtelijk zijn en worden
vastgelegd. De context bepaalt hoe actueel gegevens minimaal moeten zijn."_

Een samenvoegend verstrekkingspunt werkt per definitie met een kopie van de brongegevens. Er zit
altijd vertraging tussen een mutatie in de bron en de beschikbaarheid in het verstrekkingspunt. De
mate van vertraging hangt af van het synchronisatiemechanisme (event-driven of periodieke
batch-imports) en de afspraken tussen bron en verstrekkingspunt over synchronisatiefrequentie en
-prioriteit. Het verstrekkingspunt moet deze vertraging transparant maken door actualiteitsmetadata
per record bij te houden (tijdstip van bronmutatie, tijdstip van synchronisatie).

Dit geldt voor zowel cumulatie als consolidatie. Bij consolidatie kan de vertraging groter zijn
wanneer conflictdetectie en -resolutie extra verwerkingstijd vergen, wat des te meer reden is om de
actualiteit expliciet vast te leggen.

## 2. Juistheid en consistentie

_"De ontsloten gegevens moeten juist zijn en onderling consistent, conform wat de bronnen als
waarheid beschouwen."_

Bij **cumulatie** worden bronnen zonder bronhouder-overstijgende integriteitscontroles samengevoegd.
Als twee bronnen conflicterende informatie bevatten, wordt dit conflict als zodanig gepubliceerd. De
afnemer ziet de inconsistentie en moet daar zelf mee omgaan. Het verstrekkingspunt biedt dan geen
enkele garantie op consistentie.

Bij **consolidatie** worden conflicten gedetecteerd en opgelost via consolidatieregels. Gegevens
worden mogelijk afgekeurd, er wordt teruggemeld aan de bronnen en er worden herstellende acties
verwacht. Het resultaat is een consistenter beeld voor de afnemer, maar de juistheid is afhankelijk
van de kwaliteit van de consolidatieregels. Bovendien kan de eindsituatie afwijken van wat de
bronnen uiteindelijk vaststellen: de bronnen kunnen tot andere oplossingen komen dan de
consolidatieregels.

## 3. Authenticiteit

_"De afnemer moet kunnen vertrouwen dat de ontvangen gegevens daadwerkelijk afkomstig zijn uit de
aangewezen bron en niet zijn gewijzigd. Het FDS beschouwt dit als onderdeel van *provenance*: de
betrouwbaarheid en authenticiteit van gegevens (zie
[traceerbaarheid](https://federatief.datastelsel.nl/kennisbank/traceerbaarheid/))."_

In een samenvoegend verstrekkingspunt ontvangen afnemers hun data niet direct van de bron maar via
een tussenliggend systeem. Vergeleken met het estafettemodel is dit een verbetering (minder
tussenschakels), maar vergeleken met directe bronbevraging is het een concessie.

Bij **cumulatie** is de authenticiteit relatief goed bewaard: de data wordt 1-op-1 overgenomen uit
de bronnen zonder transformatie. Provenance-metadata per record (welke bron, welk moment, welke
synchronisatie) kan de authenticiteit borgen.

Bij **consolidatie** is de authenticiteit een groter aandachtspunt. Het verstrekkingspunt trekt
eigen conclusies bij conflicten. De ontsloten data bevat dan afgeleide informatie die niet direct
toewijsbaar is aan één specifieke bron. De provenance wordt complexer: naast de bronherkomst moet
ook de toegepaste consolidatieregel worden vastgelegd. Dit staat op gespannen voet met het principe
dat data authentiek moet zijn aan de oorspronkelijke vastlegging.

Bij consolidatie is het verstrekkingspunt feitelijk een nieuwe bron: het ontsluit niet alleen
gegevens uit de oorspronkelijke bronnen, maar ook eigen conclusies op basis van consolidatieregels.
Dit betekent dat een consoliderend verstrekkingspunt zowel maximaal de originele bronnen dient te
weerspiegelen, als de eigen afgeleide conclusies zelfstandig moet verantwoorden, met bijbehorende
eisen aan herleidbaarheid en provenance.

## 4. Toegangscontrole

_"De toegang tot gegevens moet gecontroleerd kunnen worden, bij voorkeur door of namens de
bronhouder."_

Een samenvoegend verstrekkingspunt kan centrale toegangscontrole implementeren. Het FDS onderscheidt
vier niveaus van toegangsbeperkingen (zie
[toegang](https://federatief.datastelsel.nl/kennisbank/toegang/)): verbinding, vraagstelling,
entiteitstoegang en dataniveau. Een verstrekkingspunt kan op al deze niveaus beperkingen toepassen:
één autorisatiepunt voor afnemers, uniforme afhandeling van toegangsverzoeken, en de mogelijkheid om
fijnmazige policy-based autorisatieregels (PBAC) toe te passen.

Het nadeel is dat de bronhouder directe controle verliest over wie toegang krijgt tot de gegevens.
De bronhouder moet vertrouwen op het toegangsbeleid van het verstrekkingspunt. Dit vergt goede
governance-afspraken en mandaatverlening. Het FDS benadrukt dat zowel aanbieders als afnemers
verantwoordelijkheid dragen voor het toepassen van beperkingen.

Voor beide varianten geldt dit op dezelfde manier. Het verschil zit niet in cumulatie versus
consolidatie, maar in de mate waarin de bronhouder betrokken is bij het toegangsbeleid van het
verstrekkingspunt.

## 5. Herleidbaarheid

_"Het moet navolgbaar zijn waar gegevens vandaan komen, de data lineage van bron tot afnemer. Het
FDS vat onder [traceerbaarheid](https://federatief.datastelsel.nl/kennisbank/traceerbaarheid/) drie
verwante begrippen samen: *traceerbaarheid* (volgen van gegevens door ketens), *lineage*
(bewerkingen die data heeft ondergaan), en *provenance* (betrouwbaarheid en authenticiteit)."_

Herleidbaarheid is een van de belangrijkste voordelen van het samenvoegend verstrekkingspunt ten
opzichte van alternatieven. In het estafettemodel lopen gegevens via meerdere tussenstations
waardoor de herkomst moeilijker traceerbaar wordt. Een samenvoegend verstrekkingspunt reduceert het
aantal schakels: de afnemer heeft één verstrekkingspunt en dat verstrekkingspunt heeft directe
relaties met de bronnen.

Het verstrekkingspunt kan lineage-metadata bijhouden per record: uit welke bron, op welk moment
ontvangen, via welke synchronisatie. Het FDS biedt hiervoor concrete standaarden: FSC-logging voor
het loggen van transacties, het Logboek Dataverwerkingen voor verwerkingsverantwoording, en de W3C
PROV-standaard voor het modelleren van provenance. Dit maakt de herleidbaarheid naar de bron (van
oorsprong) expliciet.

Bij **consolidatie** is er een subtiliteit: als het verstrekkingspunt een eigen resolutie toepast,
moet ook die beslissing herleidbaar zijn. De consolidatieregels moeten gedocumenteerd zijn en de
lineage moet aangeven welke bronrecords aan de basis liggen van het geconsolideerde resultaat.

## 6. Dataminimalisatie

_"Er mogen niet meer gegevens worden opgeslagen en gedeeld dan strikt noodzakelijk voor het doel."_

Een samenvoegend verstrekkingspunt aggregeert per definitie alle gegevens uit alle aangesloten
bronnen. Het verstrekkingspunt bevat daarmee een brede dataset, breder dan wat individuele afnemers
doorgaans nodig hebben.

Dit staat op gespannen voet met het principe van dataminimalisatie. De data is weliswaar
_beschikbaar_ voor afnemers, maar niet elke afnemer heeft alle data nodig. Zonder aanvullende
maatregelen ontsluit het verstrekkingspunt meer data dan strikt noodzakelijk.

Mitigatie is mogelijk via de mechanismen die het FDS beschrijft voor
[toegang](https://federatief.datastelsel.nl/kennisbank/toegang/): beperking op vraagstelling (welke
vragen mag een afnemer stellen), entiteitstoegang (over welke personen/zaken), en dataniveau (welke
kenmerken). Het
[dataminimalisatieprincipe uit de FDS datadiensten](https://federatief.datastelsel.nl/kennisbank/datadiensten/)
stelt dat afnemers gevraagde kenmerken moeten beperken via vragen, toegangscontrole, of combinaties
daarvan. Dit vereist echter dat het verstrekkingspunt op de hoogte is van de doelbinding per
afnemer.

Dit geldt voor zowel cumulatie als consolidatie; het onderscheid is hier niet relevant.

## 7. Bewaar- en vernietigingstermijnen

_"Gegevens moeten worden bewaard en vernietigd conform de geldende termijnen, die in principe door
de bron worden bepaald."_

Het verstrekkingspunt heeft een eigen kopie van de brongegevens en heeft daarmee een eigen
retentiebeleid nodig. Dit beleid moet zijn afgestemd op de bewaartermijnen van de bronnen. Als een
bron gegevens vernietigt, moet het verstrekkingspunt daar tijdig van op de hoogte zijn en de
betreffende gegevens ook verwijderen.

Dit vergt synchronisatie-afspraken voor vernietiging, niet alleen voor mutaties. Het risico bestaat
dat het verstrekkingspunt gegevens langer bewaart dan de bron toestaat, bijvoorbeeld door vertraging
in de synchronisatie of door onvolledigheid van de vernietigingssignalen.

Bij **consolidatie** is er een extra complicatie: geconsolideerde records zijn afgeleid van meerdere
bronrecords. Als één bronrecord wordt vernietigd, moet het geconsolideerde record worden herberekend
of verwijderd.

## 8. Kosten voor opslag, beheer en beveiliging

_"De kosten van de oplossing voor opslag, operationeel beheer en beveiliging moeten in verhouding
staan tot de baten."_

Een samenvoegend verstrekkingspunt is een extra systeem dat moet worden gebouwd, beheerd en
beveiligd. Dit brengt kosten met zich mee die er niet zouden zijn als afnemers de bronnen direct
bevragen.

Daar staat tegenover dat het verstrekkingspunt een veelheid aan point-to-point koppelingen
elimineert. Zonder LV zouden _N_ afnemers elk _M_ bronnen moeten bevragen, wat leidt tot _N × M_
koppelingen met elk hun eigen kosten voor beveiliging en beheer. Het verstrekkingspunt reduceert dit
tot _M + N_ koppelingen.

De netto kosten hangen af van de schaal: bij veel afnemers en veel bronnen is het verstrekkingspunt
kostenefficiënt; bij weinig afnemers kan het extra systeem een onevenredige investering zijn.

Voor beide varianten gelden vergelijkbare kostenstructuren, al vergt consolidatie meer
verwerkingscapaciteit voor de conflictresolutie.

## 9. Performance en beschikbaarheid

_"De gegevens moeten met voldoende snelheid en betrouwbaarheid beschikbaar zijn voor afnemers."_

Dit is de primaire motivatie voor het samenvoegend verstrekkingspunt. Afnemers bevragen één punt in
plaats van _N_ bronnen. Het verstrekkingspunt kan worden geoptimaliseerd voor leesperformance
(indexering, caching, horizontale schaalbaarheid) onafhankelijk van de bronsystemen. De
beschikbaarheid van het verstrekkingspunt is niet direct afhankelijk van de beschikbaarheid van
individuele bronnen: als een bron tijdelijk onbereikbaar is, kan het verstrekkingspunt de laatst
bekende stand blijven ontsluiten.

Vergeleken met directe bronbevraging door meerdere afnemers reduceert dit ook de belasting op de
bronsystemen: zij hoeven niet elke individuele afnemer te bedienen.

Dit voordeel geldt voor zowel cumulatie als consolidatie.

## 10. Complexiteit oplossing

_"De oplossing moet zo eenvoudig mogelijk zijn; complexiteit brengt risico's met zich mee voor
beheersbaarheid en correctheid."_

De complexiteit verschilt aanzienlijk tussen de twee varianten.

**Cumulatie** is relatief eenvoudig: gegevens uit bronnen samenvoegen en ontsluiten. De complexiteit
zit vooral in de synchronisatie en in het communiceren van conflicten aan afnemers.

**Consolidatie** is aanzienlijk complexer. Er zijn consolidatieregels nodig die vastleggen hoe
conflicten worden opgelost. Er moet een terugmeldproces zijn. Het FDS definieert
[terugmelden](https://federatief.datastelsel.nl/kennisbank/datadiensten/#terugmelden) als standaard
deelfunctie van datadiensten, waarmee bronnen geïnformeerd worden over conflicten. Bronnen kunnen
herstellende acties ondernemen, waarna het verstrekkingspunt eerder genomen resolutiebeslissingen
moet intrekken. De eindsituatie kan anders zijn dan wat eerder is gepubliceerd. Dit vergt naast
technische complexiteit ook organisatorische governance: wie stelt de regels vast, wie is
verantwoordelijk bij fouten, hoe wordt het proces bewaakt?

De complexiteit van consolidatie is een bewuste trade-off: het biedt afnemers een consistenter
beeld, maar tegen de prijs van een aanzienlijk complexer systeem.
