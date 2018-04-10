---
parent: forstudents.md
menu: Asphalt fracture analysis
---

# Aszfalt (útburkolat) fényképek kiértékelése

Ide azok a témák tartoznak, melyek egy a cv4s keretrendszerre épülő új alkalmazás formájában útburkolati hibák keresését és osztályozását célozzák. A cél az úthálózat állapotának minél teljesebb felmérése, mely a bemeneti anyag mennyisége miatt csak automatizált eszközökkel lehetséges.

* TOC
{:toc}

## Útburkolati repedések azonosítása

Az alábbi képen egy a Q épület előtt lévő útburkolat részlet látszik a jobb szélen. Középen az Adaptive Double Threshold Segmentation eredménye, mint gyors kísérlet, bal szélen pedig az azonosított polygonok, valamint a repedés részletei egyelőre kézzel kijelölve.

![Útburkolat fénykép és az Adaptive Double Threshold Segmentation eredménye. Block size 101, Loose C -1. Strict C -10.]({{ site.baseurl }}/assets/aszfalt_adts.png){: .center-image }

A feladat az ilyen képek feldolgozásának minél jobb automatizálása. A megoldásra váró részfeladataink:
  * Küszöbszintek minél automatikusabb beállítása a fényviszonyoknak és a kép jellemzőinek megfelelően. (Például nem mindig lesz a repedés a világosabb.)
  * További képszegmentációs eljárások kipróbálása, hátha azok szebb eredményeket adnak.
  * A repedések részleteinek megkülönböztetése a többi zajtól. Első körben a kapott összefüggő polygonok méretét, valamint a kisebbek esetében a hosszúkásságukat érdemes vizsgálni. Ha minden pixelhez feljegyezzük a rajta átmenő leghosszabb, polygonon belüli egyenes szakasz hosszát, az alapján ki lehet szűrni ezeket a foltokat?

> Amiket tanulhatsz vele:
>
>  * Képfeldolgozási alapok OpenCV segítségével, C# környezetben
>  * Thresholding módszerek felhasználása, küszöbszintek automatikus, például hisztogram alapú meghatározása.
>  * Háttér eltávolítási módszerek (például nagyobb blokkméretre számolt átlagos színtől való eltérés).
>  * Pixel szintű kiértékelések, polygonon belüli távolságok mérése, egyéb statisztikák kinyerése

## A repedések osztályozása

Az útburkolati hibákat irányuk és formájuk alapján tipikus hiba kategóriákba lehet sorolni. Mintafelismerési, osztályozási módszerekkel további cél a repedések megfelelő kategóriákba sorolása.

> Amiket tanulhatsz vele:
>
>  * OpenCV Machine Learning moduljának használata
>  * Az osztályozás alapját képező tulajdonságok kinyerése, meghatározása (feature extraction).
>  * Osztályozási módszerek

## További várható feladatok

További feladatok, amikre már most látjuk az igényt:
  * Képsorozatok összeillesztése: a fentieken kívül előbb-utóbb ezeket a képeket egy mozgó járműről fogjuk készíteni, így a sok képet egymás mögé kell majd illeszteni és az útszakasz teljes hosszában kell majd kiértékelni. Ez alapvetően képillesztési feladat kamera torzítás kompenzációval, eléggé ismétlődő mintázatú képeken.
  * Termikus infra kamera használata: egy kísérletet mindenképpen megér, hogy hőkamera képen a repedések mennyire látszanak. Ha hőmérséklet alapján könnyebb őket azonosítani (nem feltétlenül kell nagyon pontosan körberajzolni őket), akkor megéri azt is használni. Akár csak arra is, hogy a normál képek bizonyos részeit eleve kizárjuk a repedés keresésből, ha ott biztosan nincsen rá esély.
  * Egy lapos szögben érkező lézer vonalban a repedések széle által vetett árnyék különbözik valamiben a többi területtől?
  * Érdesség (felszínhibák) mérése
  * Útburkolat minőség ellenőrzéskor készített fúrómag mintáról készült fényképen szemcseösszetétel meghatározása.
  * CT felvétel alapján georadar kalibrációja. A CT a belső sűrűség viszonyokat határozza meg. Ha ez alapján meg tudjuk határozni, hogy a georadar mérési eredményeiből (alapvetően visszaverődési helyek) hogyan lehet a belső hibákat megtalálni, egy könnyen használható, az útburkolatot térfogatában is vizsgáló rendszert tudnánk kifejleszteni.
