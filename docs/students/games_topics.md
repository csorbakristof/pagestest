---
parent: forstudents.md
menu: Games
---

(This page is meant for hungarian students, that is why it is in Hungarian.)

# Játékfejlesztés cv4s alapokon

Bár eredetileg nem erre készült, a cv4s keretrendszer kiválóan alkalmas táblás stratégiai játékok fejlesztésére is, mivel a cimkézett polygonok a játéktér mezőiként is használhatók.

A belső adatreprezentáció címkézett polygonokat tárol, ahol a megjelenést (pl. szín) a polygonon lévő címkék halmaza határozza meg. A szerver oldalt kiegészítve (amivel REST alapon kommunikál a cv4sensorhub) érdekes mezőszínezgetős, vagy esetleg polygonok módosításán alapuló játékokat is lehet készíteni. A téma célja egy ilyen játék kitalálása és implementálása. (A szerver oldal miatt nincs akadálya több klienssel multiplayer játéknak sem, ráadásul a projekt keretében nem csak WPF alapú, hanem HTML5 alapú megjelenítő és szerkesztő kliens is készül, vagyis ha a játék elkészül, az HTML5 alól is játszható lesz, amint az a kliens is elkészül.

Jelenleg ilyen alkalmazás még nincsen, ez egy teljesen új irány.

* TOC
{:toc}

## Területfoglalós játék fejlesztése

A cv4s adatmodell polygonjaiból játékteret összeállítva a polygonok címkéivel tudjuk jelezni egyrészt a mező típusát, másrészt tartalmát. Színek, bábúk, különböző harci egységek stb. ábrázolása így könnyen megoldható. A megjelenítési alrendszer pedig képes arra, hogy a címkék tartalma alapján piktogrammokat jelenítsen meg a polygonok felett.

Jelenlegi formájában a keretrendszer még biztosan nem tud mindent, ami egy játékhoz kell, de ezeket elkészítve változatos, akár multiplayer játékok készítésére is lehetőség nyílik. A feladat tehát egy játék kiválasztása/kitalálása, majd a szükséges kiegészítő funkciók elkészítése hozzá. Emellett természetesen ha valakinek van kedve hozzá, mesterséges intelligencia játékost is lehet készíteni, amit aztán tetszőleges ideig lehet okosítgatni.

> Amiket tanulhatsz vele:
>
>   * A cv4s adat- és műveletmodell felhasználása egy játék megvalósítására.
>   * WPF trükkök MVVM architektúrában
>   * Amennyiben MI játékos is készül, ennek keretében meg lehet ismerkedni tanuló algoritmusokkal, neurális háló alkalmazásokkal, döntéselmélettel stb.

## Infrastruktúra, kapacitás és építés

Ennek a feladatnak nem titkolt célja, hogy felmérje, későbbi esetleges ipari projektek esetében mennyire alkalmas a cv4s keretrendszer olyan feladatok megoldására, ahol például csővezeték vagy elektromos hálózatokat kell felügyelni, irányítani, kapacitások és terheléseket ellenőrizni.

Mindezt első körben játékos formában, például egy olyan játék keretében, ahol csöveken kell folyadékokat átjuttatni az ellenség által okozott hibák ellenére, szelepeket lehet kapcsolgatni, szivattyúkat vezérelni, javításokat végrehajtani. (De akár kis szabályozástechnikát is bele lehet csempészni, ha van kedvetek.)

> Amiket tanulhatsz vele:
>
>   * A cv4s adat- és műveletmodell felhasználása egy játék megvalósítására.
>   * WPF trükkök MVVM architektúrában
>   * Amennyiben komolyabb fizikai szimuláció vagy szabályozástechnika is kerül a feladatba, annak elméleti hátterét is egy konkrét alkalmazáson keresztül lehet megismerni.

## Árvíz és elöntés szimuláció

Ennek a témának is az a célja, hogy a cv4s geoinformatikai alkalmazhatóságát mérje fel esetleges későbbi ipari projektek számára. Amennyiben a cv4s adatmodell polygonjaiból térképet készítünk és a kapcsolódó kulcs-érték párokkal leírjuk minden területen a tengerszint feletti magasságot, aktuális vízszintet, esetleg áramlási irányt, akkor ebből könnyedén lehet készíteni egy olyan játékot, ahol gátakat lehet építeni, árkokat ásni stb., majd jön a víz és minél több területet meg kell védeni. Még akkor is, ha a kalózhajó és az édesvizi bálna is megjelenik.

Később könnyen elképzelhető olyan ipari alkalmazás, ahol a fenti adatok (kivéve a kalózok és a bálna) szenzorhálózatból vagy távérzékelési eszközökből (műhold, drone) érkeznek. Köztes megoldásként akár a tanszéken fejlesztett droneok vezérlését is össze lehet kapcsolni ezzel a "játékkal", ha a polygonok által megadott térkép már nem teljesen fiktív, hanem például az egyetem környékét ábrázolja.

> Amiket tanulhatsz vele:
>
>   * A cv4s adat- és műveletmodell felhasználása egy egyszerűbb fizikai szimuláció elkészítésére.
>   * WPF trükkök MVVM architektúrában
>   * Fizikai folyamatok egyszerű szimulációjának felhasználása egy játékprogram kialakítására
>   * Ha van kedved játéktérnek berántani az OpenStreetMaps egy részét, annak világával is megismerkedhetsz.


## Egy példa screenshot

Az alábbi screenshot nem egy feladat, hanem egy kis betekintést enged abba, hogy a keretrendszer hogyan tudna játékokat megjeleníteni. Texttúrázott polygonok, rajtuk piktogrammok és háttérképek mind szerepelnek a keretrendszerben. A végleges alkalmazások felhasználói felülete felhasználja a keretrendszer megjelenítő funkcióit, de tetszőlegesen ki tudja azokat egészíteni vagy el tudja fedni azokat.

![cv4s példa screenshot]({{ site.baseurl }}/assets/jatek_demo_abra.png){:.center-image}
