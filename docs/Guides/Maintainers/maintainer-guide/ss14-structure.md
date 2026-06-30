---
authors: [portfiend]
tags:
  - guides
  - maintainers
---

# The Structure of Space Station 14

:::note
This document was copy-pasted from [portfiend](/blog/authors/portfiend)'s document archive and is not specific to Macrocosm. It may be subject to further iteration in the future.
:::

## Entity Component System

SS14 uses an **Entity Component System** framework - instead of an entity being defined as a "pig" that is a type of "animal" that is a type of "mob" (object-oriented approach), a "pig" entity has a collection of components that apply all of its functionality. 

A pig may be `Damageable` (allowing it to take damage,) `ToolRefineable` (allowing it to be sliced into meat when dead), and have a `MobState` (alive or dead), which allows you to kill the pig and butcher it for its meat. Other components may give the pig a `Bloodstream`, make it oink and wander around, give it organs, and allow it to consume food. All of these components are modular and self-contained, allowing other entities to have all, some, or none of this functionality.

An entity is an object that has components. Components **only** store data, like "hunger rate = 5". Systems translate this data into functionality.

## Languages

Much of the game's **logical flow** is written in the programming language C# ("C-Sharp"). This is all of your entity systems and components - like turning inputs into movement, or decreasing your hunger over time, or dealing damage to an animal when you attack them.

A bit of C# code might look like this:

```csharp
// Very truncated for demonstration.

public sealed class GasPortableSystem : EntitySystem
{
  [Dependency] private NodeContainerSystem _nodeContainer = default!;

  public override void Initialize()
  {
    base.Initialize();
    SubscribeLocalEvent<GasPortableComponent,
        AnchorStateChangedEvent>(OnAnchorChanged);
  }

  private void OnAnchorChanged(Entity<GasPortableComponent> ent,
      ref AnchorStateChangedEvent args)
  {
    if (!_nodeContainer.TryGetNode(ent.Owner, ent.Comp.PortName,
        out PipeNode? portableNode))
      return;

    portableNode.ConnectionsEnabled = args.Anchored;
  }
}
```

All of the game's **content** is written in a data serialization language called YAML. YAML is written like collections of keys and values - the values in questions are much simpler to parse. You can add new items, mobs, species, structures, and more using only YAML.

A bit of YAML markup might look like this:

```yml
# Very truncated for demonstration.

- type: entity
  abstract: true
  parent: [ BaseStructureDynamic, BasePaperLabelableVisualized ]
  id: GasCanister
  name: gas canister
  description: A canister that can contain any type of gas. It can be
    attached to connector ports using a wrench.
  components:
  - type: GasPortable # This is the same GasPortableComponent in the C# example.
  - type: GasCanister
    gasTankSlot:
      name: comp-gas-canister-slot-name-gas-tank
      ejectOnBreak: true
      whitelist:
        components:
        - GasTank
```

Many player-facing strings (except for entity names and descriptions) utilize a localization ID in order to translate the same string into different languages. This is done in the **[Fluent](https://projectfluent.org/)** language, and supports variables that are supplied in C# code.

A bit of Fluent markup might look like this:

```fluent
comp-gas-canister-ui-release-pressure = Release Pressure (kPa):
comp-gas-canister-ui-pressure = {$pressure} kPa
comp-gas-canister-slot-name-gas-tank = Gas tank
```

A handful of other languages are used in the game's development - sprite definitions utilize the [Robust Station Image](https://docs.spacestation14.com/en/specifications/robust-station-image.html) (RSI) specification, guidebook entries and UI are written in XAML/XML, server configurations are written in TOML, and so on. C# is generally the most "technical" language that SS14 contributors use.
