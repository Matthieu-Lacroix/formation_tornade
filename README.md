# Genèse d'une tornade — bac à sable interactif

Une application web *single-page*, en Three.js pur, qui explique la genèse d'une tornade supercellulaire à travers un modèle interactif, manipulable étape par étape, plutôt qu'un récit passif.

**[→ Voir la démo](#)** *(ajoute ton lien GitHub Pages ici une fois déployé)*

![Aperçu](#) *(ajoute une capture d'écran ou un GIF ici)*

## Pourquoi ce projet

La plupart des vulgarisations sur les tornades montrent un tube qui se redresse puis se resserre, sans jamais expliquer *pourquoi*. Ce projet part du cadre scientifique actuel (Markowski & Richardson) et rend chaque mécanisme manipulable : on règle soi-même le cisaillement, l'updraft, le RFD, l'étirement — et on voit la géométrie du vortex, le nuage et les masses d'air répondre en temps réel.

## Cadre scientifique

L'application suit le schéma en trois processus physiquement distincts établi par la littérature récente sur la tornadogenèse supercellulaire :

1. **Mésocyclone (mi-niveaux)** — le cisaillement vertical du vent crée une vorticité horizontale, basculée à la verticale par le courant ascendant de l'orage. Rotation à 3-6 km, sans lien avec le sol.
2. **Vorticité près du sol (RFD)** — indépendamment du mésocyclone, le contact entre l'air chaud de l'*inflow* et l'air frais du *rear-flank downdraft* (RFD) génère une nouvelle vorticité horizontale par processus barocline.
3. **Étirement / convergence** — sous le mésocyclone de basse couche, l'air converge vers l'axe de rotation en montant. Par conservation du moment angulaire (L ≈ r²·ω), ce resserrement amplifie violemment la rotation jusqu'à former la tornade.

**Sources** : Markowski & Richardson (2009, *Atmospheric Research* ; 2014) · Klemp & Rotunno (1983) · Davies-Jones (2006).

> ⚠️ **Ce n'est pas une simulation physique.** Aucune équation de Navier-Stokes, pas de vraie thermodynamique, échelles et proportions non respectées, topologie RFD/inflow simplifiée. L'objectif est d'illustrer la *logique* des mécanismes, pas de les calculer. Ce point est rappelé dans l'application elle-même.

## Fonctionnalités

- **5 étapes manipulables** : cisaillement → basculement → vorticité RFD → étirement → vue d'ensemble automatique
- **Vortex en particules** (~4200) enroulées sur une courbe de Bézier quadratique dont les points de contrôle répondent aux sliders en temps réel
- **Masses d'air visibles** (RFD froid / inflow chaud) avec étiquettes et flux animés
- **Conservation du moment angulaire** rendue lisible : rayon et vitesse de rotation affichés en direct
- **Cisaillement vectoriel** (vitesse + direction), avec boussole dédiée — le cisaillement est un vrai prérequis : sans lui, rien en aval ne se développe
- **Lecture automatique** ("Vue d'ensemble") qui rejoue toute la chaîne sans intervention
- **Mode capture** plein écran pour filmer proprement (réseaux sociaux)
- **Bilingue FR/EN**, responsive mobile

## Utilisation

Aucune dépendance à installer : un seul fichier HTML, Three.js chargé depuis un CDN.

```bash
# Cloner puis ouvrir directement
git clone <ton-repo>
cd <ton-repo>
open tornado-sandbox-v3.html   # ou double-clic
```

Pour un déploiement GitHub Pages : place le fichier à la racine du dépôt (éventuellement renommé `index.html`), active Pages dans les paramètres du dépôt sur la branche `main`.

## Stack technique

- **Three.js r128** (CDN, aucun bundler)
- JavaScript natif, un seul fichier — HTML/CSS/JS intégrés
- Aucune dépendance backend

## Structure du code

Tout est commenté directement dans le fichier. Grandes sections :

- Scène / caméra / lumières / sol
- Nuage paramétrique (blobs sphériques par rôle : cumulus, tour, enclume, wall cloud, collar cloud)
- Vortex principal : système de particules sur `THREE.QuadraticBezierCurve3`
- Vecteurs de vent, flux d'air (updraft, inflow, RFD descendant), débris au sol
- Masses d'air RFD/inflow avec étiquettes en sprites
- Logique par étape (`STAGES_DATA`) : texte scientifique + sliders + pose de courbe, en français et anglais
- Autoplay (rejoue les étapes dans le temps sans intervention)
- Boucle d'animation avec lissage systématique (opacités, rayon, vitesse de rotation, position du nuage) pour éviter tout saut visuel entre états

## Limites connues

- Proportions non réalistes (échelle indicative seulement, via le repère "immeuble ~30 m / barre 500 m")
- Topologie RFD/inflow simplifiée à deux volumes géométriques
- Pas de cisaillement directionnel complet (hodographe) — seulement une direction simple pour le vent d'altitude

## Licence

*(à compléter selon ton choix — MIT recommandé pour un projet pédagogique)*

## Remerciements

Construit par itérations successives avec Claude (Anthropic), sur la base du cadre scientifique de Paul Markowski et Yvette Richardson.
