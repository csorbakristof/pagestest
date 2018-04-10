---
parent: forstudents.md
menu: Concrete section analysis
---

(This page is meant for hungarian students, that is why it is in Hungarian.)

# Beton minták struktúrális elemzése

Ide azok a témák tartoznak, melyek egy a cv4s keretrendszerre épülő új alkalmazás formájában beton minták elemzését célozzák. Az összetétellel és porozitással kapcsolatos kiértékelések egyik célja a Paks 2 atomerőmű építkezéshez használt beton összetétel kiválasztása.

* TOC
{:toc}

* ![]({{ site.baseurl }}/assets/video.png){: .vertical-center-image } [cv4s Concrete projekt demó](https://youtu.be/yMM0VqbP_LM)

## Kavicsok és pórusok azonosítása

A beton belső struktúrájának elemzésekor elsődleges célunk az alábbiak azonosítása:

  * Pórusok, melyeken át az átmérőtől függően a víz beszivárog a beton belsejébe és csökkenti a fagyállóságot.
  * Légbuborékok, melyek javítják a fagyállóságot azzal, hogy megszakítják a szűk pórusokat.
  * Kavicsok, melyek változatos színűek és még ha van is bennük szín alapján pórusnak azonosítható pont, az nem számít pórusnak.
  * Speciális adalékok, melyek növelik például a gamma sugárzás elnyelő képességet, ezért fontos a mennyiségük és hogy a beton kötése közben egyenletes maradt-e a térbeli eloszlásuk (vagy például leülepedtek az aljára a nehéz szemcsék).

A pórusokat és légbuborékokat úgy lehet azonosítani, hogy a beton mintát gyantába áztatják a csiszolás előtt, és így jellegzetes színűek lesznek azok a helyek, ahova a gyanta be tudott szivárogni. Az alábbi csiszolat képen a keresett pórusok zöldes gyantával vannak kitöltve. (A képek forrása: Nehme Salem, BME)

![Beton csiszolat és a pórusok]({{ site.baseurl }}/assets/concrete_merged.png){: .center-image }

A feladat az ilyen képek feldolgozásának minél jobb automatizálása. Viszont a megfelelő minőség és a felhasználók bizalma érdekében fontos, hogy lehetőséget adjunk az ellenőrzésre és szükség esetén a beavatkozásra, vagyis például a megtalált pórusok törlésére, átrajzolására. A cv4s keretrendszer az ilyen módosításokkal kapcsolatos műveletek nagy részét már támogatja, de további specializált műveletekre is szükség lesz.

> Amiket tanulhatsz vele:
>
>  * Képfeldolgozási alapok OpenCV segítségével, C# környezetben
>  * Median szűrő, Canny edge detector, watershed (vagy más, pl. MSER) szegmentációs algoritmus használata
>  * Érdekességek az építőanyagok világából

## Ergonómikus felhasználói felület tervezése a beton csiszolati képek elemzéséhez

Mivel ebben az alkalmazásban igen fontos, hogy a műveletek kézre essenek és könnyű legyen a munka, gondosan meg kell terveznünk a felhasználói felületet és az azon elérhető műveleteket. Ilyen műveletek többek között az alábbiak:

  * Pici pórusok (foltok) kiválasztása és törlése: az egérrel akkor is ki lehessen jelölni egy kis foltot, ha nincsen pont rajta az egérkurzor. Vagyis bizonyos távolság alatt az egérhez legközelebbi folt már kijelölődjön.
  * Mivel gyakran kell felváltva nézni a foltokat és az eredeti képeket, hasznos lehet egy olyan billentyű (pl. a Shift), amit nyomva tartva eltűnnek a foltok és csak az eredeti kép látszik, a billentyűt felengedve pedig újra megjelennek. Így gyorsan lehet egymáson "villogtatni" a két nézetet.

> Amiket tanulhatsz vele:
>
>  * Képfeldolgozási műveletek integrálása felhasználói felületbe.
>  * A WPF összetettebb eseménykezelő mechanizmusai, esetleg animációs képességei

## Monte Carlo alapú képszegmentációs módszerek vizsgálata beton csiszolatok elemzésére

A beton csiszolatokban az egyes szétválasztandó részek színe és textúrája jelentősen eltér. Az egyik fő irány a szegmentációra a foltok határának megkeresése, amit azonban a textúra meg tud nehezíteni. Egy másik megoldás az, ha a képet sokkal több kis részre felosztjuk és ezeket a kis területeket vonogatjuk össze, ha azok nagyon hasonlítanak egymásra. Itt a hasonlóságba könnyebb belevenni a textúra hasonlóságát, pl. a szín hisztogram vizsgálatával.

Ennek a megközelítésnek az egyik matematikai módszere a véletlen sorsolásokon alapuló Monte Carlo módszerek csoportja, melyek egyszerre mindig csak egy terület páros összevonásáról vagy szétválasztásáról döntenek. A döntésnél pedig a sorsolási valószínűség attól függ, hogy mennyivel lesz "jobb a helyzet", ha megtörténik a művelet. Ilyenkor még akár azt is figyelembe lehet venni, hogy a kialakuló szemcse alakja konvex lesz-e a művelet hatására. Ha nagyon nem, akkor az egy kicsit gyanús például a kavicsok esetében.

> Amiket tanulhatsz vele:
>
>  * Monte carlo alapú optimalizáló algoritmusok használata (ami nem is olyan nehéz, mint elsőre gondolnád)
>  * Képfeldolgozási, szegmentációs és szűrési módszerek megismerése.
