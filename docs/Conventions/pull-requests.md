---
tags:
  - Conventions
---

# Pull Requests

## Conventions

We recommend referring to Wizard's Den's [Conventions](https://docs.spacestation14.com/en/general-development/codebase-info/conventions.html) and the documentation of Microcosms in additions to the standards stated here.

### Content should be tested in Microcosms before being brought to Macrocosm

Pull requests made to Macrocosm will be treated with increased scrutiny and with the expectation that the pull request is a full-fledged, feature-complete addition to the project. Due to the bureaucracy involved with accepting changes to Macrocosm, we want to avoid small iterative bugfixes and microbalance changes as much as possible. 

We highly recommend playtesting and finalizing content in a Microcosm first and upstreaming it when the content is stable.

### Content brought to Macrocosm must match our license

Our codebase is under the MIT License. <!-- link to our repos license goes here when we make it --> While other codebases are free to use any license that suits them, we require that all code brought to Macrocosm be licensed under MIT as well. **It is the responsibility of the Pull Request creator to ensure that they are following the license of all code involved. If we believe that a PR has not received appropriate permission to be relicensed to MIT, it will be closed.**

### Original content goes in `_MACRO` <!-- wip namespace maybe need something less horny -->

As we are downstream of Wizard's Den, namespacing content unique to Macrocosm is important for easing the difficulty of upstream merges.

<!-- THIS ONES CONTROVERSIAL!!! READ IT AND DECIDE!!! -->

All unique content **must be in the `_MACRO`** namespace. This includes all new **prototypes**, **audio**, **textures**, **locale strings**, and **C# code**.

### Content should be easy for a downstream to disable

Macrocosm prides itself on its customizability as a base for downstreams. All content should have some way to "opt out" of it if feasible, ideally via cvars or minimal YML edits. **If a PR does not provide a way to disable itself, it may be rejected.**

### Comment changes made outside of `_MACRO`

If you alter code, you need to leave a comment to indicate that the code was altered. This is to prevent confusion and accidental erasure of your changes in the future.

Additionally, changes to a YAML prototype that add components should be added to the end of the prototype.

#### Some examples of appropriate comments in a YML file:

<!-- code from impstation#2744 w/ comments changed -->
```yml
- type: entityTable
  id: LetterRareEntityTable
  table: !type:GroupSelector
    children:
    - id: ResearchDisk5000
    - id: JointRainbow
    - id: StrangePill
      amount: !type:RangeNumberSelector
        range: 1, 3
    - !type:GroupSelector
      children:
      - id: Brutepack
      - id: Ointment
      - id: Gauze
      - id: Bloodpack
      # macrocosm start
      - id: SimpleSuture
      - id: Tincture
      # macrocosm end
    - id: SyndicateBusinessCard
      weight: 0.5
    # macrocosm start
    - !type:NestedSelector
      tableId: LetterImpRareEntityTable
```
This prefix and suffix format is preferable if a large amount of additions are made to the prototype; a suffix is only necessary if the prototype continues after the additions.

<!-- code from impstation#3319 with comments changed -->
```yml
- type: reagent
  id: Egg
  name: reagent-name-raw-egg
  group: Foods
  desc: reagent-desc-raw-egg
  physicalDesc: reagent-physical-desc-mucus-like
  flavor: raw-egg
  color: white
  recognizable: true
  metabolisms:
    Food:
      effects:
      - !type:AdjustReagent
        reagent: UncookedAnimalProteins
        amount: 0.5
      - !type:AdjustReagent # macrocosm
        conditions:
          - !type:OrganType
            type: Kodepiia
        reagent: UncookedAnimalProteins
        amount: 1
```
Note that there is just one comment here, on the line with the effect type; even though everything after it alters the prototype, it's considered all one addition, so just one comment suffices.


#### Some examples of appropriate comments in a CS file:

<!-- code from impstation#4024 w/ comments changed -->
```csharp
[DataField("damage")] public DamageSpecifier Damage = new()
{
    DamageDict = new ()
    {
        { "Cellular", 0.3 }, // macro "Poison", 0.3 > cellular 0.3
    }
};
```
This inline comment is preferable for very small, single line changes.

<!-- code from funky-station#368 w/ comments changed-->
```csharp
// BEGIN Macrocosm
// Smoking in bed is dangerous!
if (HasComp<SleepingComponent>(containerManager.Owner)
    && HasComp<BuckleComponent>(containerManager.Owner))
{
    // 25% chance over the lifetime of a cigarette (66 times)
    if (_random.Prob(0.03f))
        _flammableSystem.AdjustFireStacks(containerManager.Owner, 0.5f, null, true);
}
// END Macrocosm
```
This prefix and suffix format is preferable for multi-line blocks of code added to a file.

### Use comments to describe what your code is doing

This is helpful both for maintainers to vet the code and ensure that it works as intended, and for future contributors to more easily understand code and be able to iterate on it.

Here is a sample of a well-summarized, fully explained piece of code:

<!-- code from impstation#3946 i picked this one because its funny sorry fan -->
```csharp
    /// <summary>
    /// Our function for handling the breeding action once all checks are finished and the
    /// animal has approached its partner.
    /// </summary>
    /// <param name="approacher"></param>
    /// <param name="approached"></param>
    /// <returns></returns>
    public bool TryBreedWithTarget(EntityUid approacher, EntityUid approached)
    {
        // Realistically this should never return false but it's just here for the moment
        if (!_entManager.TryGetComponent<ImpReproductiveComponent>(approacher, out var component))
            return false;

        // Same with this one but i'm paranoid
        if (!_entManager.TryGetComponent<ImpReproductiveComponent>(approached, out var partnerComp))
            return false;

        // Just being 100% sure we aren't trying to self breed.
        if (approacher == approached)
            return false;

        // The one giving birth needs to have options
        if (partnerComp.PossibleInfants == null)
            return false;

        // one last check in case someone beat us to the cow or bred us on the way there
        // It's dumb but unless I make the system assign pairings this is the best i can think of for the moment
        if (!CanYouBreed((approacher, component)) || !CanYouBreed((approached, partnerComp)))
            return false;

        // Ready up for birth
        partnerComp.Pregnant = true;
        partnerComp.EndPregnancy = partnerComp.PregnancyLength;

        // Add them to our list of pregnant NPCs to be tracked
        _mobsWaiting.Add(approached, partnerComp);

        // Picks which offspring to give birth to based on the mob we bred with
        var ctx = new EntityTableContext(new Dictionary<string, object>
        {
            { ValidPartnerCondition.PartnerContextKey, component.MobType },
        });
        partnerComp.MobToBirth = _entTable.GetSpawns(partnerComp.PossibleInfants, ctx: ctx).ElementAt(0);

        if (TryComp<InteractionPopupComponent>(approached, out var interactionPopup))
            Spawn(interactionPopup.InteractSuccessSpawn, _transform.GetMapCoordinates(approached));

        partnerComp.PreviousPartner = approacher;

        // GET HUNGRY GET THIRSTY
        _hunger.ModifyHunger(approacher, -component.HungerPerBirth);
        _hunger.ModifyHunger(approached, -partnerComp.HungerPerBirth);

        _thirst.ModifyThirst(approached, -component.HungerPerBirth);
        _thirst.ModifyThirst(approached, -partnerComp.HungerPerBirth);

        _adminLog.Add(LogType.Action, $"{ToPrettyString(approacher)} (carrier) and {ToPrettyString(approached)} (partner) successfully bred.");
        return true;
    }
```