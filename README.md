# Décodeur METAR

Webapp statique en français pour apprendre à lire un METAR aéronautique.

Elle permet de coller un METAR ou de récupérer un METAR par code OACI, puis de le décomposer en tableau pédagogique : lecture littérale, explications, conversion UTC vers heure locale, vitesses en km/h et m/s, altitudes en mètres, pression en Pa et symbole aéronautique de vent (hampe et barbules) pour la direction et la force du vent.

L'encart de détail de l'aérodrome affiche aussi la distance et la direction depuis votre position (si la géoloc est connue) et des coordonnées cliquables qui ouvrent une carte.

Chaque groupe décodé explique le sens détaillé des sigles (ex. BKN = *Broken*, ciel fragmenté de 5 à 7 octas) et propose un menu accordéon « autres valeurs possibles » listant tout le vocabulaire de la catégorie (nébulosité, temps présent, tendances...) pour apprendre.

## Utilisation

Ouvrir directement `index.html` dans un navigateur, ou utiliser la version GitHub Pages :

https://sharkoz.github.io/decodeur-metar/

Un aérodrome peut être partagé ou mis en favori avec le paramètre `icao` :

https://sharkoz.github.io/decodeur-metar/?icao=LFBD

À l'ouverture, la page préremplit l'OACI et récupère automatiquement le METAR correspondant. Sans paramètre `icao` (aucun aérodrome sélectionné), elle propose de vous géolocaliser : elle liste les aérodromes les plus proches, teste leur disponibilité METAR de haut en bas (les aérodromes sans donnée sont grisés) et charge automatiquement le premier disponible.

Le bouton de géolocalisation (icône cible, à gauche de l'étoile favoris) permet de relancer cette recherche à tout moment. Si un aérodrome est déjà sélectionné, il déroule la liste des aérodromes proches avec leur disponibilité **sans** en charger un automatiquement : à vous de choisir.

Le champ de recherche propose une autocomplétion : en saisissant un code OACI, un code IATA ou un nom de ville/aérodrome, un bandeau de suggestions s'affiche (navigable au clavier avec les flèches et Entrée). Quand la position est connue, les suggestions sont triées par distance, la distance en km et une flèche de direction sont affichées, et la disponibilité METAR de chaque suggestion est testée (les indisponibles sont grisées).

La page propose un mode clair/sombre. Le choix est conservé localement dans le navigateur, avec le thème système utilisé par défaut.

### Installation sur mobile (PWA)

L'application est une PWA installable : sur Android/Chrome via « Ajouter à l'écran d'accueil » (ou la bannière d'installation), sur iOS via le menu Partager → « Sur l'écran d'accueil ». Elle s'ouvre alors en plein écran avec son icône (barbule de vent). Un *service worker* met en cache l'interface ; hors-ligne, seule la dernière observation et la liste des aérodromes déjà chargées restent consultables (les données temps réel nécessitent le réseau).

## Sources de données

- Autocomplétion et détails aéroport : `https://raw.githubusercontent.com/mwgg/Airports/master/airports.json`
- METAR principal : `https://metar.vatsim.net/{ICAO}`
- Fallback METAR : `https://api.met.no/weatherapi/tafmetar/1.0/metar.txt?icao={ICAO}`

Aucune donnée d'aéroport n'est copiée localement : le fichier `airports.json` est chargé dynamiquement par la page.

## Déploiement

Le site est statique. GitHub Pages le sert depuis la branche `main`, avec `index.html` à la racine. Les fichiers PWA (`manifest.json`, `sw.js`, `icon.svg`, `icon-*.png`, `apple-touch-icon.png`) doivent rester à la racine à côté de `index.html`.

> Note : après une mise à jour, le *service worker* sert l'ancienne version en cache jusqu'à sa prochaine activation. Le cache porte une version (`metar-shell-v1` dans `sw.js`) ; l'incrémenter force le rafraîchissement chez les visiteurs.
