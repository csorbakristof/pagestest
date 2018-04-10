---
parent: forstudents.md
menu: GIS
---

(This page is meant for hungarian students, that is why it is in Hungarian.)

# Geoinformatikai alkalmazások cv4s alapokon

A geoinformatika egy olyan terület, ahol adat bőven van, ráasásul ez nagyon sokszor polygonok vagy képek formájában áll rendelkezésre. A cv4sensorhub pedig pont ezek kezelésére jött létre, így felvetődik a kérdés, hogy a két eszköztár egyesítésével milyen új megoldásokat lehet létrehozni. A cv4sensorhub adatmodelljében polygonok és hozzájuk kapcsolódó kulcs-érték párok segítségével könnyedén tudunk térképeket, jármű útvonalakat, szenzorhálózati mérési eredményeket ábrázolni, majd azok alapján összetett következtetéseket, becsléseket készíteni. A keretrendszer pedig már gondoskodik ezek látványos megjelenítéséről, a szerkeszthetőségről.

* TOC
{:toc}

(A [játékfejlesztéses témák]({{ site.baseurl }}/students/games_topics.html) között szintén szerepel még néhány ötlet, ami hasonló megoldásokat céloz meg, csak egyelőre játék jelleggel.)

## Autók üzemi adatainak gyűjtése és elemzése

