# Vizsgaremek
## Bevezetés
### Feladat leírása
A pénzügyi térben mozogni kívánóknak  elengedhetetlen az előzetes ismeret, így a gyakorlás számára fontos egy kockázatmentes, valósághű környezet, ahol a felhasználók megismerhetik a piaci mechanizmusokat, gyakorolhatják a kereskedést, és visszajelzést kaphatnak a döntéseikre. A valós platformok használata anyagi kockázatot rejt, míg a teljesen szintetikus tesztkörnyezet a valós adatok dinamikus viselkedésével  modellezi az éles szituációkat. A javasolt megoldás olyan hibrid szimulátor létrehozása, amely hasonlóan viselkedik a valós piacokhoz, mégis megőrzi a kockázatmentességet.

Az feladatot két fő részre bontjuk. A webes felületen a felhasználók élvezhetik az applikáció nyújtotta lehetőségeket, míg az asztali alkalmazás az admin szintű hozzáférést biztosítja a projekt háttrének.

### A projekt célja
A projekt több, egymáshoz kapcsolódó célt szolgál. Az alkalmazások lehetőséget adnak a felhasználóknak arra, hogy tanulási vagy oktatási célból megismerjék a tőzsde és a kereskedés alapelveit, mindezt biztonságos, kockázatmentes környezetben. Emellett lehetőséget biztosítanak arra is, hogy a felhasználók kipróbálhassák meglévő tudásukat és különböző kereskedési stratégiáikat, valós árfolyamadatok alapján, valódi pénzügyi kockázat nélkül.

A projekt szakmai minőségét tekintve képesek leszünk dokumentációk, teszteredmények és az asztali, valamint webes alkalmazás bemutatására.

## Rendszeráttekintés
### Rendszerarchitektúra és komponensek
A rendszer három rétegből épül: front-end (webes React ), backend (Node.js REST API), és az adatbázis (PostgreSQL). Az adminisztrációs felület különálló WPF asztali alkalmazásként kapcsolódik ugyanahhoz a REST API-hoz. Külső API-k: CoinMarketCap a piaci adatokhoz; Stripe teszt API a pénzügyi szimulációkhoz; opcionálisan autentikációhoz  OAuth szolgáltatók (Google, GitHub).

### Webes alkalmazás

| Funkciók                                                | Ingyenes  | Stadard  | Pro  |
| :------------------------------------------------------ | :-------: | :------: | :--: |
| Chart nézet (gyertya/vonal)                             |    ✅     |    ✅    |  ✅  |
| Wallet (Stripe teszt API)                               |    ✅     |    ✅    |  ✅  |
| Egyenleg + tranzakciók megjelenítése                    |    ✅     |    ✅    |  ✅  |
| Eszközök (coinok) listázása                             |    ✅     |    ✅    |  ✅  |
| Átváltás crypto <-> crypto                              |    ✅     |    ✅    |  ✅  |
| Felhasználói adatok szerkesztése                        |    ✅     |    ✅    |  ✅  |
| Adás/Vétel (Spot[^1])                                   |    ✅     |    ✅    |  ✅  |
| Margin[^3] kereskedés                                   |    ✅     |    ✅    |  ✅  |
| Limit[^2] kereskedés                                    |    ✅     |    ✅    |  ✅  |
| AI (szimulált) kereskedés                               |    ✅     |    ✅    |  ✅  |
| AI chatbot kreditek                                     |    5      |    30    |  100 |
| 2FA + profil + közösségi fiókok + fizetés + OAuth (???) |    ❌     |    ✅    |  ✅  |
| Valósidejű kereskedés                                   |    ❌     |    ✅    |  ✅  |
| Korlátlan portfólió méret                               |    ❌     |    ❌    |  ✅  |
| Stop‑loss                                               |    ❌     |    ❌    |  ✅  |
| TradingView  chart                                      |    ❌     |    ❌    |  ✅  |
| Előfizetési díj                                         |   FREE    |    $35   |  $49 |

### Asztali alkalmazás

