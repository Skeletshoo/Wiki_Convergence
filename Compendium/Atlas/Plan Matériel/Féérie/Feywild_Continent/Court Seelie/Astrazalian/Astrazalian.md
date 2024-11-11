---
type: locale
locations:
 - "[[Court Seelie]]"
tags:
 - location/city
headerLink: "[[Astrazalian#Astrazalian]]"
---

![[banner.jpg|banner]]
###### Astrazalian, Cité des Étoiles
<span class="sub2">:FasCity: City</span>
___

> [!quote|no-t] RÉSUMÉ
>La ville d'Astrazalian, la Cité des Etoiles- la plus grosse ville éladrine en Féérie gouvernée par [[Dame Shandria]], la nièce de [[Titania]] qui était aventurière aussi à la base. Ca peut être intéressant parce que non seulement c'est la plus grosse ville exportatrice de biens de tout le plan mais aussi parce que la moitié de l'année la ville est sur le plan matériel donc on a une chance sur deux de pouvoir les trouver facilement.

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
const page = dv.current().file.path;
const pages = new Set();
const stack = [page];
while (stack.length > 0) {
const elem = stack.pop();
const meta = dv.page(elem);
if (!meta) continue;
for (const inlink of meta.file.inlinks.concat(meta.file.outlinks).array()) {
const locations = dv.page(inlink.path);
if (!locations || pages.has(inlink.path) || inlink.path === meta.locations?.[0]) continue;
 if (dv.array(locations.locations).join(", ").includes(meta.file.path)) {
 pages.add(inlink.path);
 stack.push(inlink.path);
}}}
const data = Array.from(pages)
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
FROM "Compendium/Atlas/Plan Matériel/Féérie/Feywild_Continent/Court Seelie/Astrazalian"
WHERE type= "landmark"
SORT file.name ASC
>
>> [!note]- HISTOIRE
>>```dataview
LIST WITHOUT ID headerLink
FROM "Session Notes" AND [[Astrazalian]]
SORT file.ctime DESC