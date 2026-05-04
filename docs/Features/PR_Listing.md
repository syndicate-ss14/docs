---
tags:
  - features
---

# PRs

Macrocosm has a number of features to choose from. This is a comprehensive list of all Macrocosm features by PR in order to create a guide for Microcosm owners.

By default, all features that are not purely enhancements or direct upgrades of features are disabled by default.

## PR 4 - Salvage Ticket System

Tickets are disabled by default. To enable them: 
1. Have mappers replace the existing SalvageVendor with a SalvageTicketVendor. This will be immobile and force salvagers to return to the station to deposit tickets.
2. Change this CVar to True in your server's settings "salvage.tickets_enabled". This allows recyclers and ore refiners to produce tickets.

## PR 5 - Salvage Ruins

Ruins are enabled by default, but updating a YML listing can make the ruins pulled by the salvage magnet resemble your station ruins.

Edit the file Resources/Prototypes/_MACRO/Procedural/ruin_mals.yml and update the map id and path to your fork's maps. Directions included for details.
