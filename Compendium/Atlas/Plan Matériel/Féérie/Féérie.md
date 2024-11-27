---
type: realm
locations:
  - "[[Plan Matériel]]"
tags:
  - 
headerLink: "[[Féérie#Féérie]]"
---

![[feywild.webp|banner+tall]]
###### Féérie
<span class="sub2">:RiGlobalLine: Realm (world)</span>
___

> [!quote|no-t] SUMMARY
>La Féerie (parfois aussi connue sous le nom de plan des Fées) est le double verdoyant et sauvage du monde des mortels. De vertigineuses forêts s'y étalent sur des milliers de lieues. Des prairies ambrées parfaites et vallonnées séparent des montagnes dont les pics enneigés disparaissent dans les nuages. Des mers vert émeraude, turquoise et jade déferlent sur des plages sans fin. Le bleu pur du ciel, inconnu du monde matériel, abrite des orages dont la masse nuageuse noire comme le charbon bouillonne sous l'effet de vents violents et de pluies torrentielles. Ici, l'énergie arcanique vrombit dans le moindre arbre, le moindre caillou. Toute existence est magique. La Féerie est un plan parallèle aux dimensions et à la topographie semblables au monde des mortels découpée en domaine, chacun d'eux sous le contrôle d'un archifée.  
>
>Les créatures originaires de la Féerie, tels les dangereuses [guenaudes](https://www.aidedd.org/dnd/monstres.php?vf=guenaude-verte) et les farouches [dryades](https://www.aidedd.org/dnd/monstres.php?vf=dryade), sont chargées de l'énergie mystique de ce plan. Mais si elle est une bénédiction pour certains, elle en pervertit d'autres. Tout comme leur environnement, les créatures féeriques qui résident sur ce plan tendent à se placer dans les extrêmes. Celles qui sont bonnes, nobles et justes protègent le monde naturel et les mortels auxquels elles choisissent d'accorder leur faveur. Celles qui sont mauvaises incarnent le déchaînement de l'instinct le plus primaire sous le signe du sang, des griffes et de la colère. Les créatures de Féerie peuvent être avenantes, cruelles, nobles, monstrueuses et féroces, et souvent tout cela à la fois. On y trouve des elfes, des satyres, des pixies, des feux follets, mais aussi des chiens esquiveurs, des dragons féeriques, des sylvaniens, des licornes, ainsi que des gobelins, des ogres et des géants.

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
FROM "Compendium/Atlas/Plan Matériel/Féérie"
WHERE type= "continent" OR type="ocean"
SORT file.name ASC
>
>> [!note]- HISTOIRE
>>```dataview
LIST WITHOUT ID headerLink
FROM "Session Notes" AND [[Féérie]]
SORT file.ctime DESC