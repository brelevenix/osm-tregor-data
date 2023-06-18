# Exemples de données de Lannion-Trégor Commuanuté

- Fichier [GeoJSON](ltc.geojson) des limites de LTC
- Fichier [ZIP](ltc.zip) des limites de LTC

## Obtenir les limites depuis OpenStreetMap

Requête sur [Overpass](https://overpass-turbo.eu/)

```
(area["name"="Bretagne"]->.zone;
rel(area.zone)
  ["ref:FR:SIREN"="200065928"];);
out;>;out skel;
```

Conversion au format SHP avec `ogr2ogr`

```bash
 ogr2ogr -nlt POLYGON -skipfailures ltc.shp ltc.geojson
```
