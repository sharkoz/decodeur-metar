# Décodeur METAR

Webapp statique en français pour apprendre à lire un METAR aéronautique.

Elle permet de coller un METAR ou de récupérer un METAR par code OACI, puis de le décomposer en tableau pédagogique : lecture littérale, explications, conversion UTC vers heure locale, vitesses en km/h et m/s, altitudes en mètres, pression en Pa et boussole visuelle pour le vent.

## Utilisation

Ouvrir directement `index.html` dans un navigateur, ou utiliser la version GitHub Pages :

https://sharkoz.github.io/decodeur-metar/

Un aérodrome peut être partagé ou mis en favori avec le paramètre `icao` :

https://sharkoz.github.io/decodeur-metar/?icao=LFBD

À l'ouverture, la page préremplit l'OACI et récupère automatiquement le METAR correspondant.

## Sources de données

- Autocomplétion et détails aéroport : `https://raw.githubusercontent.com/mwgg/Airports/master/airports.json`
- METAR principal : `https://metar.vatsim.net/{ICAO}`
- Fallback METAR : `https://api.met.no/weatherapi/tafmetar/1.0/metar.txt?icao={ICAO}`

Aucune donnée d'aéroport n'est copiée localement : le fichier `airports.json` est chargé dynamiquement par la page.

## Déploiement

Le site est un fichier statique. GitHub Pages sert la branche `gh-pages`, avec `index.html` à la racine.
