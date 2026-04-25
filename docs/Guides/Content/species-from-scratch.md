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

This guide will walk through the steps for creating species in both Nubody and Oldbody, using the example of the Gray species.

**Relevant reading:**
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

We're going to work through creating our species from the bottom up, meaning that we will be starting with making our 'Urist' mob and defining it as a species at the end.

<Tabs>
  <TabItem value="Nubody">

  </TabItem>
  <TabItem value="Oldbody">

  </TabItem>
</Tabs>

:::note

Expect a better guide on displacements in the future. It's a complicated system which you can do some really crazy things with.

*- [mqole](/blog/authors/mqole)*

:::

## Body, Parts, Organs

<Tabs>
  <TabItem value="Nubody">

  </TabItem>
  <TabItem value="Oldbody">

  </TabItem>
</Tabs>

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