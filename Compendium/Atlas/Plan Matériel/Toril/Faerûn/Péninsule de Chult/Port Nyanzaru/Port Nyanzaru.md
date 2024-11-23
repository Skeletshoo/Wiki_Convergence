---
type: locale
locations:
 - "[[Péninsule de Chult]]"
tags:
 - location/city
headerLink: "[[Port Nyanzaru#Port Nyanzaru]]"
---

![[Nyanzaru.webp|banner]]
###### Port Nyanzaru
<span class="sub2">:FasCity: City</span>
___

> [!quote|no-t] RÉSUMÉ
>Port Nyanzaru est le principal centre du commerce de la [[Péninsule de Chult]]. Vers la fin du XVe siècle CV, elle en est la dernière cité humaine connue. [[Le Jour de la Convergence]], la cité a subi une attaque des Hérauts d'Hier qui aurait été repoussée par [[Suleiman Al-Ghazi]] et son équipage.

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
FROM "Compendium/Atlas/Plan Matériel/Toril/Faerûn/Péninsule de Chult/Port Nyanzaru"
WHERE type= "landmark"
SORT file.name ASC
>
>> [!note]- HISTOIRE
>>```dataview
LIST WITHOUT ID headerLink
FROM "Session Notes" AND [[Port Nyanzaru]]
SORT file.ctime DESC