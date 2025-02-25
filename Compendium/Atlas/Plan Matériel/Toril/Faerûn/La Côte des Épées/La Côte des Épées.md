---
type: region
locations:
  - "[[Faerûn]]"
tags:
  - location/generalRegion
headerLink: "[[La Côte des Épées#The Sword Coast]]"
---

![[swordCoast.jpg|banner+tall]]
###### La Côte des Épées
<span class="sub2">:FasMap: General Region</span>
___

> [!quote|no-t] SUMMARY
>La **Côte des Épées** est une côte rocheuse qui tire son nom des falaises blanches et tranchantes,les **Dents de l'Épée**.Celles-ci s'élèvent le long du rivage, séparant la mer à l'ouest, et la terre à l'est. Les falaises peuvent atteindre près de huit cents mètres de haut. Il n'y a presque aucun point d'ancrage praticable pour les navires le long de cette côte et les ports y sont rares et épars.

#### marker
> [!column|flex 3]
> > [!hint]-  NPC's
> > <input type="checkbox" id="npc"/><ul class="sortMenu"><li class="sortIcon">:RiListSettingsLine:<ul class="dropdown npcedit"><li><label for="npc" class="directLabel active">Direct Links Only</label></li><li><label for="npc" class="childLabel">Include Sub-Locations</label></li></ul></li></ul>
> >```dataviewjs
dv.container.className += ' npcDirect';
dv.list(dv.pages('"Compendium/NPC\'s"')
 .where(p => p.file.outlinks.includes(dv.current().file.link))
.sort(p => p.file.link)
.map(p => p.headerLink), 1);
>>```
>>```dataviewjs
dv.container.className += ' npcChild';
let page = dv.current().file.path;
let pages = new Set();
let stack = [page];
while (stack.length > 0) {
let elem = stack.pop();
let meta = dv.page(elem);
if (!meta) continue;
for (let inlink of meta.file.inlinks.concat(meta.file.outlinks).array()) {
let locations = dv.page(inlink.path);
if (!locations || pages.has(inlink.path) || inlink.path === meta.locations?.[0]) continue;
 if (dv.array(locations.locations).join(", ").includes(meta.file.path)) {
 pages.add(inlink.path);
 stack.push(inlink.path);
}}}
let data = Array.from(pages)
.filter(p => dv.page(p)?.type === "npc")
.map(p => dv.page(p).headerLink)
.sort((a, b) => {
if (a < b) return -1;
if (a > b) return 1;
return 0;
});
dv.list(data);
> 
>> [!example]- LOCATIONS
>>```dataview
LIST WITHOUT ID headerLink
FROM "Compendium/Atlas/Plan Matériel/Toril/Faerûn/La Côte des Épées"
WHERE type= "locale"
SORT file.name ASC
>
>> [!note]- HISTORY
>>```dataview
LIST WITHOUT ID headerLink
FROM "Session Notes" AND [[La Côte des Épées]]
SORT file.ctime DESC
#### marker