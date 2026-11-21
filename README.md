# Nagy Magyarország – vármegyék, 1910

Interaktív OpenStreetMap-térkép a Magyar Királyság 1910-es vármegyéiről. A korábbi egyszerűsített országhatár megmaradt, mellé került a szűkebb Magyarország 63 vármegyéje és Fiume, valamint külön kikapcsolható rétegen Horvát-Szlavónország 8 vármegyéje.

A térkép a `index.html` fájl. A geometria a `data/` mappában van:

- `data/magyar-kiralysag-hatar.geojson` – az eredeti, egyszerűsített királysághatár
- `data/varmegyek-magyarorszag-1910.geojson` – 63 vármegye + Fiume város és területe
- `data/varmegyek-horvat-szlavon-1910.geojson` – Horvát-Szlavónország 8 vármegyéje

A vármegyehatárok az OpenHistoricalMap 1910-es közigazgatási viszonyaiból származnak (CC0, a szlovén határ egyes szakaszai CC BY 4.0). A forrás, a licenc, a viszonyazonosítók és a tulajdonságmezők leírása: [SOURCES.md](SOURCES.md).

Helyi megtekintéshez a mappából egy webszerver kell, mert a térkép a GeoJSON-fájlokat kéri le:

```bash
python3 -m http.server 8765
```
