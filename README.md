# Carte interactive — Présence terrain RD Congo

Carte Leaflet en un seul fichier (`index.html`), prête à héberger sur GitHub Pages et à intégrer en `<iframe>`.

## Mettre en ligne (GitHub Pages)

1. Crée un nouveau dépôt public sur GitHub (ex. `carte-rdc`).
2. Ajoute le fichier `index.html` à la racine du dépôt (commit + push).
3. Dans le dépôt : **Settings → Pages → Source** → choisis la branche `main` et le dossier `/ (root)` → **Save**.
4. Après 1–2 minutes, ta carte est en ligne à l'adresse :
   `https://TON-NOM-UTILISATEUR.github.io/carte-rdc/`

## Intégrer sur ton site (iframe)

```html
<iframe
  src="https://TON-NOM-UTILISATEUR.github.io/carte-rdc/"
  style="width:100%; height:700px; border:0; border-radius:16px; overflow:hidden;"
  loading="lazy"
  title="Carte interactive - Présence terrain RD Congo">
</iframe>
```

Ajuste `height` selon l'espace disponible sur la page (600–800px fonctionne bien sur desktop ; sur mobile la carte s'adapte automatiquement en hauteur réduite).

## Mettre à jour les données

Toutes les données (provinces, coordonnées, staff, projets, partenaires) sont dans le tableau
`provincesData` en haut du `<script>` dans `index.html`. Pour ajouter/modifier une province,
copie ce modèle et ajuste :

```js
{
  name: "Nom-Province",
  lat: 0.000, lng: 0.000,      // coordonnées GPS du centre de la province
  staff: 25,                    // nombre total de staff
  projets: [
    "1. Intitulé du projet…",
    "2. Intitulé du projet…"
  ],
  partenaires: "Partenaire A; Partenaire B; Partenaire C"  // séparés par ;
}
```

Pas besoin de toucher au reste du code : les totaux d'en-tête, la légende, les couleurs des
bulles et la liste latérale se recalculent automatiquement à partir de ce tableau.

## Ce qui a été corrigé par rapport à la première version

- **Taille des bulles fiable au zoom** : remplacement de `L.circle` (rayon en mètres, donc
  instable selon le niveau de zoom) par `L.circleMarker` (rayon fixe en pixels).
- **Fond de carte adapté à un usage public/iframe** : tuiles CARTO au lieu d'appeler directement
  les serveurs OpenStreetMap (évite un blocage d'IP en cas de trafic).
- **Navigation par liste** en plus des bulles sur la carte, avec recherche — utile pour les
  petites provinces (ex. Lualaba, 10 staff) difficiles à cliquer sur mobile.
- **Légende reliée aux données réelles** et cliquable pour filtrer les provinces par tranche de staff.
- **Totaux automatiques** (nombre de provinces, staff total, nombre de projets) calculés depuis
  les données, donc toujours justes même après modification.
- **Version mobile** : la liste devient un tiroir accessible via le bouton ☰.

## Notes

- Deux numéros de projets apparaissent en double dans les données sources pour le Nord-Kivu et
  le Sud-Kivu (ex. deux entrées "5." et deux "13."/"15."). Je les ai conservés tels quels — à
  corriger dans le fichier source si ce sont de vraies erreurs de numérotation.
