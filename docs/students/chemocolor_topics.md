---
parent: forstudents.md
menu: ChemoColor
---

(This page is meant for hungarian students, that is why it is in Hungarian.)

# ChemoColor alkalmazás specifikus témák

Ide tartoznak a csontevő baktérium (osteoclast) fejlődést követő feladathoz kapcsolódó fejlesztések.

A ChemoColor bizonyos részeit más a végfelhasználók is tesztelik, de még mindig sok olyan funkció van, ami csak terv szinten alakulgat. Ebben a témakörben a feljesztés mellett bele lehet kóstolni a megrendelőkkel folytatott kommunikáció, közös ötletelés és a feladat egyeztetés részleteibe is.

A ChemoColor egyik feladata színstatisztikák készítése a képek alapján, a másik pedig az osteoclastok kialakulásához és a területük körberajzolásához kapcsolódik. Ez utóbbira a cv4sensorhub keretrendszer funkciói segítéségvel már most is van lehetőség, de természetesen még bőven van mit automatizálni ezen a területen is.

![]({{ site.baseurl }}/assets/video.png){: .vertical-center-image } [Demó videó osteoclast félautomatikus körberajzolásra](https://youtu.be/e-VF6DXkxzM)

* TOC
{:toc}

## Színstatisztikák képsorozatokból

A ChemoColor háttérben olyan kísérletek állnak, ahol piros és zöld színű sejtek olvadnak össze, az eredmény pedig egy sárga színű sejthalmaz (az osteoclast). A kialakulás követéséhez ezért első sorban a képpontok színéből készített statisztikák vezetnek. Mivel képek sorozatáról van szó, gyakorlatilag egy színhisztogram sorozatot állítunk elő, melyben minél jobban láthatóvá tesszük ennek az átalakulási folyamatnak a részleteit.

![Színes képek osteoclast kialakulásról]({{ site.baseurl }}/assets/chemocolor_oc_color.png){: .center-image }

## Körberajzolás támogatása

A színes képek mellett rendelkezésünkre állnak olyan megfestett képek is, melyeken a sejtek határai sokkal jobban látszanak, a színük viszont a festés miatt nem. Viszont a színes képeken meg a határvonalak nem látszanak tisztán, így a kétféle képet együttesen érdemes használni. A kontúrok mentén körberajzolás minél pontosabb automatizálása fontos cél, mivel igen sok sejthalmazról van szó, így a kézi megoldás lassabb, mint amilyen tempóban az új feldolgozandó képek keletkeznek.

![Színes képek osteoclast kialakulásról]({{ site.baseurl }}/assets/chemocolor_oc_painted.png){: .center-image }

Képfeldolgozási szempontból külön érdekesség, hogy itt két, alapvetően különböző képet is fel tudunk használni: van, amit az egyiken kényelmesebb megtenni, van, amit a másikon. Hogy ez hogyan lesz áttekinthető és kényelmes, az megint csak egy komoly UX (user experience) tervezési feladat.

> Amiket tanulhatsz vele:
>
>   * Képszegmentációs módszerek felhasználása félautomata vagy teljesen automatikus sejt körberajzolásra.
>   * A feladat során sokszor találkozunk azzal a kérdéssel, hogy az új vagy esetleg már jól ismert informatikai megoldásokat hogyan lehet a felhasználók számára is kényelmes formára hozni. Mert attól, hogy például van egy (néha azért pontatlan) kontúrkereső algoritmus implementációnk, attól még a felhasználó sejtet pontosan körberajzoló munkáját nem oldottuk meg. Ki kell találni, mi lesz az algoritmus oldal és az OnMouseMove események között a kapocs.
>   * UX tervezés, a felhasználó számára egy nem triviális, több képen végzett képfeldolgozási folyamat áttekinthetővé tétele.

## Esztétikus kimenetek előállítása

Az eredmény statisztikák meghatározása után azokat prezentációra, tudományos publikációkba helyezésre alkalmas formára kell hozni. Mivel eredményeinkre további munkafázisok is épülnek majd, elsődleges kimenetünk Excel tábla, valamint látványos videók, animációk.

>   * Diagram készítő és összetettebb Excel funkciók elérése .NET környezetből.
>   * Az OpenCV videó generálásra alkalmas funkcióinak megismerése.
>   * Képsorozatok és összetett adatok alapján egy a lehetőségekhez mérten testre szabható tartalmú és esztétikus videó generálásának lehetőségei.
