---
parent: forstudents.md
menu: ChemoTracker
title: ChemoTracker alkalmazás specifikus témák
---

Ide tartoznak a fehérvértest követési feladathoz kapcsolódó fejlesztések. Az alkalmazás céljairól itt található részletesebb leírás: ([ChemoTracker]({{ site.baseurl }}/chemotracker.html))

A ChemoTracker készen áll az első végfelhasználókkal végzett tesztekre, így hamarosan éles külső projekt jelleget ölt a fejlesztése. Ezt azt is jelenti, hogy ezekben a feladatokban a feljesztés mellett bele lehet kóstolni a megrendelőkkel folytatott kommunikáció, közös ötletelés és a feladatok egyeztetés feladataiba.

* ![]({{ site.baseurl }}/assets/video.png){: .vertical-center-image } [Demó videó osteoclast félautomatikus körberajzolásra](https://youtu.be/e-VF6DXkxzM)

* TOC
{:toc}

## Hol vannak a fehérvértestek?

A ChemoTracker egyik legfontosabb feladata a fehérvértestek helyének meghatározása. Ez van, amikor viszonylag egyszerű feladat, de vannak trükkösebb helyzetek is: két felvétel között nem pont ugyanoda áll vissza a robotmikroszkóp, pacák az üvegen, döglött sejtek stb. (A képek forrása: Mócsai Attila, Erdélyi András, Semmelweiss Egyetem)

![Nehezebb esetek]({{ site.baseurl }}/assets/sejtek_crop2.png){: .center-image }

A jelenlegi verzió is több detektor módszert alkalmaz, de még nagyon sok lehetőség van a kísérletezésre és javításra. Szóba jöhetnek fényesség alapú küszöbszintek és alakzat alapú szűrések, mintaillesztés alapú megoldások, neurális hálózatok, képszegmentációs módszerek és még sok más.

> Amiket tanulhatsz vele:
>
>   * Képfeldolgozási módszerek objektum felismerési céllal
>   * Szakterületi ismeretek integrációja, vagyis a képfeldolgozás során olyan ismeretek felhasználása, mely az alkalmazás szakterületéről jön és nem tisztán képfeldolgozással kapcsolatos. (Például a fehérvértestek alakváltozásai, mozgása, "mi ténylegesen sejt és mi nem az"...)

## Interaktív mozgás követés

Ha már tudjuk, hol vannak a sejtek, a következő lépés a mozgások követése, vagyis az egymás utáni képkockák sejtejinek megfeleltetése. Mivel a robotmikroszkóp több mintát fényképez párhuzamosan, kb. 12 másodperc kell neki, amíg körbe ér. Ennyi idő alatt előfordul, hogy egyes sejtek jelentősen nekilódulnak vagy irányt változtatnak, így megtalálásuk a következő képkockán nem triviális. Az egyik lehetőség a sebesség és esetleg lassabb sejtek esetén a gyorsulás becslése és ebből a várható pozíció meghatározása. A végső megfeleltetés egyik módja az, ha az előző és következő képek sejtjei között teljes párosítást keresünk, melyben a páros gráf élsúlyai a megfelelés valószínűségétől függenek.

Külön érdekesség, amikor a felhasználó belejavít a követésbe és ezután újra kell azt futtatni. Ilyenkor ha sikerül megfelelően kihasználni a manuális segítséget, lehet, hogy már egy jóval könnyebb feladatot kapunk. Vagy akár meg is lehet kérni a felhasználót, hogy néhány, a program által kiválasztott sejtet segítsen lekövetni, mert azzal nyerünk a legtöbbet. És természetesen ha sok sejt van, nem is szükséges mindegyiknek a lekövetése, így ha meg tudjuk becsülni, hogy melyikeket tudjuk a legbiztosabban követni, választhatjuk azokat is.

> Amiket tanulhatsz vele:
>
>   * WPF trükkök a kézre eső felhasználói felület érdekében
>   * A mozgáskövetés és megfeleltetés, újrafelismerés módszereinek alkalmazása
>   * Az ergonómia és C# fejlesztés határán olyan eszközök kifejlesztése, melyek a speciális szaktudású, nem informatikus végfelhasználók számára ténylegesen könnyítik a munkát és kézre esnek.

## Látványos kimenetek generálása

A ChemoTracker által támogatott kutatásokban a számszerű eredmények mellett fontos az is, hogy ha vannak eredményeink, minél áttekinthetőbben, előadások esetében minél látványosabban tudjuk prezentálni. Ezért az sem utolsó szempont, hogy a ChemoTracker a követési adatok alapján tud-e szép animációkat generálni, például bejelölve az egyes mozgástípusokat, az aktív sejteket, azok mozgási útvonalait stb.

> Amiket tanulhatsz vele:
>
>   * Statisztikák látványos megjelenítésének eszközei
>   * Animációk automatikus készítése időben változó adatok látványos megjelenítésére
>   * Egy másik szakterület kutatói számára értékes ábrák, animációk megtervezése, az ő szempontjaiknak, céljaiknak és gondolkodási módjuknak a megismerése.
