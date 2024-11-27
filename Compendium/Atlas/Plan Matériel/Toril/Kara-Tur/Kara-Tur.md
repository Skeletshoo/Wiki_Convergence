---
type: continent
locations:
 - "[[Toril]]"
tags:
 - 
headerLink: "[[Kara-Tur#Kara-Tur]]"
---

![[KaraTur.jpg]]
###### Kara-Tur
<span class="sub2">:FasEarthAmericas: Continent</span>
___

> [!quote|no-t]
>Kara-Tur est un des continents de [[Toril#Toril]], situé à l'est de [[Faerûn]] et de [[Zakhara]]. C'est un merveilleux territoire de légende constitué de montagnes aussi hautes que le ciel, d'impénétrables jungles et de vastes prairies inhabitées, parcourues par de féroces tribus séparent des empires tentaculaires. Kara-Tur est réputé pour sa soie, ses épices et son or, ainsi que pour ses cruels seigneurs de guerre.

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
FROM "Compendium/Atlas/Plan Matériel/Toril/Kara-Tur"
WHERE type= "region"
SORT file.name ASC
>
>> [!note]- HISTOIRE
>>```dataview
LIST WITHOUT ID headerLink
FROM "Session Notes" AND [[Kara-Tur]]
SORT file.ctime DESC
#### marker