| Funkciók                                               | Admin  |
| :----------------------------------------------------- | :----: |
| Felhasználói adatok megjelenítése, szerkesztése        |   ✅   |
| Büntetés szabályszegés esetén (Wash trading, spoofing) |   ✅   |
| Tranzakciók részleteinek megjelenítése                 |   ✅   |
| Teljes jogú felhasználói fiók kezelése                 |   ✅   |
| Fiók létrehozása (web + desktop jogokkal)              |   ✅   |

### Felhasznált technológiák
1. React
2. WPF .NET Framework
3. Node.js
4. REST API 
5. Git

## Szerepkörök és jogosultságok

| Szerepkör      | Funkciók                                                                        |
| :------------- | :------------------------------------------------------------------------------ |
| Admin          | * Asztali alkalmazás funkcióinak kezelése<br>* Weben elérhető funkciók kezelése |
| Végfelhasználó | -  Weben elérhető funkciók kezelése                                             |

## Funkcionális követelmények

### Webes alkalmazás

| ID   | Funkció neve                      | Leírás                                                                                                   | Bemenet                                  | Kimenet / eredmény                        |
| :--- | :-------------------------------- | :------------------------------------------------------------------------------------------------------- | :--------------------------------------- | :---------------------------------------- |
| F-01 | Chart nézet                       | A felhasználó grafikonon tekintheti meg a kriptovaluták árfolyamát.                                      | Kiválasztott eszköz (coin), nézet típusa | Megjelenített TradingView chart           |
| F-02 | AI / Real time adatválasztás      | A felhasználó választhat AI-szimulált adatok és valós idejű adatok között.                               | Mód kiválasztása                         | A kiválasztott adatforrás megjelenítése   |
| F-03 | Fiókkezelés                       | Felhasználói fiók létrehozása és kezelése (GitHub-layout szerint).                                       | Név, email, jelszó, profilkép            | Aktív felhasználói profil                 |
| F-04 | Wallet integráció                 | A felhasználó Stripe API segítségével kezelheti a pénztárcáját.                                          | Be- és kiutalási adatok                  | Egyenleg frissítése a tranzakció alapján  |
| F-05 | Egyenleg megjelenítés             | A rendszer megjeleníti a felhasználó egyenlegét.                                                         | Felhasználói azonosító                   | Valuta, összeg                            |
| F-06 | Be- és kiutalás                   | Fiat és kripto eszközök be- és kiutalása.                                                                | Összeg, típus, célpont                   | Tranzakció létrejön és naplózódik         |
| F-07 | Eszközlista                       | A rendszer megjeleníti a felhasználó birtokában lévő coinokat.                                           | Felhasználói azonosító                   | Saját coinlista                           |
| F-08 | Swapping                          | Két eszköz közti átváltás megadott árfolyamon.                                                           | Forrás coin, cél coin, mennyiség         | Swap utáni egyenleg, csere végrehajtva    |
| F-9  | Előfizetés kezelése               | A felhasználó „Free”, „Standard” vagy „Pro” előfizetést választhat havi/éves díjjal.                     | Csomag kiválasztása                      | Előfizetés aktiválása, kreditek kiosztása |
| F-10 | AI chatbot használata             | A felhasználó krediteket használhat AI-alapú elemzésekre.                                                | Lekérdezés, kredit mennyiség             | Elemzés válasza, kredit levonása          |
| F-11 | Kereskedési funkciók              | Adás-vétel lehetősége árfolyam alapján, több üzemmódban.                                                 | Eszköz, mennyiség, típus (spot[1])       | Tranzakció végrehajtva                    |
| F-12 | Stop-loss[^4] beállítás           | Prémium funkció: árfolyam-alapú automatikus eladás beállítása.                                           | Eszköz, árfolyam                         | Automatikus eladás adott feltételnél      |
| F-13 | Felhasználói profil testreszabása | Profilkép, közösségi fiókok, fizetési módok, OAuth beállítása.                                           | Feltöltött adatok                        | Frissített profilinformációk              |
| F-14 | Felhasználói portfólió            | Pro felhasználóknál korlátlan mennyiségű coin kezelése. Kisebb csomagokban korlátozás, maximum 10 valuta | Felhasználói azonosító                   | Portfólió adatainak tárolása              |
| F-15 | Tranzakciós napló                 | A rendszer naplózza a kereskedési eseményeket és tranzakciókat.                                          | Tranzakció adatai                        | Naplóbejegyzés az adatbázisban            |
### Asztali alkalmazás

