---
parent: forstudents.md
menu: The framework
title: A keretrendszerrel kapcsolatos témák
---

Ide tartoznak azok a feladatok, melyek magát a keretrendszert okosítják úgy, hogy az első körben még egyik konkrét alkalmazáshoz sem kapcsolódik, de természetesen azok hamarosan profitálni fognak belőlük.

* TOC
{:toc}

## Okosabb polygon műveletek fejlesztése a felhasználó felület számára

Itt következnek olyan eszközök, melyeket a felhasználó közvetlenül tud felhasználni az automatikus módszerek eredményeinek korrigálására, például a határvonalak kézi kijavítására. Fontos, hogy ezek a végfelhasználóknak tényleg praktikusak és kényelmesek legyenek, különben nem fogják őket használni.

### Általános polygon szerkesztési műveletek fejlesztése

Mivel a rendszer alapvetően polygonokban gondolkozik, ezek szerkesztése sok szempontból fontos. Ide tartoznak a szokásos műveletek, mint vertex hozzáadása vagy elvétele, mozgatások, összeolvasztás, metszet képzés és számos egyéb. Ezek az esetek nagy részében egyszerű műveletek, de vannak bőven speciális esetek (például pontosan átfedő vezérlőpontok, egymást éppen érintő szakaszok stb.), amikor hirtelen már nem is olyan triviális a feladat.

Ha például egy vektorgrafikus környezetben akarunk vastag ecsettel rajzolni, az eredményül kapott polygonhoz az egér minden elmozdulásakor össze kell olvasztani az ecset alakját jelképező polygonnal. És ezt ráadásul elég gyorsan kell megtenni, mivel a folyamatos rajzoláshoz másodpercenként igen sok ilyen műveletre szükség lehet.

> Amiket tanulhatsz vele:
>
>   * Polygonokon végezhető műveletek elméletben és gyakorlatban
>   * Polygon műveletek futási idejének vizsgálata, becslése, optimalizálása
>   * A cv4s adatmodell flexibilis használata

### Live polygon

Ha egy képen egy girbe-gurba vonalat akarok bejelölni, ami a képen is ott van, csak sok a zaj és az elágazás, akkor hasznos lenne egy olyan "ecset", ami követi az egeret, de közben a háttérképen lévő sötét vonalakhoz próbál igazodni. A live polygon szerkesztő azt jelenti, hogy a vonalnak már meghúzott végétől az egérkurzorig egy "élő" vonalszakasz fut: folyamatosan mutatja, hogy ha ide kattintanék, akkor merre futna pontosan a vonal. Ezáltal ha az algoritmus kitalálja a helyes utat, kattintok és megyek tovább. Ha nem sikerül neki, akkor visszább megyek a már megrajzolt vonal végéhez egészen addig, amíg helyes nem lesz a megoldás. Ha jó a heurisztika, nagy léptekkel haladhatok. Ha rossz (a feladat túl bonyolult azon a helyen), akkor sűrűbben kell súgnom a programnak, hogy merre van a helyes irány.

Technikailag ez egy folyamatos útvonalkeresést jelent minden egérmozgáskor (tipikusan A* algoritmussal). Az alábbi képeken egy mesterséges és egy a lenti videóban bemutatott kezdetleges implementációval kapott példa látható.

![Live polygon működés közben]({{ site.baseurl }}/assets/LivePolygonElesben.png){: .center-image }

