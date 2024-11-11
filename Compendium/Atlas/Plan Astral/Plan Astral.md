---
type: plane
tags:
 - 
headerLink: "[[Plan Astral#Plan Astral]]"
---
![[banner.jpg|banner]]
###### Plan Astral
<span class="sub2">:FasCircleHalfStroke:  Plan d'Existence</span>
___

> [!quote|no-t] RÉSUMÉ
>C'est l'espace qui sépare tout, la route qui mène partout, le lieu où l'on se trouve lorsque l'on n'est nulle part ailleurs. Le plan astral est l'espace qui sépare les plans. Lorsqu'un personnage franchit un portail interplanaire ou projette son esprit dans un plan d'existence différent, alors il voyage à travers le plan astral. Même les sorts permettant un mouvement instantané à travers un plan, comme _porte dimensionnelle_, touchent brièvement au plan astral. Le plan astral est une formidable sphère infinie de ciel clair et argenté, s'ouvrant aussi bien en haut qu'en bas. De larges nuages en forme de tubes ondulent paresseusement au loin, certains rappelant ceux d'un orage et d'autres des tornades immobiles de vents gris. Des tourbillons de couleur erratiques dansent à mi-hauteur, tels des pièces de monnaie tournoyantes. On aperçoit à l'occasion quelque morceau de matière solide, mais la majorité du plan astral est un lieu ouvert et infini. Ses principaux habitants sont les [githyankis](https://www.aidedd.org/dnd/monstres.php?vf=githyanki-guerrier), une race de proscrits faisant leurs proies des voyageurs passant par le plan.

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
FROM "Compendium/Atlas/Plan Astral"
WHERE type= "realm"
SORT file.name ASC
>
>> [!note]- HISTOIRE
>>```dataview
LIST WITHOUT ID headerLink
FROM "Session Notes" AND [[Plan Astral]]
SORT file.ctime DESC