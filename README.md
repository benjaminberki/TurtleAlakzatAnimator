README – BBP Turtle alakzat-animátor


Név: Berki Benjámin Péter

Neptun-kód: YELRCY

Tárgy: Szkript nyelvek – Python

Féléves projektfeladat

00-Python-Projektfeladat

1. Feladat rövid leírása

A program egy turtle alapú grafikus alkalmazás, amely különböző szabályos alakzatokat (ötszög, hatszög, csillag, strb) rajzol és animál a képernyőn.

Az alkalmazás:

turtle grafikai modullal rajzolja ki az alakzatokat és a BBP monogramos logót

billentyűzettel és egérrel vezérelhető

használ saját modult, saját osztályt és saját függvényt, melyek nevében szerepel a monogram: BBP

demonstrálja egy tanult modul (pl. random) és egy bemutatandó modul (turtle) használatát, több függvényhívással 

04-3-Python

A felhasználó:

SPACE lenyomásával vagy az alakzatváltó gomb kattintásával léphet a következő alakzatra

R billentyűvel vagy a forgatás gombbal be-/kikapcsolhatja az automatikus forgatást

ESC vagy a Kilépés gomb segítségével bezárhatja az alkalmazást

Indításkor a program röviden kirajzol egy BBP monogram logót, majd megjeleníti az első alakzatot és az UI-gombokat.

2. Program felépítése és indítás

A program a beadandó leírásának megfelelően main.py-ból indul. 

00-Python-Projektfeladat

Fájlstruktúra:

main.py – belépési pont

app_BBP.py – az alkalmazás logikája (kontroller / „app” modul)

shapes_BBP.py – saját modul, alakzatleírásokkal és BBP-s függvényekkel

Indítás:

python main.py


A main.py létrehozza az alkalmazás objektumát, majd meghívja a futtató metódust.

3. Modulok és függvények
3.1. Tanult és bemutatandó modulok (standard modulok)

turtle modul – bemutatandó modul
A grafikus rész nagy része a turtle modulra épül (előadás 11–12. szerint).
Használt főbb elemek:

turtle.Screen() – grafikus ablak létrehozása

screen.title() – ablak címe

screen.bgcolor() – háttérszín beállítása

turtle.Turtle() – teknős objektumok létrehozása

turtle.mainloop() / screen.mainloop() – eseménykezelő ciklus futtatása

screen.onkey(függvény, "billentyű") – billentyűzet-események kezelése

turtle.onclick(függvény) – egérkattintás kezelése gombhoz

Rajzoló függvények: forward(), left(), right(), penup(), pendown(), goto(), circle(), dot(), stb.

Ezekkel demonstrálom a bemutatandó modul legalább 3 függvényét/metódusát.

random modul – tanult modul 

04-1-Python

random.choice() – véletlenszerű szín választása az alakzatok kirajzolásakor

(Szükség esetén bővíthető randint / egyéb függvényekkel is.)

3.2. Saját modul: shapes_BBP.py

Saját Python modul, amely tartalmaz egy BBP monogramos osztályt és egy BBP nevű függvényt.

Osztály: ShapeBBP

Attribútumok:

name – az alakzat neve (pl. „Ötszög”, „Hatszög”, „Csillag”)

sides – oldalak száma (csillagnál a belső logika miatt 5)

size – az alakzat mérete (távolság a turtle lépéseiben)

is_star – logikai érték, hogy csillag-alakzatot rajzoljon-e

Metódusok:

__init__(self, name, sides, size, is_star=False)
Inicializálja az alakzat paramétereit.

draw(self, t)
A kapott turtle.Turtle objektummal kirajzolja az adott alakzatot a képernyőre.

ha is_star == True, akkor 5 ágú csillagot rajzol

egyébként szabályos sokszöget rajzol sides és size alapján

Saját függvény (monogramos): random_color_BBP()

Visszaad egy véletlenszerűen választott színt egy előre megadott színlistából.

A TurtleAnimator osztály minden újrarajzoláskor ezt hívja meg, így az alakzatok dinamikusan eltérő színeket kapnak.

(Ez a függvény a beadandó kiírásának megfelelően tartalmazza a BBP monogramot a nevében. 

00-Python-Projektfeladat

)

3.3. Saját modul: app_BBP.py

Az alkalmazás logikai része, eseménykezeléssel és „frontend” elemekkel (gombok, státuszfeliratok).

Osztály: TurtleAnimatorBBP

Felelős:

a turtle.Screen beállításáért

az alakzatok listájának kezeléséért

az aktuális alakzat kirajzolásáért

az animáció (forgás) vezérléséért

a billentyűzet- és egéresemények kezeléséért

az UI „gombok” és státuszsor kirajzolásáért

Főbb attribútumok:

screen – turtle ablak

t – rajzoló teknős

shapes – ShapeBBP objektumok listája (ötszög, hatszög, csillag)

current_index – az aktuális alakzat indexe

rotate – logikai változó, hogy a forgás be van-e kapcsolva

UI-hoz használt kiegészítő teknősök (cím, státuszsor, gombok feliratai)

Fontosabb metódusok:

__init__(self)
Beállítja az ablakot, létrehozza az alakzatokat, az UI-t és az eseménykezelőket.

draw_current(self)
Törli a képernyőt, véletlen színt kér a random_color_BBP() függvénytől, majd kirajzolja az aktuális alakzatot.

next_shape_BBP(self)
A következő alakzatra lép (a lista elemei között ciklikusan), majd meghívja a draw_current() metódust.

toggle_rotation(self)
Átbillenti a rotate állapotot (forgás be/ki).

animate(self)
Időzítő alapú animációs ciklus (screen.ontimer(...)). Ha a rotate igaz, akkor kis szögben elforgatja az alakzatot, és újrarajzolja.

close(self)
Lezárja az alkalmazást (screen.bye()).

run(self)
Elindítja az első kirajzolást és az animációs loopot, majd meghívja a turtle.mainloop()-ot / eseményciklust.

A TurtleAnimatorBBP osztály nevében szintén benne van a BBP monogram, ezzel teljesítve a „saját osztály neve tartalmazza a monogramot” követelményt. 

00-Python-Projektfeladat

4. Eseménykezelés

A program a következő eseményeket kezeli:

Billentyűzet

SPACE – továbblép a következő alakzatra (next_shape_BBP)

R – forgás be-/kikapcsolása (toggle_rotation)

ESC – kilépés a programból (close)

Egér

Alul található három „gomb” turtle-rajzolt keretek:

„Következő alakzat” – ugyanaz, mint a SPACE (alakzatváltás és újrarajzolás)

„Forgatás be/ki” – ugyanaz, mint az R billentyű

„Kilépés” – ugyanaz, mint az ESC billentyű

A gombokra kattintást onclick események figyelik, és a megfelelő metódusokat hívják meg.

5. Osztályok összefoglalva

ShapeBBP
Saját osztály, ami egy szabályos alakzat leírására szolgál (név, oldalszám, méret, csillag-e), és képes a turtle objektummal kirajzolni azt.

TurtleAnimatorBBP
Az alkalmazás vezérlő osztálya. Kezeli az ablakot, a rajzolást, az animációt, az eseményeket és a felhasználói felület elemeit (gombok, státuszsor, cím).
