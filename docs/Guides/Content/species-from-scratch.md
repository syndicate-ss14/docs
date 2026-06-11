---
authors: [mqole]
tags:
  - guides
  - content

slug: /Guides/Content/species-from-scratch
---

<!-- if you are adding yourself as an author, dont forget to update authors.yml -->

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Species From Scratch

This is a reference guide for anyone who wants to create their own SS14 species.

Wizard's Den currently uses an implementation of `BodySystem` that was overhauled in January of 2026, and completely redefines how species are handled (henceforth referred to as Nubody). Many downstream servers still use the old implementation (Oldbody) to keep interaction with various medical and surgery systems.

This guide will walk through the steps for creating species in both Nubody and Oldbody, using the example of the Moth species.

**Relevant reading:**
- [Adding a Simple Bike Horn - Space Wizards Development Wiki](https://docs.spacestation14.com/en/ss14-by-example/adding-a-simple-bikehorn.html)
- [Converting Oldbody to Nubody - Space Wizards Development Wiki](https://docs.spacestation14.com/en/ss14-by-example/converting-oldbody-to-nubody.html)

## Species Checklist

At absolute minimum, you will need to incorporate the following for your species to work:

<Tabs>
  <TabItem value="Nubody">

- A `SpeciesPrototype`, which should define:
- An abstract `EntityPrototype` for your `BaseMob` where your species' components are all handled,
- A `BaseSpeciesAppearance`,
- A `MarkingsGroup`,
- And a `LocalizedDatasetPrototype` of random names to choose from.

For your `BaseSpeciesAppearance`, you will also need to create:

- All the limb and organ `EntityPrototype`s,
- And a new `InventoryTemplatePrototype`.

  </TabItem>
  <TabItem value="Oldbody">

- A `SpeciesPrototype`, which should define:
- An abstract `EntityPrototype` for your `BaseMob` where your species' components are all handled,
- An `EntityPrototype` parented from `BaseSpeciesDummy`,
- A `SpeciesBaseSpritesPrototype` which will require new `HumanoidBaseSpritePrototype`s for each body part,
- A `MarkingLimitsPrototype`,
- And a `LocalizedDatasetPrototype` of random names to choose from.

For your `BaseMob` entity, you will also need to create:

- A `BodyPrototype` containing your species limbs and organs,
- All the limb and organ `EntityPrototype`s,
- And a new `InventoryTemplatePrototype`.

  </TabItem>
</Tabs>

:::note

Make sure all these prototype definitions are in the right folders. Keeping your file structure consistent with existing species will minimise confusion for future contributors!

:::

## Making a 'Urist'

We're going to work through creating our Moth species from the bottom up, meaning that we will be starting with making our 'Urist' mob and defining it as a species at the end.

<Tabs>
  <TabItem value="Nubody">

  First, let's make a new file `moth.yml` in `Resources/Prototypes/Body/Species`. We'll start by defining our new entity, `MobMoth` like so:

  ```yaml
  - type: entity
    parent:
    - AppearanceMoth
    - BaseSpeciesMobOrganic
    id: MobMoth
    name: Urist McFluff
    components:
  ```

  Our entity here is parented to `BaseSpeciesMobOrganic`, which is an abstact entity that comes with the components that are needed for all species (physics, hands, status effects, et cetera). This base entity can be found in `Resources/Prototypes/Body/species_base.yml` if you want to look at all of the components that come with it.

  Notice how we've also defined another parent, `AppearanceMoth`. We'll focus on this parent entity in the next section. Don't worry about it for now.
  
  </TabItem>
  <TabItem value="Oldbody">
  
  First, let's make a new file `moth.yml` in `Resources/Prototypes/Entities/Mobs/Species`. We'll start by defining our new entity, `BaseMobMoth` like so:

  ```yaml
  - type: entity
    save: false
    abstract: true
    parent: BaseSpeciesMobOrganic
    id: BaseMobMoth
    name: Urist McFluff
    components:
  ```

  Our entity here is parented to `BaseSpeciesMobOrganic`, which is an abstact entity that comes with the components that are needed for all species (physics, hands, status effects, et cetera). This base entity can be found in `Resources/Prototypes/Entities/Mobs/Species/base.yml` if you want to look at all of the components that come with it.

  </TabItem>
</Tabs>

Now that we have our base Moth mob, it's time to consider what unique aspects our species will have, and add components to our mob accordingly. I want my Moth species to have a unique blood type, more emotes, a special accent, and a different set of damage modifiers. I'll add components to accomplish this in accordance with ECS:

  ```yaml
  components:
  - type: Damageable
    damageModifierSet: Moth
  - type: Speech
    speechVerb: Moth
    allowedEmotes: ['Chitter', 'Squeak', 'Flap']
  - type: Bloodstream
    bloodReferenceSolution:
      reagents:
      - ReagentId: InsectBlood
        Quantity: 300
  - type: MothAccent
  ```

  While adding these components, I had to create a new `DamageModifierSet` and new `SpeechVerb`. If you're not sure how to add new components to an entity, it's recommended that you read the SS14 [bikehorn guide](https://docs.spacestation14.com/en/ss14-by-example/adding-a-simple-bikehorn.html) to learn the basics of ECS.

  This is just an example of what you can add to a species. Theoretically, you can add any component you like to your species. Take a look at the components attached to existing species if you aren't sure what your species might need.

## Appearance

Our 'Urist' mob is done. Now let's define its appearance. Nubody creates a new entity for this which our Urist inherits, while Oldbody defines everything on the Urist itself.

In this step, we'll also add displacements to our mob. Displacements are optional sprites that function as a 'map' for clothing and other equippable items, and can move or hide pixels on the sprite of the equipped item to make it fit closer to the mob's silhouette. The `Tools` folder contains some templates and Aseprite plugins for creating your own displacements.

<Tabs>
  <TabItem value="Nubody">

  It's time to revisit `AppearanceMoth`. I'll define this as a new entity, putting it above our Urist in the same `moth.yml` file.

  ```yaml
  - type: entity
    parent: BaseSpeciesAppearance
    id: AppearanceMoth
    categories: [ HideSpawnMenu ]
    name: moth appearance
    components:
  ```

  Same as before, we're parenting this entity to `BaseSpeciesAppearance`, which can be found in `appearance_base.yml`. Pay special attention to `HideSpawnMenu` - this category means that this entity will not be shown in the ingame entity spawn menu, which means that it's less likely to be spawned on accident when someone's looking for our Urist.

  There are two components that we *need* to add to this entity: `InitialBody` and `HumanoidProfile`. If you're familiar with Oldbody, these are roughly equivalent to `Body` and `HumanoidAppearance` respectively - they define the body parts of the species, and the visual data that will be used.

  ```yaml
  components:
  - type: InitialBody
    organs:
      # A list of organs will go here. We'll look at this later!
  - type: HumanoidProfile
    species: Moth
  ```

  Just like with our Urist, we can add additional components to this entity or modify components inherited from `BaseSpeciesAppearance`.

  </TabItem>
  <TabItem value="Oldbody">

  To handle the appearance of our Urist, we first need to add a `HumanoidAppearance` component and a `Body` component to the mob.

  ```yaml
  components:
  - type: HumanoidAppearance
    species: Moth
    hideLayersOnEquip:
    - HeadTop
  - type: Body
    prototype: Moth
    requiredLegs: 2
  ```

  </TabItem>
</Tabs>

For displacements, we'll need to modify our entity's `Inventory` component. Displacements are defined on a per-layer basis - for every layer you want to apply displacement maps to, you will need to point that layer to the desired sprite. Here we are defining some displacements for the `jumpsuit` and the `back` layer:

```yaml
components:
- type: Inventory
  displacements:
    jumpsuit:
      sizeMaps:
        32:
          sprite: Mobs/Species/Moth/displacement.rsi
          state: jumpsuit-male
    back:
      sizeMaps:
        32:
          sprite: Mobs/Species/Moth/displacement.rsi
          state: back
```

You also have the option to create sex-specific displacements in addition to standard displacements. If you choose to use sex-specific displacements for your species, you will need to redefine all your displacement layers, even those that are the same as your non-sexed displacement layers.

```yaml
- type: Inventory
  femaleDisplacements:
    jumpsuit:
      sizeMaps:
        32:
          sprite: Mobs/Species/Moth/displacement.rsi
          state: jumpsuit-female
    back:
      sizeMaps:
        32:
          sprite: Mobs/Species/Moth/displacement.rsi
          state: back
```

This `Inventory` component is also where we can define our species' `InventoryTemplate`, if we have a unique one. `InventoryTemplates` can be used to offset equipped items, determine what slots an entity has for the purposes of equipping items, modify how long it takes to remove an item from a slot, or more.

```yaml
- type: Inventory
  speciesId: moth
```

:::note

Expect a better guide on displacements in the future. It's a complicated system which you can do some really crazy things with.

*- [mqole](/blog/authors/mqole)*

:::

## Body, Parts, Organs

We've pointed our mob to the species and body data that will define how it looks and functions, but we haven't defined our species or our body prototypes yet. Let's start with our body.

Bodies are made up of organs. Organs can be 'internal' (eyes, heart, lungs) or 'external' (arms, torso, head). External organs may also be referred to as 'parts' - this is the term that was used to refer to them in Oldbody, but Nubody consolidated organs and parts into a single prototype. All you need to remember is that internal organs are not visible on the sprite, and external organs / parts are visible.

<Tabs>
  <TabItem value="Nubody">

  Let's start by creating a new base organ.

  ```yaml
  - type: entity
    parent: OrganBase
    id: OrganMoth
    abstract: true
    suffix: Moth
  ```

  Functionally, this is just a copy of `OrganBase` with the `Moth` suffix. Adding a suffix to an entity will show that suffix to anyone searching for this entity in the spawn menu. This is useful to, among other things, let admins tell the difference between two items in the spawn menu both called 'stomach'.

  We're going to do this same process a few times to create some more abstract parent entities we can use in place of the base entities:

  ```yaml
  - type: entity
    parent: OrganMoth
    id: OrganMothInternal
    abstract: true
    components:
    - type: Sprite
      sprite: Mobs/Species/Human/organs.rsi

  - type: entity
    id: OrganMothVisual
    abstract: true
    components:
    - type: VisualOrgan
      data:
        sprite: Mobs/Species/Moth/parts.rsi
    - type: VisualOrganMarkings
      markingData:
        group: Moth

  - type: entity
    parent: [ OrganMoth, OrganMothVisual ]
    id: OrganMothExternal
    abstract: true
    components:
    - type: Sprite
      sprite: Mobs/Species/Moth/parts.rsi
  ```

  Here's where we get into the divide between internal and external organs. For our purposes, the main thing you need to know is that internal organs are invisible, and external organs are visible.

  Our internal organs will use human sprites, so we define our sprite path as `Mobs/Species/Human/organs.rsi` (the same path as humans use). We aren't going to include a `state` here - the reason we attach the path to the parent is so that any child entities don't need to redefine that path. A lot of the base parent organs we'll be relying on later have that path defined already!

  `OrganMothVisual` has two components - `VisualOrgan` and `VisualOrganMarkings`. These should point to your `parts.rsi` folder (meaning, the sprites for your species' default body and limbs), and your marking data. We'll be looking at markings later, but what we're doing here is basically just defining what markings this visual organ can accept.

  The last parent we need to define is our metabolizer. This is done for entities that have unique metabolisms, which can be represented by eating food, breathing gas, or even touching pools of liquid.

  ```yaml

  - type: entity
    id: OrganMothMetabolizer
    abstract: true
    components:
    - type: Metabolizer
      metabolizerTypes: [ Moth ]

  ```

  Metabolizer types are defined in `Resources/Prototypes/Chemistry/metabolizer_types.yml`, but all the information about how a metabolizer type interacts with different reagents or gases will be stored in the data for those specific reagents or gases.

  :::note

  If you're using organs that already exist, you might not need to define all these parents! For instance, if your species has a diet like a human, you can parent your custom stomach to a human's metabolizing organ base.

  :::

  </TabItem>
  <TabItem value="Oldbody">

  </TabItem>
</Tabs>

:::note

Probably also going to make a metabolizer guide in the future.

*- [mqole](/blog/authors/mqole)*

:::~

## Species Prototype

<Tabs>
  <TabItem value="Nubody">

  </TabItem>
  <TabItem value="Oldbody">

  </TabItem>
</Tabs>

:::tip

If you aren't already familiar with how Robust Toolbox handles `Prototype` definitions, now's a great time to explore this using `SpeciesPrototype`.

`SpeciesPrototype.cs` contains `DataField`s like so:

```cs
/// <summary>
/// Whether the species is available "at round start" (In the character editor)
/// </summary>
[DataField(required: true)]
public bool RoundStart { get; private set; } = false;
```

This is a required field, meaning our `SpeciesPrototype` yml will have to include a true or false value for the `roundStart` parameter, and it's set to false by default.

If you aren't sure what parameters you need to include for a prototype's yml, consider looking at the relevant cs file!

*- [mqole](/blog/authors/mqole)*

:::

## Markings and Customization

<Tabs>
  <TabItem value="Nubody">

  </TabItem>
  <TabItem value="Oldbody">

  </TabItem>
</Tabs>

## Extra Considerations