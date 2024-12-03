---
type: region
locations:
 - "[[Faerûn]]"
tags:
 - location/generalRegion
headerLink: "[[Mer des Étoiles déchues#Mer des Étoiles déchues]]"
---

![[banner.jpg|banner+tall]]
###### Mer des Étoiles déchues
<span class="sub2">:FasMap: General Region</span>
___

> [!quote|no-t] SOMMAIRE
>La Mer des Étoiles déchues est la plus grande mer intérieure de [[Faerûn]]. Elle relie les parties orientales et occidentales du continent et fut la première route d'immigration qu'utilisèrent les humains de Chondath pour quitter le Bief de Vilhon puis coloniser le centre et le nord de Faerûn. Elle est le domaine privilégié des navires et compagnies marchandes de l'ensemble du nord et de l'est de Faerûn. Les royaumes sous-marins de la Mer des Étoiles déchues sont collectivement désignés par leurs habitants sous le nom de [[Serôs]].

#### marker
> [!column|flex 3]
> > [!hint]-  PNJs
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
>> [!example]- LIEUX
>>```dataview
LIST WITHOUT ID headerLink
FROM "Compendium/Atlas/Plan Matériel/Toril/Faerûn/Mer des Étoiles déchues"
WHERE type= "locale"
SORT file.name ASC
>
>> [!note]- HISTOIRE
>>```dataview
LIST WITHOUT ID headerLink
FROM "Session Notes" AND [[Mer des Étoiles déchues]]
SORT file.ctime DESC
#### marker