---
type: realm
locations:
  - "[[Plan Matériel]]"
tags:
  - 
headerLink: "[[Gisombre#Gisombre]]"
---

![[5e_DMG_Shadowfell.png|banner+tall]]
###### Gisombre
<span class="sub2">:RiGlobalLine: Realm (world)</span>
___

> [!quote|no-t] RÉSUMÉ
>La Gisombre est l'écho ténébreux du monde des mortels, un lieu de ténèbres impénétrables aux paysages familiers et pourtant différents, qui offre des décors à couper le souffle et des visions à faire perdre l'esprit, un domaine crépusculaire qui est comme « l'envers » du monde et de ses habitants. La légende raconte qu'une obscurité surnaturelle grandit autour des vestiges de la matière brute qui servit à la création. Avec le temps, cette obscurité s'aggloméra pour prendre une forme similaire à celle du monde physique, mais plus sombre et lugubre, vibrant d'un pouvoir étrange et inattendu. Cette terre obscure engendra ses propres enfants et attira d'autres êtres des différentes régions du cosmos. Elle finit par être habitée par une population de créatures diverses, certaines bienveillantes, d'autres malveillantes. La Gisombre est plus qu'un simple reflet obscur et déformé. Ce plan est la destination des âmes libérées de leur corps, le domaine des défunts, l'ultime étape des âmes avant leur voyage vers l'inconnu. C'est pour cela que la Gisombre attire l'attention de tous ceux qui s'intéressent à la mort. C'est un plan parallèle aux dimensions et à la topographie semblables au monde des mortels.
>
>La [[Féerie]] rappelle au voyageur le monde des mortels, avec une exagération de la luxuriance végétale. La Gisombre est pareillement évocatrice du monde des mortels, mais le reflet qu'elle en propose est bien différent. Les paysages, les êtres et les lieux familiers sont transformés, comme s'ils surgissaient de cauchemars à demi oubliés ou avaient été pervertis par la peur et le doute. Les dangers sont nombreux en Gisombre : dragons d'ombre, morts-vivants, manteleurs, mantes obscures. Pourtant l'attrait de trésors perdus, de mystères étranges (notamment ceux de la mort) et de visions irréelles attirent les audacieux ou les insensés qui viennent éprouver leur courage en affrontant les forces des ténèbres qui gouvernent ce plan lugubre. En fait, pour beaucoup de visiteurs de Gisombre, ce plan a plus de points communs avec le monde physique qu'il n'a de différences, ce qui est à la fois réconfortant et troublant.

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
FROM "Compendium/Atlas/Plan Matériel/Gisombre"
WHERE type= "continent" OR type="ocean"
SORT file.name ASC
>
>> [!note]- HISTOIRE
>>```dataview
LIST WITHOUT ID headerLink
FROM "Session Notes" AND [[Gisombre]]
SORT file.ctime DESC