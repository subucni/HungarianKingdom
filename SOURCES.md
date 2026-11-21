# Források és licenc

A vármegyehatárok 1910. december 31-i, a népszámlálás napján érvényes közigazgatási állapotot ábrázolják. A koordináták minden fájlban WGS84 földrajzi koordináták, GeoJSON-sorrendben: `[hosszúság, szélesség]`.

## Fájlok

| Fájl | Tartalom |
| --- | --- |
| `data/magyar-kiralysag-hatar.geojson` | A térképen rajzolt királysághatár: a vármegyék uniójának külső pereme, Horvát-Szlavónországgal együtt. |
| `data/nagy-magyarorszag-1910-vonal.geojson` | Ugyanez a határ vonalként (LineString), a korábbi uMap-körvonal formátumában. |
| `data/nagy-magyarorszag-1910-terulet.geojson` | Ugyanez a határ felületként (Polygon), a korábbi uMap-felület formátumában. |
| `data/magyarorszag-es-fiume-1910-vonal.geojson` | Csak a szűkebb Magyarország és Fiume külső pereme (MultiLineString: az ország és a fiumei exclávé). |
| `data/magyarorszag-es-fiume-1910-terulet.geojson` | Ugyanez felületként (MultiPolygon). |
| `data/magyarorszag-mai-hatar-vonal.geojson` | A mai Magyarország határa vonalként (LineString). |
| `data/magyarorszag-mai-hatar-terulet.geojson` | Ugyanez felületként (Polygon); ezt rajzolja a térkép. |
| `data/varmegyek-ma.geojson` | A mai 19 vármegye és Budapest (20 felület). |
| `data/oszver.geojson` | Öszvér réteg: mai vármegyék a mai határon belül, 1910-es maradék azon kívül. |
| `data/oszver-vonal.geojson` | Ugyanezek külső vonala. |
| `data/varmegyek-ma-vonal.geojson` | Ugyanezek külső vonala, vármegyénként. |
| `data/varmegyek-magyarorszag-1910.geojson` | A szűkebb Magyarország 63 vármegyéje és Fiume város és területe (64 elem). |
| `data/varmegyek-horvat-szlavon-1910.geojson` | Horvát-Szlavónország 8 vármegyéje. |

Egy vármegye tulajdonságai:

- `name` – magyar név, például `Pest-Pilis-Solt-Kiskun vármegye`
- `szekhely` – 1910-es megyeszékhely
- `orszagok` – a mai országok, amelyekkel a poligon érdemben átfed (nagyobb átfedés elöl)
- `tipus` – `vármegye` vagy, Fiume esetében, `corpus separatum`
- `orszagcsoport` – `magyarorszag` vagy `horvat-szlavonorszag`
- `cimke` – a felirat helye `[hosszúság, szélesség]`, a poligon belsejében

## A királyság határa

A korábbi uMap-export két, koordinátára azonos fájl volt, mindkettő neve `Nagy-Magyarország (egyszerűsített)`, 878 töréspont, zárt gyűrű:

- vonal (`LineString`) – a körvonalréteg
- felület (`Polygon`) – a kitöltő réteg

Ezt a 878 pontos, egyszerűsített vonalat a vármegyék uniójának külső pereme váltotta fel. Minden új töréspont rajta van valamelyik 1910-es megyehatáron. A néhány négyzetkilométeres, megyék közé szorult rést (csatlakozási hézag, nem valódi enklávé) a körvonal kitölti, hogy a vonal egyetlen folyamatos perem legyen.

| Változat | Név a fájlban | Geometria | Töréspont |
| --- | --- | --- | --- |
| Teljes királyság, vonal | Nagy-Magyarország (1910) | LineString | 3310 |
| Teljes királyság, felület | Nagy-Magyarország (1910) | Polygon | 3310 |
| Magyarország és Fiume, vonal | Magyarország és Fiume (1910) | MultiLineString (2 rész) | 2830 + 29 |
| Magyarország és Fiume, felület | Magyarország és Fiume (1910) | MultiPolygon (2 rész) | 2830 + 29 |

