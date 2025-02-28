---
type: plane
tags: 
headerLink: "[[Plan Matériel#Material Plane]]"
---

![[materialPlane.avif|banner+tall]]
###### Plan Matériel
<span class="sub2">:FasCircleHalfStroke: Plan d'Existence</span>
___

> [!quote|no-t] SUMMARY
>The Material plane (also seen as Prime Material Plane) is the plane in which Toril and the surrounding cosmos exist. The phrase "Prime Material plane," or simply the "Prime," is generally used by beings from other planes in the multiverse to refer to the inhabitants of the Material Plane.

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
>> [!example]- LIEUX
>>```dataview
LIST WITHOUT ID headerLink
FROM "Compendium/Atlas/Plan Matériel"
WHERE type= "realm"
SORT file.name ASC
>
>> [!note]- HISTOIRE
>>```dataview
LIST WITHOUT ID headerLink
FROM "Session Notes" AND [[Plan Matériel]]
SORT file.ctime DESC