<%*
// ###########################################################
//                       Helper Functions
// ###########################################################

// Convert string to camelCase
function toCamelCase(str) {
  return str
    .replace(/(?:^\w|[A-Z]|\b\w|\s+|[-_])/g, (match, index) =>
      index === 0 ? match.toLowerCase() : match.toUpperCase()
    )
    .replace(/[\s-_]+/g, '');
}

// Format tags
function formatTags(pclass, race) {
  return [
    pClass && ` - class/${toCamelCase(pClass)}`,
    race && ` - race/${toCamelCase(race)}`
  ]
  .filter(tag => tag)
  .join('\n');
}

// Return icon based on class
function getIcon(pClass) {
  const iconMappings = {
    Artificer: ':RiToolsFill: Specialist',
    Barbarian: ':FasCity: Primal Path',
    Bard: ':FasGuitar: College',
    Cleric: ':FasPersonPraying: Divine Domain',
    Druid: ':FasMoon: Circle',
    Fighter: ':FasUserShield: Archetype',
    Monk: ':FasHandFist: Tradition',
    Paladin: ':FasFireFlameCurved: Oath',
    Ranger: ':FasBullseye: Conclave',
    Rogue: ':RiSwordFill: Archetype',
    Sorcerer: ':FasHandSparkles: Origin',
    Warlock: ':FasBurst: Patron',
    Wizard: ':FasWandMagicSparkles: Tradition'
  };

  return iconMappings[pClass] || ':FasCircleQuestion: Sub Class';
}

// ###########################################################
//                         Main Code
// ###########################################################

// Call modal form & declare variables
const result = await MF.openForm('PC');
const quote = result.Quote.value;
const level = result.Level.value;
const pClass = result.pClass.value;
const subClass = result.subClass.value;
const subType = getIcon(pClass);
const name = result.Name.value;
const race = result.Race.value;
const tags = formatTags(pClass, race);

if (result.status === 'ok') {

    // Rename file & open in new tab; Fire toast notification
    await tp.file.rename(name);
    await app.workspace.getLeaf(true).openFile(tp.file.find_tfile(name));
    new Notice().noticeEl.innerHTML = `<span style="color: green; font-weight: bold;">Finished!</span><br>New player character <span style="text-decoration: underline;">${name}</span> added`;

    // Refresh the tab because dataview inline doesn't load initially
    const leaves = this.app.workspace.getLeavesOfType('markdown');
    for (const leaf of leaves) {
        if (leaf.view.file.basename === `${name}`) {
            const tab = app.workspace.getLeafById(leaf.id);
            const blank = this.app.vault.getAbstractFileByPath('Assets/Templates/REFRESH.md');
            const file = this.app.vault.getAbstractFileByPath(`Compendium/Party/Player Characters/${name}.md`);
            setTimeout(async () => {
                await tab.openFile(blank, { active: false });
                await tab.openFile(file, { active: false });
            }, 50);
        }
    }


} else {

    // Fire toast notification & exit templater
    new Notice().noticeEl.innerHTML = `<span style="color: red; font-weight: bold;">Cancelled:</span><br>Player character has not been added`;
    return;
}
_%>
---
type: pc
tags:
<% tags ? tags : ' - ' %>
headerLink: "[[<% name %>#<% name %>]]"
level: "<% level ? level : '' %>"
race: "<% race ? race : '' %>"
class: "<% pClass ? pClass : '' %>"
subClass: "<% subClass ? subClass : '' %>"
groupe: "<% groupe ? groupe : '' %>"
cover: "/Assets/Images/Party/Portrait.jpg"
---

###### <% name %>
:FasPerson: Personnage Joueur &nbsp; | &nbsp; :FasQuoteLeft: <% quote ? quote : 'Quote or tagline here' %> :FasQuoteRight:
___
> [!infobox|no-t right]
> ![[portrait.jpg]]
> ###### Details:
> | Type | Stat |
> | ---- | ---- |
> | :FasCrown: Niveau   | `=this.level` |
> | :RiSwordFill: Classe |  `=this.class`|
> | <% subType %> |  `=this.subClass`|
> |  :FasUserGroup: Race |  `=this.race`|
> |  :LiSwords: Groupe |  `=this.groupe`|

> [!quote|no-t]
> Description de Personnage Ici
 
#### marker
> [!column|flex 3]
>> [!info]- QUÊTES/STORYLINES:
>>```dataview
>>LIST WITHOUT ID headerLink
>>FROM "Compendium/Party/Quests" AND [[<% name %>]]
>>SORT file.ctime DESC
>
>>[!note]- HISTOIRE
>>```dataview
>>LIST WITHOUT ID headerLink
>>FROM "Session Notes" AND [[<% name %>]]
>>SORT file.ctime DESC
>
>>[!hint]- Relations (PNJ)
>>```dataview
>>LIST WITHOUT ID headerLink
>>FROM "Compendium/NPC's" AND [[<% name %>]]
>>SORT file.ctime DESC
>>
```image-layout-masonry-3

```