A két rész Magyarország és a tőle Horvát-Szlavónország által elválasztott Fiume. A fájlok szerkezete a régi exporté: egy `FeatureCollection`, egy elem, egyedüli tulajdonság a `name`, szóköz nélküli JSON. Ezek tölthetők vissza uMapba. A térkép a teljes királyság felületét használja, kitöltés nélkül, piros vonallal.

## Mai magyar határ

Forrás: OpenStreetMap Magyarország-viszony (`relation/21335`, adminisztratív országhatár), letöltve 2026. november 21-én a Nominatim polygon-végpontjáról. Licenc: [ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/), © OpenStreetMap közreműködők. A nyers vonal 37 754 pont volt; Douglas–Peucker egyszerűsítés 0,002 fokos tűréssel 1689 pontra csökkentette. A felület területe az egyszerűsítés után 93 011 km², a részletes poligoné 93 012 km².

A fájlban a név: `Magyarország (mai határ)`. A térkép kék vonallal (`#1d4ed8`) rajzolja, a piros királysághatár és a vármegyefelületek fölött.

## Mai vármegyék

Forrás: OpenStreetMap, a hét statisztikai régió (`admin_level=5`) alatti 20 `admin_level=6` viszony: 19 vármegye és Budapest. Letöltve 2026. november 21-én. Licenc: [ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/), © OpenStreetMap közreműködők.

A közös megyehatárokat egyszer, 0,002 fokos tűréssel egyszerűsítettük, hogy a szomszédok éle azonos maradjon. A külső peremet a már egyszerűsített mai országhatárra illesztettük: a vármegyék uniója és a `magyarorszag-mai-hatar` felület eltérése 0,001 km² alatt van. Az OSM névcímkéje még „megye”; a fájlban a 2023 óta hivatalos „vármegye” alak szerepel, Budapest külön főváros. A székhely az OSM `admin_centre` csomópontja. Pest vármegye székhelye Budapest, a székhely pontja ezért a főváros felületén van, nem a megyéében.

A térkép lila vonallal (`#6d28d9`) rajzolja, halvány lilás kitöltéssel, hogy a határ összevethető legyen az 1910-es vármegyékkel. Tulajdonságok: `name`, `szekhely`, valamint `tipus` (`vármegye` vagy `főváros`) és `cimke`. A vonalas fájlban csak `name` és `szekhely` van.

## Öszvér réteg

A mai országhatáron belül a `varmegyek-ma.geojson` 20 eleme szerepel (`tipus`: `mai`). Azon kívül, a királyság 1910-es külső határáig, az 1910-es vármegyéknek a mai Magyarországból kivont része (`tipus`: `1910-maradek`). A Horvát-Szlavónországból származó maradékok `orszagcsoport` értéke `horvat-szlavonorszag`, a magyarországiaké `magyarorszag`. A maradékok megtartják az `orszagok` mezőt.

A határvonalak egyszerűsítése miatt a mai határ mentén vékony szilánkok keletkeztek. Ezeket nem önálló elemekként tartottuk meg: ami 1 km²-nél kisebb és nem tömör folt (a kivétel egy legalább 0,4 km²-es, legalább 0,8 km széles, kitöltöttségében legalább 0,3-as darab), azt a vele határos megmaradt vármegyéhez olvasztottuk. Összesen 162 ilyen szilánk volt, 11,8 km². Így a réteg hézagmentesen és átfedés nélkül fedi a királyság felületét.

A térképen a mai rész lila (`#6d28d9`), az 1910-es magyarországi maradék borostyán (`#9a3412`), a horvát-szlavón maradék zöldeskék (`#0f766e`). A réteg alapból ki van kapcsolva.

## Vármegyehatárok

