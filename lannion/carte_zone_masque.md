# Méthode pour créer la carte

## Récupération des donnés des rues
Récupération des noms via l'arrêté disponible sur le ville de Lannion

## Récupération des rues de Lannion
Petit script utilisé:
```
wget http://download.geofabrik.de/europe/france/bretagne-latest.osm.pbf
osmium tags-filter bretagne-latest.osm.pbf r/ref:INSEE=22113 -o Lannion.osm
osmium export Lannion.osm --geometry-types=polygon -o Lannion.geojson
osmium extract -p Lannion.geojson bretagne-latest.osm.pbf -o Lannion.pbf
osmium tags-filter Lannion.pbf nw/highway=*  -o Lannion_highways.osm
```

## Vérification des noms de rue entre OSM et les noms publiés dans l'arrêté
Quelques corrections apportées:

- Allée Georges Clemenceau => Allée Clemenceau 
- Avenue de Park Nevez => Avenue de Park Névez
- Boulevard Mendes France => Boulevard Pierre Mendès-France
- Chemin de Penn Ar C’Hra => Chemin de Penn ar C’hra
- Escaliers de Brélévénez => Les Escaliers de Brélévénez 
- Rue de Crec’h Quillien => Rue de Crec’h Quellien
- Rue de Pen ar Stang => Rue de Penn Ar Stang
- Rue de Pors an Prat => Rue de Pors An Prat
- Rue du Léandy => Rue de Léandy
- Rue Henri Rol Tanguy => Rue du Colonel Rol-Tanguy
- Rue Saint-Elivet => Rue de Saint-Elivet
- Rue Saint-Jean du Baly => Rue du Baly dans OSM, modifié dans le fichier local OSM
- Mail François Mitterand absent dans OSM => ajouté

Quelques coquilles sur '`' (Forlac'h)

=> A vérifier avec la mairie et corriger ensuite sur OSM si besoin

## Ajustements des rues par rapport aux numéros
Utilisation de JOSM pour couper les rues par rapport aux numéros

## Ajout des éléments manquants sous JOSM
Les différentes places qui sont associées à des `parking`

## Export en Geojson
Plus facile pour travailler ensuite sur Python
```
osmium export Lannion_highways.osm -o Lannion_highways.geojson
```

## Génération du fichier représentant les différentes rues
Utilisation des bibliothèques shapely, geosjon

Tentative de créer un polygone avec `cascade_union` et `convex_hull`, mais le polygone est trop englobant

Conversion des différentes `LineString` en `Polygon' en utilisant la méthode `buffer`qui permet aussi
de mieux visualiser la rue. Utilsation du coefficient 0.00005 
`envelope = linestring.buffer(0.00005)`

## Publication sur umap
Import du fichier geojson et parmétrisation de la couleur et ajout de quelques infos
[Carte Umap](http://umap.openstreetmap.fr/fr/map/zone-de-port-du-masque-a-lannion_522120#16/48.7309/-3.4591)






