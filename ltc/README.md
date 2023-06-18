# Exemples de données de Lannion-Trégor Commuanuté

- Fichier geojosn des limites de LTC
- Fichier zip avec limites au format shp

## Obtenir les limites depuis OpenStreetMap

Requête sur [Overpass](https://overpass-turbo.eu/)

```
(area["name"="Bretagne"]->.zone;
rel(area.zone)
  ["ref:FR:SIREN"="200065928"];);
out;>;out skel;
```

Conversion en shp avec `ogr2ogr`:

```bash
 ogr2ogr -nlt POLYGON -skipfailures ltc.shp ltc.geojson
```
