---
tags:
  - features
---

# Species

Macrocosm features a variety of unique and complex alien species.

By default, all Macrocosm species are disabled for character creation. To enable a species, you must navigate to their species prototype and remove the following line:

![A screenshot of an IDE. The line "roundStart: false" is highlighted and underlined.](/img/docs/features/enable-species.png)

By default, all Macrocosm species will not be selected for randomly generated characters, such as visitor shuttles or other random ghost roles. To enable a species to be randomly generated, you must navigate to their species prototype and change `midRoundRandomViable:` from `false` to `true`.

![A screenshot of an IDE. The line "midRoundRandomViable: true" is underlined.](/img/docs/features/enable-midround.png)

A short description of all Macrocosm species are as follows:

## Allulalo
<div class="text--center">
    ![A screenshot of an Allulalo.](/img/docs/features/species/allulalo.png)
</div>

 Allulalo are a small avian species with alcoholic blood reminiscent of raptors. They lack traditional hands, and instead manipulate items using their beak.
 The largest drawbacks for playing an Allulalo is the singular hand and the inability to use large machines without buckling themselves or floating (be it moon-boots or lack of gravity).
 Allulalo can also inject people they bite with a weak toxin up to four times, with a 20 second recharge time (for one bite).
 Allulalo are naturally faster than other species. It's a hefty balance concern so disable it if you want by commenting out the MovementSpeedModifier component in their prototype.

 Enabling them is a good idea if you lack avian species (Say, you only have vox enabled), and want another species that introduces gameplay challenges.
 You might want to keep them disabled in a server that doesn't prioritize non-humanoid species, or one with an abundance of Avian species.

## Ant

 Ants are literally just ants. They die incredibly easily but can go under airlocks. They're not intended to be roundstart species, but can be enabled as one if you wish.

## Apid
<div class="text--center">
    ![A screenshot of an Apid.](/img/docs/features/species/apid.png)
</div>


 Apids are smaller, floatier moths. You can almost think of them like a moth equivelant of a monkey stats wise.
 They have dramatically lower health, are limited to one hand (although they can still wield!), and are permanently immune to gravity in all contexts. In return, they're very fast!

 Apids are primarily intended to be a ghost role, but that code isn't on Macrocosm. Instead, they're here as an option if you want to use them for something, or if youd like to roundstart them for your server.

 Be aware if you choose to do so that they have a lot of overlap with moths, and have a fairly dramatic lack of customization options, so if you would like to have them as an available species you might want to give them a little bit of love and care first.
 (And if you do, please send it upstream!)

## Decapoid
<div class="text--center">
    ![A screenshot of a Decapoid.](/img/docs/features/species/decapoid.png)
</div>

 Decapoids are fairly a complicated species.
 They first of all, can survive in space without any worries whatsoever, as they take no barotrauma or cold damage from space. However, they do take twice as much heat damage (Steam the crab. Do it)
 In order to speak, decapoids need to wear a vaporizer, which acts as a gas mask as Decapoids breathe exclusively water vapor, nothing else, however they don't get poisoned by anything.
 They also cannot be injected into, their shell too thick to pierce. this means they have to sip medicine or be placed into cryopods.
 And their final limiting factor is the fact they only have one usable hand, as the other is a large claw that makes them clumsy.

 You might choose to enable them if you want a relatively complex species in your server that takes some getting used to.
 They're fairly difficult to play in medical and security positions (as they cant use defibs OR guns).
 You might want them disabled if you're worried about the balance of a spacewalking species, or find them too limiting.

## Gastropoid
<div class="text--center">
    ![A screenshot of a Gastropoid.](/img/docs/features/species/gastropoid.png)
</div>

 Gastropoids are a species of snail aliens. They're very heavy, very slow, and have two back slots.
 They resist pierce and slash, but are exceptionally (5x) weak to cold damage and start freezing faster.
 In return, however, they can handle much higher temperatures than most species.
 They get poisoned horrifically by salt (and most salt related chems), and sspeeaak vveerryy sslloowwllyy.
 They also can't wear shoes, but they have perma-magboots at all times thanks to being stuck to the floor.

 You might like to enable them if you are looking for a species that can haul a lot of materials, or maybe you just like them because they're charming. Don't expect combat prowess, though.

## Gray
<div class="text--center">
    ![A screenshot of a Gray.](/img/docs/features/species/gray.png)
</div>

 Grays are very self explanatory.
 They have a whopping 50% weakness to all brutes, and are very lightweight, but in return they are extremely resilient to energy weapons after all their years of being shot by ray guns.
 They have a word replacement accent that makes them almost completely inscrutable, and are mostly just very funny in all contexts they end up in.

 You might choose to enable them if you want something more light-hearted for your fork, or conversely you may want to keep them disabled if you're trying to be as serious as possible.

## Kodepiia
<div class="text--center">
    ![A screenshot of a Kodepiia.](/img/docs/features/species/kodepiia.png)
</div>

 Kodepiia are cuttlefish-esque aliens. 
 They have a very striking and diverse set of markings and customization, to allow for two Kodepiia to look dramatically different from each other.
 Kodepiia have an action that randomizes their appearance, similar to a DNA scrambler, once every ten minutes.
 They also have a very large and mostly custom set of emote sounds.
 Kodepiia get hungry faster than most other species, usually starving after twenty minutes without eating, and have a very restrictive diet: cooked protein makes them sick, and nutriment has no effect on them, meaning they must eat raw meat. They have a button that allows them to take a bite out of a crit or dead body to sate hunger, but if used too many times on the same body, will gib it.

 You might choose to enable them if you want a species with an unprecedented level of character customization, or if you want a species that engages with the service department in an unusual way. You may want to keep them disabled if your fork would not be comfortable with the mimicry identity of the species, or its ability to eat (and round remove) other players.

## Ungu
<div class="text--center">
    ![A screenshot of an Ungu.](/img/docs/features/species/ungu.png)
</div>

 Ungu are a slow, hulking, ungulate species.
 They cannot wear hardsuits, and instead their only form of space protection are softsuits, such as the EVA suit. They are highly resistant to cold but weak to piercing and poison damage. Their melee attacks are slower but more powerful than the average species and they have the ability to charge forward at a high speed. 

 You might choose to enable Ungu if you want a unique take on a "gentle giant" species, but you may want to keep them disabled if their gameplay disadvantages are too much for your fork.