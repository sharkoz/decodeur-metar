# Décodeur METAR

Webapp statique en français pour apprendre à lire un METAR aéronautique.

Elle permet de coller un METAR ou de récupérer un METAR par code OACI, puis de le décomposer en tableau pédagogique : lecture littérale, explications, conversion UTC vers heure locale, vitesses en km/h et m/s, altitudes en mètres, pression en Pa et symbole aéronautique de vent (hampe et barbules) pour la direction et la force du vent.

L'encart de détail de l'aérodrome affiche aussi la distance et la direction depuis votre position (si la géoloc est connue) et des coordonnées cliquables qui ouvrent une carte.

## Utilisation

Ouvrir directement `index.html` dans un navigateur, ou utiliser la version GitHub Pages :

https://sharkoz.github.io/decodeur-metar/

Un aérodrome peut être partagé ou mis en favori avec le paramètre `icao` :

https://sharkoz.github.io/decodeur-metar/?icao=LFBD

À l'ouverture, la page préremplit l'OACI et récupère automatiquement le METAR correspondant. Sans paramètre `icao` (aucun aérodrome sélectionné), elle propose de vous géolocaliser : elle liste les aérodromes les plus proches, teste leur disponibilité METAR de haut en bas (les aérodromes sans donnée sont grisés) et charge automatiquement le premier disponible.

Le bouton de géolocalisation (icône cible, à gauche de l'étoile favoris) permet de relancer cette recherche à tout moment. Si un aérodrome est déjà sélectionné, il déroule la liste des aérodromes proches avec leur disponibilité **sans** en charger un automatiquement : à vous de choisir.

Le champ de recherche propose une autocomplétion : en saisissant un code OACI, un code IATA ou un nom de ville/aérodrome, un bandeau de suggestions s'affiche (navigable au clavier avec les flèches et Entrée). Quand la position est connue, la distance en km est indiquée, et la disponibilité METAR des 5 premières suggestions est testée (les indisponibles sont grisées).

La page propose un mode clair/sombre. Le choix est conservé localement dans le navigateur, avec le thème système utilisé par défaut.

## Sources de données

- Autocomplétion et détails aéroport : `https://raw.githubusercontent.com/mwgg/Airports/master/airports.json`
- METAR principal : `https://metar.vatsim.net/{ICAO}`
- Fallback METAR : `https://api.met.no/weatherapi/tafmetar/1.0/metar.txt?icao={ICAO}`

Aucune donnée d'aéroport n'est copiée localement : le fichier `airports.json` est chargé dynamiquement par la page.

## Déploiement

Le site est un fichier statique. GitHub Pages sert la branche `gh-pages`, avec `index.html` à la racine.