| ID   | Funkció neve                     | Leírás                                                                           | Bemenet                             | Kimenet / eredmény                |
| ---- | -------------------------------- | -------------------------------------------------------------------------------- | ----------------------------------- | --------------------------------- |
| F-16 | Felhasználók megjelenítése       | Az admin láthatja a rendszer összes felhasználóját.                              | -                                   | Felhasználói lista                |
| F-17 | Felhasználói adatok szerkesztése | Az admin módosíthatja a felhasználók adatait.                                    | Kiválasztott felhasználó, új adatok | Frissített adatok mentve          |
| F-18 | Szabálysértések kezelése         | Az admin büntetést szabhat ki szabályszegés esetén (zárolás, levonás).           | Wash trading[^5], spoofing[^6]      | Fiók zárolva, egyenleg csökkentve |
| F-19 | Tranzakciók részletei            | Tranzakciós adatok megtekintése.                                                 | Tranzakció azonosító                | Részletes adatnézet               |
| F-20 | Fiók létrehozása adminból        | Az admin új fiókot hozhat létre, teljes jogosultsággal.                          | Felhasználói adatok                 | Új aktív fiók                     |
| F-21 | Teljes hozzáférés biztosítása    | Az admin minden webes funkcióhoz hozzáfér, valamint adminisztratív műveletekhez. | -                                   | Admin funkciók elérhetőek         |
## Nem funkcionális követelmények
### Biztonság
Jelszavak titkosítása (bcrypt), token-alapú hitelesítés (JWT), HTTPS minden kommunikációnál, adatbázis titkosítás. 
### Teljesítmény 
Chart frissítése és adathívások 1–3 másodperces késleltetésen belül legyen real-time módban.  
### Skálázhatóság 
A backend konténerizálható legyen (Docker), horizontálisan skálázható API réteg. 
### Megbízhatóság 
Konzisztens naplózási rendszer, adatbázis azonnali frissítése módosulások esetén. 
### Használhatóság 
Mind a webes, mind pedig az asztali alkalmazás UI reszponzív, akadálymentes. 
## Felhasználói felület 
A felhasználói felület mind a webes, mind az asztali alkalmazásban letisztult megjelenést mutat. A navigáció egyszerű a bal oldali menüszalaggal, ahol láthatjuk az adott pozíciónkat és almenüket.
### Megjelenítési javaslatok
#### Webes felület

<p>
	<p align="left">
		A weboldal a grafikon (chart) nézettel nyílik. Itt lehetőségünk van választani a valós vagy szimulált adatok használata között. Chart nézetben lehetőség az AI (kredit alapú tanácsadás) és a real-time (CoinMarketCap) adatok közti váltásra. Ingyenes csomagban korlátozott chart nézet (gyertya és vonal, maximum havi nézet), míg a pro előfizetés teljes funkcionalitást biztosít.
	</p>
	<img align="right" width="45%" alt="Chart nézet" src="https://github.com/user-attachments/assets/80b177c2-4ee0-48d9-8cf4-897ac88d0ee2" />
</p>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<p>
<p align="right">
	A bal oldali menüsávban kiválaszthatjuk a „Profil” lehetőséget, ahol a saját profilunkat tudjuk megtekinteni és szerkeszteni. Lehetőségünk van az alapcsomagon felüli funkcióók kiaknázására is.
</p>
<img align="left" width="45%" alt="Fiók" src="https://github.com/user-attachments/assets/ec08986d-6ea4-4c8c-8abf-bc07a1f7ab89" />
</p>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<p>
<p align="left">
	A profil alá tartozik a „Tárca” is, amely az adott eszközeinket mutatja. Eszközeink alatt megtekinthetjük a tranzakciós előzményeinket.
