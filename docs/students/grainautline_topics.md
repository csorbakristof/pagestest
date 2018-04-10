---
parent: forstudents.md
menu: GrainAutLine
---

Ide azok a témák tartoznak, melyek a cv4s keretrendszerre épülő GrainAutLine alkalmazás feladataihoz kapcsolódnak. Az alkalmazás céljairól itt található részletesebb leírás: [GrainAutLine]({{ site.baseurl }}/grainautline.html)

* TOC
{:toc}

## Szemcse darabok összevonása monte carlo módszerrel

Számos képszegmentációs módszernél előfordul, hogy túlszegmentálja a képet, vagyis a kelleténél több darabra vágja fel. A márvány képek szegmentációja azért nehéz, mert a szemcséken belül is vannak vonalak. Ennek a feladatnak a lényege, hogy ha a szemcséket szándékosan több darabra vágjuk fel, utána azokat megfelelően összevonogatva kapjuk meg a helyes megoldást. Ahhoz, hogy a véletlenszerű összevonogatás jó irányba vigyen minket, az összevonandó területeket úgy sorsoljuk, hogy figyelembe vesszük, melyik összevonás mekkora valószínűséggel javítja a teljes megoldás értékét. Ehhez általában definiálunk egy a szemcsehalmazokon értelmezett jóság függvényt, melyet megpróbálunk maximalizálni. A jóság függvény vizsgálhatja például a szemcse méreteket, a bennük lévő esetleges kontúrokat, a  határvonalak eltérő színét, a szemcse konvexitását stb.

Az alábbi képen egy túlszegmentált kiindulási állapot látható. A kérdés az, hogy melyik területeket lenne érdemes összevonni.

![RJMCMC]({{ site.baseurl }}/assets/rjmcmc.png){: .center-image }

> Amiket tanulhatsz vele:
>
>   * Képszegmentációs feladatok megoldása, tipikus problémái
>   * Optimalizálás egy nagyon elterjedt módszercsaláddal
>   * Annak gyakorlása, hogy az alkalmazási területből származó többlet ismereteket (domain knowledge) hogyan lehet egy optimalizáló algoritmusba beépíteni.

## Megjelenítéssel kapcsolatos fejlesztések

Ezek a feladatok elsősorban a megjelenítést szolgálják magas, WPF szinten. Az adatmodellben változtatást csak akkor hajtanak végre, ha például a polygonok kulcs-érték párjait használják a kitöltési szín eltárolására.

### "Zoom lens" az egér mellé

Amennyiben a polygonok szerkesztése egy alattuk látható kép alapján történik, szükség lehet egy nagyító eszközre, mely az egérkurzortól nem túl messze követi az egeret és az egér alatti területet mutatja felnagyítva, esetleg bizonyos képrétegeket kihagyva. Egy ilyen eszköz WPF alatti, teljesítmény hatékony elkészítése igen látványos feladat, a felhasználók munkáját pedig nagyságrendekkel egyszerűsíti. (Sokszor probléma az, hogy hogyan rajzolunk be határvonalakat úgy, hogy munka közben pont a rajz takarja ki azt, ami alapján rajzolunk, vagyis az eredeti képet. Így nehéz észrevenni az esetleges hibákat.)

> Amiket tanulhatsz vele:
>
>   * WPF trükkök a gyors és szaggatásmentes felhasználói felülethez
>   * Az OpenCV és a WPF összekapcsolása

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

### Márványok distance transform histogram alapú jellemzése

Sok olyan márványkép van, amiben a kontraszt nem elég nagy ahhoz, hogy a szemcsehatárokat pontosan meg tudjuk határozni. Mivel a szemcseméret továbbra is egy fontos mennyiség, ezt megpróbálhatjuk úgy közelíteni, hogy minden pontra megnézzük, ott mekkora kört lehetne berajzolni a képre úgy, hogy az elférjen a szemcsehatár-gyanús, sötétebb vonalak között.

A képfeldolgozásban gyakran használt [distance transform](https://medium.com/on-coding/euclidean-distance-transform-d37e06958216#.9j0gdvx1k) pont ezt a berajzolható kör méretet határozza meg minden pontra. Mivel azt sem tudjuk, mekkora a kontraszt és mikortól számítson egy vonal (maszat) szemcsehatárnak, így érdemes lehet ezt minden lehetésges fényerő küszöbre megvizsgálni és ezekből együttesen levonni a következtetést.

A feladat erősen kísérletezős, kutatós. A terv az, hogy a distance transform eredményéből készítünk egy-egy hisztogrammot minden fényerő küszöb szintre, vagyis minden lehetséges "mikortól számít valami elég sötét pixelnek ahhoz, hogy szemcsehatár vonalnak tekintsük" értékre (ez lesz az adaptive thresholding küszöbszintje). Várhatóan a képtől függően ezekben a hisztogrammokban bizonyos fényerőknél jelentős változásokat látunk majd. Ha máskor nem, akkor amikor már minden szemcsehatár eltűnik és egy üres képre futtatjuk a distance transzformációt. Ezeknél a határoknál, valamint a határok között félúton lehet érdemes elkezdeni a vizsgálatot, hogy hol milyen értékek a dominánsak. Utána pedig lehet azzal folytatni, hogy a hisztogrammot nem a distance transform teljes eredményére, hanem csak a lokális maximum értékekre (csúcsokra) generáljuk le és így vizsgáljuk a fentieket. Ezek után pedig lehet kísérletezni még a thresholding utána zajszűrésekkel, hogy az 1-2 pixeles szemcsehatár maradékok már ne számítsanak bele semmibe.

> Amiket tanulhatsz vele:
>
>   * Distance transform működése és használata
>   * Alapvető képfeldolgozási műveletek (adaptive thresholding, zajszűrések)
>   * Osztályozási lehetőségek statisztikák, jelen esetben hisztogrammok alapján
>   * Megoldás publikálása tudományos cikk formájában

## Okosabb polygon műveletek fejlesztése a felhasználó felület számára

Itt következnek olyan eszközök, melyeket a felhasználó közvetlenül tud felhasználni az automatikus módszerek eredményeinek korrigálására, például a határvonalak kézi kijavítására. Fontos, hogy ezek a végfelhasználóknak tényleg praktikusak és kényelmesek legyenek, különben nem fogják őket használni.

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