Elős körös eredményekről egy videó:
![]({{ site.baseurl }}/assets/video.png){: .vertical-center-image } [Szélességi keresés alapú live polygon](https://www.youtube.com/watch?v=hTscFkFewl0)

> Amiket tanulhatsz vele:
>
>  * Útvonal keresési algoritmusok továbbfejlesztése, alkalmazása képeken történő keresésre
>  * Keresés futási idejének csökkentése mindenféle trükkökkel, előre dolgozással, cacheléssel.
>  * Útvonalkeresés integrálása felhasználói felületbe
>  * Továbbfejlesztésként a keresés adaptív paraméter hangolása esetén tanuló és optimalizáló algoritmusok használata.

### Algoritmus fejlesztése polygonok "esztétikus" összeolvasztására

Ha a felhasználó talál két polygont, amik valójában egyetlen kalcitszemcséhez tartoznak, akkor azokat jó lenne, ha minél kevesebb mozdulattal össze tudná olvasztani. Például úgy, hogy húz egy vonalat, ami minden összeolvasztandó polygonon átmegy. Ezután a program nem csak összevonja őket, hanem ki is tölti a köztük lévő réseket, amiket a hibásan felismert határvonalak okozhattak.

Az alábbi ábrán az 1-es és 2-es polygont akarjuk összeolvasztani, a 3-ast viszont nem. Ahhoz, hogy megfelelő határvonal maradjon közöttük, a zöld "kipótlás" nem szabad, hogy hozzáérjen a 3-as polygonhoz, így a piros területet mindenképpen ki kell hagyni a C és D pontok közötti összeolvasztásnál.

![Blob merge 1]({{ site.baseurl }}/assets/abra_BlobMerge.png){: .center-image }

A GrainAutLine 1 alkalmazásban ez így nézett ki, de ott az adatmodell alapvetően raszteres volt, így az a megoldás csak igen korlátozottan emelhető át és szerencsésebb újratervezni.

![Blob merge 2]({{ site.baseurl }}/assets/BlobMerge_small.png){: .center-image }

> Amiket tanulhatsz vele:
>
>   * Alacsony szintű képmanipulációs módszerek és magas szintű, felhasználói eszközök összekapcsolása
>   * A cv4s adatmodell flexibilis használata
>   * Vektoros adatmodellre vonatkozó manipulációs módszerek (pl. polygon unió és különbség meghatározása)

### Szakadást nem okozó vékonyítás

Előfordul, hogy a felhasználó egy vékony elválasztó vonalat be akar rajzolni, de azt egészen pontosan megadni időigényes feladat. Ehelyett lehet rajzolni egy vastag vonalat (az alábbi képen a fekete vonallal határolt terület), mely lefedi a helyes megoldást, de sok felesleget is tartalmaz. Képmorfológiai műveletként ezt a vonalat elvékonyítjuk úgy, hogy lehetőleg csak olyan részek maradjanak meg, amik az eredeti képen is sötétek, viszont ez nem okozhatja a vonal szakadását. Ha elszakadna, akkor meg kell elégedni néhány a kelleténél világosabb pixel meghagyásával is. Így alakul ki a szaggatott vonallal jelzett vonal. Ezt hívják ismuth-aware erosionnak.

![Ismuth aware erosion]({{ site.baseurl }}/assets/IsmuthAwareErosion.png){: .center-image }

> Amiket tanulhatsz vele:
>
>   * Alacsony szintű képmanipulációs módszerek és magas szintű, felhasználói eszközök összekapcsolása
>   * A cv4s adatmodell flexibilis használata

## Osztályozási módszerek fejlesztése

A GrainAutLine rendszer egyik elsődleges célja a márványok eredetének meghatározása. Jelenleg ez tipikusan stabil izotópok (C13 és O18, Sr87/Sr86) és a Maximal Grain Size (MGS, vagyis a legnagyobb szemcse átmérője) alapján történik. Ez utóbbit tudjuk megmérni a szemcsehatárok ismeretében. A mi feladatunk, hogy további, képfeldolgozáson alapuló tulajdonságokat nyerjünk ki, majd azokkal együtt pontosabb osztályozást tegyünk lehetővé.

Ennek a folyamatnak fontos pontja az osztályozási módszerek vizsgálata, mint például a Bayes döntés, Maximum Likelihood (ML) döntés, Linear Discriminant Analysis (LDS), Support Vector Machine (SVM), döntési fa építés például information gain alapokon, valószínűségi hálók stb.

Az alábbi ábra a [www.missmarble.info](http://www.missmarble.info/) adatbázis alapján készült, melyből igen sok márvány vékonycsiszolat képe rendelkezésünkre áll.

![Osztályozás]({{ site.baseurl }}/assets/classification.png "Osztályozás"){: .center-image }

> Amiket tanulhatsz vele:
>
>   * Az alakzatok, mintázatok jellemzésére és felismerésére használható módszerek
>   * Az osztályozási módszerek világának megismerése

### Szemcse alakzat jellemzése

Az osztályozási feladatokhoz minél több olyan jellemzőt kell kinyernünk a képekből, amik alapján meg lehet különböztetni az egyes márványokat. A szemécsék mérete mellett a képfeldolgozásban számos alakzat jellemzőt találunk (péládul terület-kerület arány, momentumok, fraktál dimenzió és még rengeteg más), melyeket érdemes megvizsgálni, hogy mennyire hasznosak a márványok megkülönböztetésében.

> Amiket tanulhatsz vele:
>
>   * Az osztályozás alapjául szolgáló tulajdonságok kinyerése, fontosságuk
>   * Alakzatok jellemzésére használt módszerek

## Megjelenítéssel kapcsolatos fejlesztések

Ezek a feladatok elsősorban a megjelenítést szolgálják magas, WPF szinten. Az adatmodellben változtatást csak akkor hajtanak végre, ha például a polygonok kulcs-érték párjait használják a kitöltési szín eltárolására.

### "Zoom lens" az egér mellé

Amennyiben a polygonok szerkesztése egy alattuk látható kép alapján történik, szükség lehet egy nagyító eszközre, mely az egérkurzortól nem túl messze követi az egeret és az egér alatti területet mutatja felnagyítva, esetleg bizonyos képrétegeket kihagyva. Egy ilyen eszköz WPF alatti, teljesítmény hatékony elkészítése igen látványos feladat, a felhasználók munkáját pedig nagyságrendekkel egyszerűsíti. (Sokszor probléma az, hogy hogyan rajzolunk be határvonalakat úgy, hogy munka közben pont a rajz takarja ki azt, ami alapján rajzolunk, vagyis az eredeti képet. Így nehéz észrevenni az esetleges hibákat.)

> Amiket tanulhatsz vele:
>
>   * WPF trükkök a gyors és szaggatásmentes felhasználói felülethez
>   * Az OpenCV és a WPF összekapcsolása

### Képfeldolgozó algoritmusok paraméterezéséhez előnézeti ablak

Számos képszűrésnél vagy más algoritmusok futtatásánál hasznos, ha egy előnézeti ablak interaktívan mutatja, hogy egy paraméter beállításnak mi lesz a hatása. Például egy küszöbszint pontos beállításánál jól jön, ha azonnal látszik, mely területek vannak a küszöb felett és melyek nem. Ilyesmire támogatás jelenleg még nincs a keretrendszerben, pedig számos helyen igen hasznos lenne.

> Amiket tanulhatsz vele:
>
>   * Képfeldolgozási műveletek futtatása és az eredmény megjelenítése C# WPF környezetben.

### HTML5 alapú megjelenítő kliens

A cv4s keretrendszer alapvetően WPF alkalmazásokra készül .NET környezetben, viszont az adatmodell könnyedén sorosítható JSON formátumba és így könnyen el lehet küldeni szerver oldalra, vagy másik klienseknek. Egy alternatív webes felület sok alkalmazásban igen jelentősen megnövelné a felhasználási lehetőségeket. Még akkor is, ha első körben például csak megjelenítésre képes, szerkesztésre nem.

A HTML5 alapú kliensprogramból még semmi nem készült el, kivéve egy a cv4s adatformátumát beolvasó és polygonok megjelenítésére képes házi feladat alkalmazást, mely kiindulási alapként szolgálhat a továbblépésre.

> Amiket tanulhatsz vele:
>
>   * HTML5 trükkök polygonok és képek megjelenítésére
>   * Egy összetettebb adatmodell szerverrel történő szinkronizálása
>   * Az adatmodell változásait követő megjelenítés webes felületen, polygonok és raszteres képek formájában.

## Andoid frontend készítése

Ennek a témának a célja egy olyan Android alkalmazás elkészítése, mely képes fényképeket készíteni, azokat elküldeni a szerver oldalon működő cv4sensorhub keretrendszerrel készült feldolgozónak (REST API kommunikációval), majd az eredményt (szöveges vagy kép) megjeleníti a felhasználónak.

Egy ilyen frontend számos alkalmazás fő felhasználói felülete lehet (pl. műkincs azonosítás, bútorlap "színkód" textúra alapú azonosítása, telefonra rakható mikroszkóp használatával szemcseméret statisztikák készítése stb.), az alkalmazásnak minél általánosabbnak és később jól testre szabhatónak (customizing, branding) kell lennie.

> Amiket tanulhatsz vele:
>
>   * Fényképek készítése, alapvető UI feladatok Android alatt.
>   * Kommunikáció szerver és Androidos eszköz között .NET környezetben
>   * API kialakítása úgy, hogy azt tetszőleges, a cv4sensorhub keretrendszerre épülő alkalmazás könnyen tudja használni.
>   * A cv4sensorhub keretrendszer alapvető felépítését (bár erre itt viszonylag kevés szükség lesz).

## Automatikus pontosság-kiértékelő környezet kialakítása

A GrainAutLine rendszer akkor jó, ha a szemcsehatárokat magától is minél pontosabban meg tudja határozni. A ChemoTracker célja szintén a sejtek helyes azonosítása, valamint a helyes követés.

A folyamatos fejlesztés során hatalmas előny, ha előre elkészített és végigellenőrzött (ground truth) adathalmazok segítségével folyamatosan lehet teszteket futtatni continuous integration jelleggel. Így ha egy módosítás lerontja a pontosságot, gyorsan észrevesszük és könnyebben ki tudjuk javítani a bevitt hibát.

Ehhez kell egy automatikus kértékelő keretrendszer, mely előre elkészített tesztképeket megetet a programmal, kiértékelteti őket, majd a mintamegoldással összeveti az eredményeket. A tesztek futtatását lehetőleg teljesen automatikusan végzi és az eredményekből tömör jelentést generál.

> Amiket tanulhatsz vele:
>
>   * Polygonok és azok halmazainak összehasonlítási módszerei
>   * Egy módszer értékelésére szolgáló módszerek megismerése. (Pontosságot igen sokféle képpen lehet mérni és nagyon nem mindegy, melyiket választjuk, mert az eredmény félrevezető lehet.)
>   * Continuous integration és egyéb tesztkörnyezetek kialakításának eszközei, report generálás például ütemezett feladatokból.