A tanszéki [VehicleICT](https://www.aut.bme.hu/Pages/Research/vehicleict) projekt keretében autók üzemi adatait (pozíció, sebesség, fogyasztás, fordulatszám stb.) gyűjtjük, hogy ezekből üzleti intelligencia megoldások segítségével következtetéseket vonhassunk le. (Például szólhassunk, ha valakinek az autója a többi ugyanolyan autóhoz képest ugyanazon az emelkedőn és ugyanazon sebességben gyanúsan sokat fogyaszt. Vagy ha az illető rendszeresen elfelejt sebességet váltani...)

A begyűjtött adatok és például az OpenStreetMaps alapján könnyedén tudunk időpont függő, autó fogyasztási térképet rajzolni, mely alapján utána lehet üzemanyag mennyiségre optimalizált útvonalakat tervezni. De hasonló módszerrel lehet károsanyag kibocsátási térképet is készíteni. Lehetőség sok van, a pontos célt az érdeklődési területek alapján, közösen fogjuk kialakítani.

> Amiket tanulhatsz vele:
>
>   * Integrációs megoldások, kommunikáció a VehicleICT szerver oldalával.
>   * OpenStreetMaps API használata
>   * Adatelemzési, statisztikai, vagy akár tanuló algoritmusok, optimalizációs módszerek megismerése.
>   * A cv4sensorhub adatmodelljének és megjelenítési képességeinek megismerése.

## Erdők összetételének és topológiájának elemzése

Egy növényzettel kapcsolatos feladatunk keretében 3D szkennerrel készített pontfelhőkből készíthetünk olyan térképeket, melyek az egyes fák törzsének és lombkoronájának helyét ábrázolják. Ehhez kapcsolódnak a fákra vonatkozó további adatok, mint például a lombkorona legalsó részének megassága, vagy az egész fa magassága, a törzs átmérője, a fa fajtája stb.

Kutatási szempontból a cél ezekben az adatokban szabályszerűségek keresése, melyhez első körben erre alkalmas megjelenítő és adatelemző környezet kell. A cv4sensorhub kiválóan alkalmas erre a feladatra, mivel címkézett polygonok formájában a fentieket könnyen ábrázolhatjuk, akár egy térkép fölé rajzolva is. (A térkép csempék formájában elkérhető az OpenStreetMapsről.)

> Amiket tanulhatsz vele:
>
>   * Földrajzi koordináták kezelése polygonokban
>   * OpenStreetMaps adatreprezentáció, adatok letöltése
>   * Szakmai kommunikáció másik szakterületek képviselőivel (ami igen tanulságos és hasznos a szakmánkban!)
>   * A cv4sensorhub adatreprezentációs és megjelenítési rendszerének megismerése

## Drone alapú adatgyűjtés koordinálása

A szenzorhálózatok egyik visszatérő problémája a kommunikációs hatótávolság és az akkumulátor kapacitás. Ha az adatok kiolvasását egy körbejáró drone végezné kis hatótávolságú kommunikációval, akkor az nagyban leegyszerűsíti a helyzetet. Az adatok összegyűjtésének koordinálása viszont ekkor egy új feladat: a bejövő adatok ábrázolása mellett a kiolvasáshoz ütemezést és drone útvonalat is kell tervezni. Főleg, ha az összes szenzor bejárása napokig tart a nagy terület miatt. Ennek a témának a célja egy olyan szoftver megoldás kialakítása, mely ezt a munkát elejétől végéig képes optimálisan koordinálni.

Az alkalmazási terület lehet mezőgazdasági (pl. talajnedvesség, növények víztartalma stb.), erdészeti (hasonló adatokkal, esetleg a lombkorona tetején végezve méréseket), vagy egészen más területek is.

> Amiket tanulhatsz vele:
>
>   * Földrajzi koordináták kezelése polygonokban, térképek használata ilyen céllal
>   * Útvonal tervezés, optimalizálási módszerek
>   * A cv4sensorhub adatreprezentációs és megjelenítési rendszerének megismerése

## Okosváros és forgalom monitorozás/szimuláció

Manapság az okosváros igen felkapott terület: nagyon sok adatot gyűjtünk és ezekre nagyon sok szolgáltatást rá lehet építeni. A cv4sensorhub címkézett polygonokon alapuló adatmodellje és ehhez kapcsolódó felhasználói felülete számos ilyen szolgáltatás alapjaként szolgálhat. Adatokat importálhatunk a BKK FUTÁR rendszerből és az OpenStreetMaps-ről, de felkészíthetjük a rendszert forgalmi adatok fogadására is ([VehicleICT projekt](https://www.aut.bme.hu/Pages/Research/vehicleict), [SOLSUN projekt](https://www.vik.bme.hu/hir/857-solsun-a-fenntarthato-kulteri-vilagitas)). Ha pedig szimulált adatokat is bevállalunk, amikhez esetleg csak később fogunk tudni hozzáférni, akkor különösen sok lehetőség adódik.

Ennek a témakörnek a célját szintén a jelentkezők érdeklődésének függvényében, közösen alakítjuk ki.

> Amiket tanulhatsz vele:
>
>   * Földrajzi koordináták, térképek kezelése polygonokban
>   * BKK FUTÁR REST API használata
>   * OpenStreetMaps API használata
>   * Útvonal tervezés, optimalizálási módszerek, szimulációk... ami a konkrét feladathoz kell.
>   * A cv4sensorhub adatreprezentációs és megjelenítési rendszerének megismerése

## Egyéb, még rendszerezetlen felvetések

  * A BKK menetrend alapján elérhetőségi térkép készítése az egész városról: honnan mennyi idő alatt érhető el pl. a BME és mekkora ennek szórása. (E szerint színezve a térképet.)

  * A user interface számára szükség lenne okos szerkesztő műveletekre, pl. olyan ecsetre, ami odébb tud tolni polygon határokat. De úgy, hogy tényleg kör alakkal „tol”, nem engedi átfedésbe kerülni a polygonokat (azok tranzitívan tolják egymást) és szétesni sem engedi őket

## Egy példa screenshot

Az alábbi screenshot nem egy feladat, hanem egy kis betekintést enged abba, hogy GIS rendszerekkel kapcsolatban nagyjából hogyan nézne ki a cv4sensorhub alapú megoldás technikai oldala. Az itt látható alkalmazás a "MinimalViewer" névre hallgat, ami arra utal, hogy design szempontjából semmilyen célalkalmazásra nincsen felkészítve, helyette viszont rendelkezésre bocsát minden olyan funkciót, ami a keretrendszerben van. A végleges alkalmazások ezeknek valószínűleg csak egy részletét fogják tartalmazni egy részletesebben kidolgozott design formájában.

![cv4s példa screenshot]({{ site.baseurl }}/assets/terkep_demo_abra.png)