</p>
<img align="right" width="45%" alt="Wallet" src="https://github.com/user-attachments/assets/a0973b77-afad-46df-875f-dd51592acc7a" />
</p>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<p>
<p align="right">
	A kereskedési felületen kiválaszthatjuk a kereskedés módját és az egyéb, a kereskedéshez nélkülözhetetlen beállításokat, mint valuta, összeg.
</p>
<img align="left" width="45%" alt="Coins" src="https://github.com/user-attachments/assets/dadeffdd-4d9d-48f6-acbb-d25434d4cdd2" />
</p>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<p>
<p align="left">
	A kereskedési felülethez hasonló módon álhatjuk át valutáinkat egy másikra.
</p>
<img align="right" width="45%" alt="Swap" src="https://github.com/user-attachments/assets/43c1c090-aadb-4191-9329-159f8e2be61b" />
</p>

#### Asztali alkalmazás

tbd

## Adatkezelés
### Adatbázis
Az alábbi ábra szerint épül fel az adatbázis. Íme az ER diagram.
![[image.png]]
## Rendszerkövetelmények
### Fejlesztői környezet
1. Microsoft Visual Studio Code 
2. Microsoft Visual Studio 
3. JetBrains Rider 
4. DBeaver
### Techstack
1. React, WPF
2. Express.js
3. Postgresql
### Általános elvárások
#### Szoftver 
1. A projekt webes felülete bármely mai, modern böngészőben fut.  
2. A projekt asztali alkalmazása kizárólag Windows környezetben fut, annak 10 vagy annál újabb verzióján.
Hardver 
3. Intel Core i3-540 vagy későbbi 
4. Legalább 4 GB ram
## Összefoglalás
A projekt funkcionális specifikációja és az abban rögzített követelmények egyértelmű iránymutatást adnak a fejlesztők számára, hogy a rendszer minden eleme megfeleljen a jogszabályi előírásoknak, a szakmai elvárásoknak és a vizsgaremekkel szemben támasztott követelményeknek. A dokumentáció részletes felépítése biztosítja, hogy a fejlesztési folyamat átlátható, követhető és egységes legyen, ezáltal jelentősen csökkenti a hibalehetőségeket, valamint elősegíti egy minőségi, stabil és bemutatható projekt elkészültét. 

A specifikáció nemcsak a fejlesztők munkáját támogatja, hanem hozzájárul a rendszer későbbi karbantarthatóságához és bővíthetőségéhez is. Egy jól strukturált dokumentáció lehetővé teszi, hogy a jövőben bárki könnyen megértse a rendszer működését, logikai felépítését vagy esetleges továbbfejlesztési pontjait. 

Kiemelten fontos szempont, hogy a felhasználók a rendszer használata során biztonságban érezzék magukat, és megbízzanak az alkalmazás működésében. A dokumentáció ennek megteremtéséhez is hozzájárul: a funkciók átlátható leírása, a működési elvek pontos rögzítése és a következetes fejlesztési gyakorlat mind azt szolgálják, hogy az alkalmazás megbízható, kiszámítható és felhasználóbarát legyen. Ez a bizalom alapvető feltétele annak, hogy a felhasználók magabiztosan dolgozhassanak a rendszerrel, és sikeresen elérhessék a tanulási vagy gyakorlási céljaikat.

[^1]: Spot: aktuális árfolyamon való azonnali kereskedés
[^2]: Limit: a tranzakció csak akkor történik meg, amik az árfolyam eléri az általunk kijelölt célértéke
[^3]: Margin: tőkeáttételes kereskedés
[^4]: Stop-loss: eladási megbízás teljesítése az általunk beállított árfolyamon
[^5]: Wash trading: a befektető saját agával kereskedik, ezzel növelve az árfolyamot
[^6]: Spoofing: megbízások létrehozása teljesítési szándék nélkül
