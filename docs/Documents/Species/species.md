---
title: Species
description: 'Species that Macrocosm hosts.'
tags:
  - species
---

# Species

Macrocosm hosts a variety of species that are available for use on downstreams. These species are **disabled by default** and will require manual enabling to appear in-game.

## Enabling a species
Species currently require three files to be edited in order to appear in-game.

First, enable the species in `/Resources/Prototypes/_MACRO/Species/allulalo.yml` by changing the field `roundstart: false` to `roundstart: true`. in the future you will also be able to enable these species as `randomViable` using the same method, which will allow them to appear as randomised humanoids (ghost roles, etc.) without being available to players at roundstart.

Second, enable the relevant guidebook page in `Resources/Prototypes/_MACRO/Guidebook/species.yml` by uncommenting the relevant entry, and then uncommenting its entry to the `Species` guideEntry category in `Resources/Prototypes/Guidebook/species.yml`. Note that if you do not do this second step, your article will simply be orphaned at the top of the guidebook in no category.

Finally, you will need to navigate to `Resources/ServerInfo/Guidebook/Mobs/Species.xml` and add the relevant mob to the guidebook index page.
For example, to add Allulalo to this page, you would take:
```xml
  <Box>
  <GuideEntityEmbed Entity="AppearanceArachnid" Caption="Arachnid"/>
  <GuideEntityEmbed Entity="AppearanceDiona" Caption="Diona"/>
  <GuideEntityEmbed Entity="AppearanceDwarf" Caption="Dwarf"/>
```
and add `AppearanceAllulalo` like so:
```xml
  <Box>
  <GuideEntityEmbed Entity="AppearanceAllulalo" Caption="Allulalo"/>
  <GuideEntityEmbed Entity="AppearanceArachnid" Caption="Arachnid"/>
  <GuideEntityEmbed Entity="AppearanceDiona" Caption="Diona"/>
  <GuideEntityEmbed Entity="AppearanceDwarf" Caption="Dwarf"/>
```

## Species Categorization

Species in this document are categorised into **two categories**, `Normal` and `Wildcard`

`Normal` species are as you would expect a regular, vanilla space station roundstart species to function. In Base SS14, this would include Moths, Reptiles, Humans, etc.

`Wildcard` species are intended for non-roundstart purposes. You can enable them roundstart if you like, but they aren't designed or balanced around it. In regular vanilla SS14 this would include Skeletons, Gingerbread Men, etc.

Wildcard species will be denoted like so, at the beginning of the article:
:::warning
This species is a **wildcard** and is not intended to be made available roundstart.
:::