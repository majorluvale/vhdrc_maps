# Carte RDC — Répartition du personnel par province (style OCHA)

Un seul fichier `index.html`, prêt pour GitHub Pages et l'intégration en `<iframe>`.

## Ce que c'est

- Une vraie carte choroplèthe : les **26 provinces de la RDC sont coloriées** selon leur
  nombre de staff (dégradé bleu clair → bleu foncé). Les provinces sans intervention
  restent en gris clair.
- **Clic sur une province** → popup avec la liste des projets et des partenaires (ou un
  message "Aucune intervention" si la province n'a pas de données).
- Pas de tableau de bord, pas de barre latérale, pas de recherche : juste la carte, une
  légende et un bandeau de titre, dans un style cartographique institutionnel (fond clair,
  Arial, légende encadrée, échelle, flèche du nord) — inspiré des cartes OCHA.
- Les limites administratives des provinces sont incluses directement dans le fichier
  (source : geoBoundaries / découpage territorial RDC à 26 provinces), donc aucune
  dépendance externe à charger à part les tuiles de fond de carte et Leaflet.

## Mettre en ligne (GitHub Pages)

1. Crée un dépôt public sur GitHub (ex. `carte-rdc`).
2. Ajoute `index.html` à la racine (commit + push).
3. **Settings → Pages → Source** → branche `main`, dossier `/ (root)` → **Save**.
4. Ta carte est en ligne à `https://TON-NOM-UTILISATEUR.github.io/carte-rdc/`.

## Intégrer sur ton site (iframe)

```html
<iframe
  src="https://TON-NOM-UTILISATEUR.github.io/carte-rdc/"
  style="width:100%; height:700px; border:0;"
  loading="lazy"
  title="Carte RDC - Répartition du personnel par province">
</iframe>
```

## Mettre à jour les données

Tout se trouve dans l'objet `provincesData` au milieu du `<script>` de `index.html` :

```js
"Nom-Province": {
  staff: 25,
  projets: ["1. …", "2. …"],
  partenaires: "Partenaire A; Partenaire B"
}
```

Le nom de clé doit correspondre au nom de la province tel qu'utilisé dans le fond de carte
(sans accent pour "Kasai" et "Equateur" — c'est déjà géré). Ajouter une province au tableau
suffit : sa couleur, sa légende et les totaux du pied de page se recalculent automatiquement.

## Notes

- Deux numéros de projets sont en double dans les données du Nord-Kivu et du Sud-Kivu
  (ex. deux "5.", deux "13."/"15."). Conservés tels quels — à corriger dans la source si ce
  sont de vraies erreurs.
- Les frontières administratives sont simplifiées pour garder un fichier léger (~85 Ko) ;
  suffisant pour un usage web à l'échelle du pays, pas pour de l'analyse géospatiale fine.