Forrás: [OpenHistoricalMap](https://www.openhistoricalmap.org/), lekérdezve 2026. november 21-én az Overpass API-n (`https://overpass-api.openhistoricalmap.org/api/`). Az 1910. december 31-én érvényes `border_type=county` határviszonyok (adminisztratív szint 5), Fiume esetében a `Fiume város és területe` viszony (1868–1918).

A határokat az OHM-szerkesztők a második és a harmadik osztrák katonai felmérés (Franziszeische / Franzisco-Josephinische Landesaufnahme), valamint a mai államhatár ottani szakaszai alapján rajzolták, ahol a történelmi vonal azzal esik egybe. Az egyes viszonyok OHM-azonosítója a vármegye nevéhez kötve a lenti listában szerepel.

### Licenc

Az OpenHistoricalMap adatbázisa, ahol egy elemen nincs külön `license` címke, a [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) közkincs-felajánlás alatt áll. A projekt kérése, hogy a felhasználásnál az OpenHistoricalMap legyen megnevezve: <https://www.openhistoricalmap.org/copyright>.

Kivétel: 39 határvonal a mai szlovén államhatár nyilvántartásából származik, `license=CC-BY 4.0` és `attribution=Surveying and Mapping Authority of the Republic of Slovenia` címkével (`source=https://ipi.eprostor.gov.si/jgp/data`). Ezek Vas, Zala, Varasd, Zágráb és Modrus-Fiume külső, Szlovéniával közös szakaszain szerepelnek. A geometriát egyszerűsítettük. Felhasználásuk feltétele a [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) szerinti névjelölés.

Más, licenccímke nélküli vonalak forráscímkéi között szerepel még az Egyesült Államok külügyminisztériumának LSIB államhatár-adata (közkincs) és a cseh–szlovák határ egyes szakaszain a `source=kapor2` címke (Trencsén, Nyitra). Ezeken nincs külön licenccímke, ezért az OHM CC0 felajánlása vonatkozik rájuk.

### Egyszerűsítés

A közös határvonalakat egyszer, Douglas–Peucker eljárással, 0,002 fokos tűréssel egyszerűsítettük, a csatlakozási pontok megtartásával, majd a koordinátákat 5 tizedesre kerekítettük. Így a szomszédos vármegyék közös éle azonos marad. Az összes vármegye együttes területe az egyszerűsítés után kevesebb mint 6 km²-rel tért el a részletes geometriától (mintegy 325 500 km²-ből), a vármegyék egymással való átfedése pedig 2 km² alatt maradt.

### Terület-ellenőrzés

A poligonok területét a magyar nyelvű 1910-es vármegyei területadatokkal vetettük össze (a vármegyék saját szócikkei és a *A Magyar Királyság vármegyéinek listája (1881–1920)*). A legtöbb vármegye 1 százalékon belül egyezik. Nagyobb, de még 5 százalék alatti eltérés van néhány erdélyi vármegyénél (Alsó-Fehér, Beszterce-Naszód, Csík) és Lika-Krbavánál: az OHM-viszonyok megjegyzései ezeket első, durvább változatnak jelölik. Fiume város és területe 22,5 km², a történeti corpus separatum mintegy 21 km²-es területéhez közel.

Abaúj-Torna, Sáros és Zemplén esetében az OHM-ben két, 1910 körül váltó változat van. Azt használtuk, amelynek területe a népszámlálási adattal pontosabban egyezik (Abaúj-Torna 2928765, Sáros 2928767, Zemplén 2829508).

Ung vármegye OHM-viszonya (2929703) hibásan 1876. június 19-től ugyaneddig van keltezve. Ez az 1876-os megyerendezés utáni poligon, területe 3226 km² a népszámlálás 3230 km²-éhez képest, ezért ezt vettük 1910-es határnak.

### Mai országok

Az `orszagok` mező a részletes (egyszerűsítés előtti) poligon és a Natural Earth 1:10 000 000 admin-0 országhatárok (közkincs, 2022. májusi kiadás) metszete. Egy ország akkor került fel, ha az átfedés legalább 25 km², vagy egyetlen, legalább 8 km²-es és kellően tömör darab (így maradt bent Ung vármegye kis magyarországi csücske). A vékony, csak a határvonal generalizálásából eredő sávok nem szerepelnek. A lista a geometria tényleges átfedését mutatja, nem egy kézi „mely utódállamok örökölték” besorolást: ahol a történelmi folyó- vagy gerinchatár nem esik egybe a mai vonallal, a szomszédos ország is megjelenhet.

### Székhelyek

Az 1910-es megyeszékhelyek a vármegyék magyar Wikipédia-szócikkeiből és a *List of historic counties of Hungary* 1867–1920 közötti felsorolásából származnak. Két helyen a korszak hivatalos nevét használtuk a későbbi helyett: Alsó-Fehér székhelye Nagyenyed (nem Gyulafehérvár), Moson székhelye Magyaróvár (a Mosonmagyaróvár név 1939 utáni).

## OpenHistoricalMap-viszonyok

Magyarország és Fiume:

| Név | OHM-viszony |
| --- | --- |
| Abaúj-Torna vármegye | 2928765 |
| Alsó-Fehér vármegye | 2928927 |
| Arad vármegye | 2829224 |
| Árva vármegye | 2829459 |
| Bács-Bodrog vármegye | 2746362 |
| Baranya vármegye | 2829048 |
| Bars vármegye | 2829773 |
| Békés vármegye | 2829207 |
| Bereg vármegye | 2829533 |
| Beszterce-Naszód vármegye | 2928938 |
| Bihar vármegye | 2829450 |
| Borsod vármegye | 2829348 |
| Brassó vármegye | 2928931 |
| Csanád vármegye | 2829206 |
| Csík vármegye | 2928934 |
| Csongrád vármegye | 2829221 |
| Esztergom vármegye | 2829058 |
| Fejér vármegye | 2829027 |
| Fiume város és területe | 2696322 |
| Fogaras vármegye | 2928928 |
| Gömör és Kishont vármegye | 2829593 |
| Győr vármegye | 2829020 |
| Hajdú vármegye | 2829509 |
| Háromszék vármegye | 2928932 |
| Heves vármegye | 2829444 |
| Hont vármegye | 2829741 |
| Hunyad vármegye | 2928925 |
| Jász-Nagykun-Szolnok vármegye | 2829445 |
| Kis-Küküllő vármegye | 2928929 |
| Kolozs vármegye | 2928936 |
| Komárom vármegye | 2829030 |
| Krassó-Szörény vármegye | 2747633 |
| Liptó vármegye | 2829454 |
| Máramaros vármegye | 2829357 |
| Maros-Torda vármegye | 2928937 |
| Moson vármegye | 2829045 |
| Nagy-Küküllő vármegye | 2928930 |
| Nógrád vármegye | 2829350 |
| Nyitra vármegye | 2830017 |
| Pest-Pilis-Solt-Kiskun vármegye | 2829222 |
| Pozsony vármegye | 2830016 |
| Sáros vármegye | 2928767 |
| Somogy vármegye | 2829034 |
| Sopron vármegye | 2829042 |
| Szabolcs vármegye | 2829510 |
| Szatmár vármegye | 2928940 |
| Szeben vármegye | 2928926 |
| Szepes vármegye | 2829558 |
| Szilágy vármegye | 2829407 |
| Szolnok-Doboka vármegye | 2928939 |
| Temes vármegye | 2747634 |
| Tolna vármegye | 2829049 |
| Torda-Aranyos vármegye | 2928935 |
| Torontál vármegye | 2747437 |
| Trencsén vármegye | 2829774 |
| Turóc vármegye | 2829770 |
| Udvarhely vármegye | 2928933 |
| Ugocsa vármegye | 2829352 |
| Ung vármegye | 2929703 |
| Vas vármegye | 2829047 |
| Veszprém vármegye | 2829035 |
| Zala vármegye | 2829036 |
| Zemplén vármegye | 2829508 |
| Zólyom vármegye | 2829443 |

Horvát-Szlavónország:

| Név | OHM-viszony |
| --- | --- |
| Belovár-Kőrös vármegye | 2747463 |
| Lika-Krbava vármegye | 2858025 |
| Modrus-Fiume vármegye | 2858024 |
| Pozsega vármegye | 2747534 |
| Szerém vármegye | 2747535 |
| Varasd vármegye | 2747458 |
| Verőce vármegye | 2747538 |
| Zágráb vármegye | 2747460 |
