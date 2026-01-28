# FDS Landelijke Voorziening

Uitwerking van patronen, voorwaarden en aspecten... rondom **landelijke voorzieningen** (LVs).

Verschillende variaties:

- 01 LV gelijkvormige bronnen incl. conflictresolutie
- 02 LV gelijkvormige bronnen 1-op-1 replicatie
- 03 LV gelijkvormige selectie uit vergelijkbare bronnen incl. conflictresolutie
- 04 LV gelijkvormige selectie uit vergelijkbare bronnen 1-op-1 replicatie
- ...? (welke variaties hebben we nog meer?)

Per variatie werken we uit:

- 1 Markdown file in `/doc` folder
  - filename conventie: `lv-<nr>-<naam>.md`
- Daarin staat volgens template:
  - Naam
  - Beschrijving (uitgebreide toelichting)
  - Sterke punten
  - Zwakke punten
  - Overwegingen
- Begeleidende plaatjes
  - in [Excalidraw](https://excalidraw.com/) of [draw.io](https://app.diagrams.net/)
  - filename conventie: `lv-<nr>-<naam>-<naam-plaatje>.excalidraw.io`

## Bronnen

Inspiratie en referentie bronnen die gebruikt zijn:

- [federatief.datastelsel.nl | Data deel concept](https://federatief.datastelsel.nl/kennisbank/datadeelconcept/)

## Contributie

We werken voornamelijk met Markdown files en plaatjes ... waarbij de plaatjes
[excalidraw](https://excalidraw.com/) plaatjes kunnen zijn (waarvoor ook een [VS Code
plugin](https://marketplace.visualstudio.com/items?itemName=pomdtr.excalidraw-editor)) voor
beschikbaar is.

Voor presentaties maken we gebruik van [Marp](https://marp.app/).

Line breaks op 120 en zie [.editorconfig](./.editorconfig).

## Development

Lokaal kan mbv [asdf](https://asdf-vm.com/) gebruik gemaakt worden van command line tools:

```bash
asdf install
```

## Formalities

This repo is licensed under [EUPL v1.2](LICENSE).
