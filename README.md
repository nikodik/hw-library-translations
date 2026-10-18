# [HW] Library — translations

Shared translations of RimWorld mods, used by **[HW] Library Gate** together with **[HW] Auto Translate**.
When a player has untranslated strings in their language and this library has them, the game offers to install them.

## Layout

```
<Language>/<packageId>.xml   one file per mod and language (AutoTranslateCache format)
filters/blocked.txt          blocked words: strings with them are dropped
index.json, index.json.sig   generated and signed by the maintainer, do not edit
```

`<Language>` is the first word of the game's language folder: `Russian`, `German`, `ChineseSimplified`...

```xml
<AutoTranslateCache mod="author.modname" name="Mod name" language="Russian" version="1">
  <e k="K" key="Some.Keyed.Key"><s>Original text {0}</s><r>Translated text {0}</r></e>
  <e k="D" t="ThingDef" key="SomeDef.label"><s>original label</s><r>translated label</r></e>
</AutoTranslateCache>
```

`s` is the exact original text. A string is used only while the mod still has that exact original, so mod
updates never show outdated translations.

## Sending translations

In the game: Mod settings → **[HW] Library Gate** → Share → *Prepare my translations*. Then open an issue here
with the **submission** label and attach the files from the outbox folder. You need a GitHub account.

## Checks

Every string is checked twice, when it is merged and again in every player's game:

- placeholders (`{0}`, `[PAWN_nameDef]`, `<color>`...) must match the original exactly;
- no links and no words from `filters/blocked.txt`;
- the length must be reasonable.

`index.json` is signed with the maintainer's key, so the game rejects any file that was changed by anyone else.
