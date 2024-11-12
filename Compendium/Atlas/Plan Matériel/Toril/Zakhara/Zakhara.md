---
type: continent
locations:
 - "[[Toril]]"
tags:
 - 
headerLink: "[[Zakhara#Zakhara]]"
---

![[Zakhara.jpg|banner]]
###### Zakhara
<span class="sub2">:FasEarthAmericas: Continent</span>
___

> [!quote|no-t]
>Le Zakhara, surnommé les Terres de la destinée, est une terre désertique ponctuée d'oasis luxuriantes et peuplées de puissants génies qui interviennent dans les affaires. Le Zakhara forme une nation unifiée par une intense foi inspirant la piété, le zèle et l'honneur. Mais le continent possède son lot de cités hantées par des démons et d'ensorceleurs impies pratiquant une étrange magie. Les côtes du continent sont infestées de corsaires redoutables qui exigent de lourds tributs et interdisent parfois même la traversée de la Grande Mer où ils opèrent.

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
FROM "Compendium/Atlas/Plan Matériel/Toril/Zakhara"
WHERE type= "region"
SORT file.name ASC
>
>> [!note]- HISTOIRE
>>```dataview
LIST WITHOUT ID headerLink
FROM "Session Notes" AND [[Zakhara]]
SORT file.ctime DESC
#### marker