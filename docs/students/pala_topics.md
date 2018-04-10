---
parent: forstudents.md
menu: Schist sections
---

(This page is meant for hungarian students, that is why it is in Hungarian.)

# Pala csiszolat képek elemzésével kapcsolatos témák

A pala csiszolatok elemzéséhez kapcsolódó témák még kialakulóban vannak, mivel a tudományos háttér igényeit most mérjük fel. Érdekes ötleteléseknek nézünk elébe, mivel (1) informatikai oldalról mi nem tudjuk, mire van szüksége a geológusoknak, (2) a geológusok nem tudják pontosan, nekünk mit könnyű és mit nehéz megoldani, valamint (3) számos olyan kutatási terület is kialakulhat, amivel a geológusok pont az esetleg hiányzó informatikai támogatás miatt eddig nem is foglalkoztak.

Az alábbi témákat már most látszik, hogy fogjuk tudni hasznosítani. (A kép Lőrincz Kingától származik, köszönet érte!)

![Pala csiszolat (c)Lőrincz Kinga]({{ site.baseurl }}/assets/pala.jpg){: .center-image }

* TOC
{:toc}

## Többféle megvilágítással készült képek együttes felhasználása

A pala csiszolatok olyan szemcséket is tartalmaznak, melyeket ha eltérő irányú polarizált fénnyel világítunk meg, más színűek lesznek (bizonyos irányok esetén színessá válnak). Ezt kihasználva még ha normál megvilágítás esetén nem is mindig látszik, hol van a szemcse határa, az egymás melletti szemcsék jó eséllyel eltérően fognak reagálni az egyes polarizációkra. Ha tehát több ilyen képünk van ugyanarról a mintáról, a képszegmentáció során egyszerre több képet figyelembe véve sokkal pontosabb szemcserajzolatot kapunk.

> Amiket tanulhatsz vele:
>
>   * Képszegmentációs módszerek
>   * Képek illesztése, a rajtuk talált polygonok hibatűrő megfeleltetése

## Nagyon sűrű szemcsés területek jellemzése

A pala csiszolatokon vannak olyan területek, ahol rengeteg kicsi szemcse van. Ezek pontos körberajzolása egyrészt nagyon nehéz, másrészt nem is biztos, hogy annyira hasznos. Milyen statisztikákkal lehetne ezeket a területeket jellemezni, osztályozni? Néhány hirtelen ötlet:

  * Csak engedjünk rá egy kontúrkereső (pl. Canny) algoritmust és az eredményül kapott foltokból készítsünk méret hisztogrammot.
  * Ha egy világossági küszöb feletti (vagy alatti) területeket tekintünk egy szemcsének, ennek a küszöbnek a függvényében hogyan változik a talált szemcsék területének átlaga, szórása, 25%-os és 75%-os percentilise? Fogunk látni ezekben valami szabályszerűséget? Hirtelen töréspontot? Valamit, ami egy jellegzetes számértéket adhatna?

> Amiket tanulhatsz vele:
>
>   * Képszegmentációs módszerek használata
>   * Alapvető képfeldolgozási eszközök, mint a küszöbölés, az erózió és a dilatáció.
>   * Statisztikák készítése hisztogrammokból, színekből
