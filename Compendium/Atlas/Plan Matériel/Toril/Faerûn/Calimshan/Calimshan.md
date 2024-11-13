---
type: region
locations:
 - "[[Faerûn]]"
tags:
 - location/country
headerLink: "[[Elturgard#Elturgard]]"
---

![[calimshan.png#calimshan]]
###### Calimshan
<span class="sub2">:FasFlag: Country</span>
___

> [!quote|no-t] SOMMAIRE
>Le **Calimshan**, pays obsédé par la richesse et que la magie n'impressionne pas, fut fondé à l'origine par des génies. Il s'agit d'un pays réputé pour son chauvinisme, ses marchés exotiques, ses guildes de voleurs, ses harems décadents, ses paysages désertiques et sa riche classe dirigeante, ainsi que pour son énorme population et ses nombreux esclaves. Le pays connut dernièrement une brève période de domination genasi, achevée dans le sang lorsque les humains se révoltèrent..

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
FROM "Compendium/Atlas/Plan Matériel/Toril/Faerûn/Elturgard"
WHERE type= "locale"
SORT file.name ASC
>
>> [!note]- HISTOIRE
>>```dataview
LIST WITHOUT ID headerLink
FROM "Session Notes" AND [[Elturgard]]
SORT file.ctime DESC
#### marker