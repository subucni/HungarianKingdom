# Nagy Magyarország – vármegyék, 1910

Interaktív OpenStreetMap-térkép a Magyar Királyság 1910-es vármegyéiről. A piros országhatár a vármegyék külső pereme. A szűkebb Magyarország 63 vármegyéje és Fiume egy réteg, Horvát-Szlavónország 8 vármegyéje külön kikapcsolható.

A térkép a `index.html` fájl. A geometria a `data/` mappában van:

- `data/magyar-kiralysag-hatar.geojson` – a térképen rajzolt királysághatár (poligon, Horvát-Szlavónországgal együtt)
- `data/nagy-magyarorszag-1910-vonal.geojson` – ugyanaz vonalként, uMap-ba visszatölthető
- `data/nagy-magyarorszag-1910-terulet.geojson` – ugyanaz felületként, uMap-ba visszatölthető
- `data/magyarorszag-es-fiume-1910-vonal.geojson` – csak Magyarország és Fiume, vonal
- `data/magyarorszag-es-fiume-1910-terulet.geojson` – csak Magyarország és Fiume, felület
- `data/magyarorszag-mai-hatar-vonal.geojson` – a mai Magyarország határa, vonal (OpenStreetMap, ODbL)
- `data/magyarorszag-mai-hatar-terulet.geojson` – a mai Magyarország határa, felület
- `data/varmegyek-ma.geojson` – mai 19 vármegye + Budapest (OpenStreetMap, ODbL)
- `data/varmegyek-ma-vonal.geojson` – ugyanezek vonalként
- `data/oszver.geojson` – öszvér: mai vármegyék belül, 1910-es maradék kívül
- `data/oszver-vonal.geojson` – az öszvér réteg vonalként
- `data/varmegyek-magyarorszag-1910.geojson` – 63 vármegye + Fiume város és területe
- `data/varmegyek-horvat-szlavon-1910.geojson` – Horvát-Szlavónország 8 vármegyéje

A vármegyehatárok az OpenHistoricalMap 1910-es közigazgatási viszonyaiból származnak (CC0, a szlovén határ egyes szakaszai CC BY 4.0). A forrás, a licenc, a viszonyazonosítók és a tulajdonságmezők leírása: [SOURCES.md](SOURCES.md).

Helyi megtekintéshez a mappából egy webszerver kell, mert a térkép a GeoJSON-fájlokat kéri le:

```bash
python3 -m http.server 8765
```
