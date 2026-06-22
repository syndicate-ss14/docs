---
tags:
- proposals
---

# Porting Roadmap

Backporting PRs from our microcosms to the Macrocosm repository can happen for many reasons, but are usually one of two:

1. The feature is desired by multiple microcosms
2. The feature is an extreme maintenance burden

*(You can read more about these reasons on our [Voting](../Conventions/voting.md) page.)*

This page exists to streamline the process of backporting by creating a list of PRs that exist on microcosms which fit one of these two criteria. It serves as a reference for:

- The kinds of PRs that Macrocosm would like to see backported / that players and developers are interested in
- Whether PRs that are desired on Macrocosm have existing licensing or conceptual approval in advance
- A to-do list of PRs people can work on
- A showcase of the cool features created by our microcosms!

**This is not a formal voting page.** Not every PR in this list has implicit conceptual or code approval from all microcosms. Even if a PR is listed as being approved by all microcosms, it will still require a formal vote before being merged.

If you wish to add a PR to this list, please open a PR on our [docs repository](https://github.com/syndicate-ss14/docs)!
<!-- mq note: might be cool to set up a little bot or something that can also auto-open issues for this. having that done could even be used AS a formal vote. thats a whole process. but really anything to streamline devstuffs ya know -->

## PR Categories
| Category | Description |
|-|-|
| Accessibility | Features designed to ease the physical, real-life burden of playing the game.
| Admin Tooling | Features for in-game administration and moderation.
| Art | Generally, resprites.
| Atmospherics | Anything to do with the 'atmospheric simulator' gameplay loop.
| Cargo / Salvage | Anything that hooks into the Cargo department, including shuttles and shipbuilding.
| Character / Species | Customization decided by players in the in-game lobby.
| Chat | 
| Combat
| Core Tech
| Discord Integration
| Engineering
| Graphics
| Guidebook
| Integration Tests
| Localization
| Mapping
| Medical
| MIDI
| Preferences
| Roundflow / Antag
| Science
| Security
| Service
| Silicon

## Roadmap
| Feature Name | Description | Category | Microcosm PR(s) | License | Notes |
|-|-|-|-|-|-|
| Pronouns on Crew Manifest	| Adds pronouns to the crew manifest. | Accessibility | [Impstation #87](https://github.com/impstation/imp-station-14/pull/87)
Last Message before Death Webhook | Discord webhook which will, at the end of a round, relay the last message sent by all players who died | Discord Integration | [Impstation #3045](https://github.com/impstation/imp-station-14/pull/3045)
Old & New Xenoarch | Combines upstream's new & old xenoarcheology systems, where an artifact randomly selects one of the two systems. | Science | [Impstation #2894](https://github.com/impstation/imp-station-14/pull/2894)
Tourists | Midrounds with the job of being annoying. | Roundflow/Antag | [Impstation #3189](https://github.com/impstation/imp-station-14/pull/3189)
Mech QOL | Makes mobs pathfind to mechs, and gives mechs the ability to wideswing. | Combat | [Impstation #2082](https://github.com/impstation/imp-station-14/pull/2082)
Visitor Species | adds a toggle to a species to enable them to be selected by RandomHumanoidSystem, letting you have species be playable but not roundstart via ghost roles | Character/Species | [Impstation #3522](https://github.com/impstation/imp-station-14/pull/3522) |
all of imps gun shit | all of imps gun shit. dvd player is insane. side note would be so fucking funny to UN fork these | Combat | Impstation
Reagent Fires | Make it a cvar like spacewind. It makes heat an actual issue on the station in a good way. Has a few bugfixes that makes it function correctly too. Last PR in the chain needs mostly just the visual stuff and can skip the structural damage | Core Tech | [Funkystation #2295](https://github.com/funky-station/funky-station/pull/2295), [#2331](https://github.com/funky-station/funky-station/pull/2331), [#2429](https://github.com/funky-station/funky-station/pull/2429), [#2360](https://github.com/funky-station/funky-station/pull/2360), [#2446](https://github.com/funky-station/funky-station/pull/2446), [#2363](https://github.com/funky-station/funky-station/pull/2363)
Washing Machine content | Imp people seemed interested in more integration with the system | Service | [Funkystation #2703](https://github.com/funky-station/funky-station/pull/2703), [#2841](https://github.com/funky-station/funky-station/pull/2841), [#2844](https://github.com/funky-station/funky-station/pull/2844)
Holo doorbell | Already shared by Imp and Funky | Cargo/Salvage | [Impstation #1357](https://github.com/impstation/imp-station-14/pull/1357)	
End screen medals | Already shared by Imp and Funky | Roundflow/Antag | Impstation	https://github.com/funky-station/funky-station/pull/2236	
Spray paint | "An item that allows you to recolor the sprites of entities. Also a generic entity system to handle entity recoloring in general. It's used in Den (prebase) for recoloring loadout items, too. Spray paint cans can be ordered from Cargo (Logistics) and used to recolor five entities each. It has popular use for outfit design, interior renovation, ""custom item"" play-pretend, admemes, and roleplay gags. Admins also have access to a magic spray paint can with a color picker. Spray paint can be removed using a towel or damp rag." | Core Tech | The Den	"PREBASE: https://github.com/TheDenSS14/TheDen/pull/1872 https://github.com/TheDenSS14/TheDen/pull/1909 https://github.com/TheDenSS14/TheDen/pull/2328 REBASE:https://github.com/TheDenSS14/TheDenTwo/pull/51"	
Supermatter | all member servers have this i think? so more unifying the implementation | Engineering			
DenTraits / Entity Traits | "A replacement of WizDen's trait system.  Instead of traits being entirely based on profile preferences, EntityTraits work sort of like status effects - entities can have a component that store their traits, and each trait is an entity contained in the trait holder.  • Traits can be added to any entity, even non-humanoid and non-player entities  • Traits can do more than add/remove components and status effects - they can perform C# logic through ""trait functions""  • Traits have logic for both adding AND removing, making all traits reversible  • Admins can add and remove traits from any entity using commands, making them admemeable  • Because trait logic is tied to entitites/components rather than prototypes, traits can store instantiated data" | Character/Species | The Den	https://github.com/TheDenSS14/TheDenTwo/pull/53 	
Mail / Couriers | "New job for the Cargo department whose job is to deliver mail to crew. When mail is opened, it adds spesos to Cargo's budget. Mail envelopes and packages contain miscellaneous fun items for the recipient, such as food, toys, clothing, or sillier things. I forgot wizden added mail LOL. Courier job...?" | Cargo/Salvage			
Microwave Separation / Frontier Cooking / TG-ish Cooking | 	"Microwaves are split into four appliances - microwave, oven, assembler, med. assembler. All cooking recipes are recategorized accordingly. relevant devs have given permission to port this to MIT codebases so it should be chill" | Service | Impstation	"https://github.com/new-frontiers-14/frontier-station-14/pull/1935  https://github.com/impstation/imp-station-14/pull/2571 "	
Den Character Requirements | "pending rewrite for den2 Refactor of job requirement system. Requirement parameters are contained in a ""context"" class; all fields are optional. The ""reason"" message is decoupled from success/failure logic. Makes it easier to add new job/character requirements. Also makes it possible to write requirement-related integration tests." | Core Tech | The Den	"PREBASE: https://github.com/TheDenSS14/TheDen/pull/1581 "	
Toys | combine our toys / plushies				
Food rebalance | rebalances reagent inventories of every single craftable edible item in the game so it at minimum matches the ingredients. huge for food being filling | Service | Impstation	https://github.com/impstation/imp-station-14/pull/2021	
cosmic cult | bring back coscult | Roundflow/Antag | Funkystation		
Food Sequence Burger Tweaks | "- visual tweaks to foodsequence burgers to make ingredients layer slightly better - tofu slices, chanterelle mushrooms, carp added to ingredient list - new ingredient sprites for all cutlets, tofu slices, chanterelle, chilis, and tomatoes note: DEN added cooked carp and carp cutlets for this. do we want that? note: imp also has quite a few new food sequence burger ingredients. can compare notes" | Service | The Den	"https://github.com/TheDenSS14/TheDen/pull/1289 https://github.com/impstation/imp-station-14/pull/471 "	
Species TLC (Arachnid, Lizard, Moth) | Adds unique sounds to Arachnids and Moths, and new emotes to Lizards. Additionally adds new organs for insect blood and blue blood species respectively. | Character/Species | Impstation	https://github.com/impstation/imp-station-14/pull/3539 https://github.com/impstation/imp-station-14/pull/3626 https://github.com/impstation/imp-station-14/pull/3571	
Paperwork Form Fields | i think they're an RMC feature? allows you to add fields to sheet of paper for quick user input with out a pen - signature fields, free text, check boxes, etc. | Core Tech | The Den		
Pool-Themed Decorations | lounge chairs, beach umbrellas, swim rings, pool tile, and pool water - for all your mapping and indoor beach/pool-themed fun | Mapping | The Den	https://github.com/TheDenSS14/TheDen/pull/2071	
Costume Bundles	Bags | used to hold clothing and costume parts. Mostly used to reduce the inventory length of the AutoDrobe by condensing all the gimmicky costumes into bundles. | Service | The Den	https://github.com/TheDenSS14/TheDen/pull/1903	 https://github.com/syndicate-ss14/macrocosm/pull/7 
Singularity Warping Toggle | allows people to disable the singularity's screen warping effects. | Accessibility | Impstation	https://github.com/impstation/imp-station-14/pull/27	
Weather Toggle | allows people to disable weather effects. honestly weather effects need to be made more pleasant in general, but a weather toggle is pretty commonplace anyways! | Accessibility | Impstation	"https://github.com/impstation/imp-station-14/pull/3986 https://github.com/impstation/imp-station-14/pull/4077"	
Gas Resprites | visually easier on the eyes compared to the original texture, which is kind of flashy. needs to be atomized out, PR contains unrelated resprites (god bless old imp you messy bitch) | Accessibility | Impstation	https://github.com/impstation/imp-station-14/pull/1111	
AI Static Toggle | allows people to disable the static in AI blindspots, replacing it with a simple gradient. | Accessibility	Impstation | https://github.com/impstation/imp-station-14/pull/4011	
Improved Flash Visuals + Flash Reduced Motion Toggle | more toggles for reduced motion! also adjusts the base flash effect in a way that keeps the flash's combat use in tact. | Accessibility | Impstation	https://github.com/impstation/imp-station-14/pull/3722	
Glasses Lens Slot | eyewear has a "lens slot" for inserting lenses, allowing you to have special eyewear that supports prescriptions | Core Tech | Impstation	"https://github.com/impstation/imp-station-14/pull/304 https://github.com/impstation/imp-station-14/pull/2441 https://github.com/impstation/imp-station-14/pull/3104  https://github.com/impstation/imp-station-14/pull/3166  https://github.com/impstation/imp-station-14/pull/3505 "	
Round status / emote panel | "ss13-style panel that allows you to see the current round time and gamemode, plus a tab for quick-using emotes. ss13 inspired. den ported it from goob i think? i (portfiend) want to recode it" | Core Tech | The Den		
Toggle Self Ghost Action | do you know how sucks it is trying to take a screenshot, toggling ghosts and then still seeing your ghost ass in frame? exactly. is this core tech it's like a button | Core Tech | Funkystation https://github.com/funky-station/funky-station/pull/906	
Breeding System | ever wanted to crossbreed a cow and a slime? It's almost done! | Core Tech | Impstation	https://github.com/impstation/imp-station-14/pull/3946	
Obvious Examine | Accessories that will show up on a character's examine text, such as pins, badges, and medals. | Core Tech | Impstation		
Go Woke with Descriptions and such | "lists PRs that adjust culturally insensitive content. i think it is good to be sensitive and aware and to keep macrocosm upstream tidy as well. currently just listing impstation PRs but if other forks have related PRs please include also tell me what category this is help"	| | "https://github.com/impstation/imp-station-14/pull/1494 https://github.com/impstation/imp-station-14/pull/3928	
Ghosts Seeing Damage and Solutions on Examine | Ghosts having the ability to be informed during observing? Sign me up buster! | Core Tech | Impstation	https://github.com/impstation/imp-station-14/pull/1318	
Reagent Color Text Contrast | Adds contrast to the color of a reagent's text to make readable against the dark text background. | Accessibility | Impstation	https://github.com/impstation/imp-station-14/pull/1439	

## Completed Features
| Feature Name | Description | Category | Originating Server | License | Link to PR | Notes |
|-|-|-|-|-|-|-|