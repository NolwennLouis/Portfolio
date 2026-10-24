# Portfolio — guide d'utilisation

Ce site est composé uniquement de fichiers HTML, CSS et JavaScript classiques.
Pas de framework, pas d'installation, pas de commande à taper. Tu peux
ouvrir `index.html` directement dans ton navigateur pour voir le site.

## Fichiers importants

| Fichier | À quoi il sert |
|---|---|
| `works.js` | La liste de tes œuvres. C'est ici que tu ajoutes/modifies/supprimes une œuvre. |
| `about.js` | Tes informations perso : nom, présentation, formation, email, liens. |
| `index.html`, `work.html`, `about.html`, `oeuvre.html` | Les pages du site. Tu n'as normalement pas besoin d'y toucher. |
| `style.css` | Les couleurs, polices et mises en page. |
| `script.js` | Le code qui affiche automatiquement le contenu de `works.js` et `about.js`. |
| `images/`, `videos/` | Tes fichiers médias. |

## Modifier mon nom, ma présentation, mes liens

Tout se passe dans **`about.js`**. Ouvre le fichier avec un éditeur de texte
(par exemple [VS Code](https://code.visualstudio.com/), ou même le Bloc-notes)
et modifie les valeurs :

```js
const ABOUT = {
  name: "Ton Nom",
  tagline: ["Character Design", "Illustration", "2D Animation"],
  bio: ["Premier paragraphe...", "Deuxième paragraphe..."],
  email: "toi@example.com",
  links: [
    { label: "LinkedIn", url: "https://linkedin.com/in/toi" }
  ]
  // ...
};
```

Sauvegarde le fichier : le site est mis à jour partout automatiquement
(en-tête, page d'accueil, page About, footer).

## Ajouter une œuvre

1. Mets ton image dans le dossier `/images` (ou ta vidéo dans `/videos`).
2. Ouvre `works.js`.
3. Copie un bloc existant (entre `{` et `}`) et colle-le juste avant le `]`
   final du tableau `WORKS`.
4. Modifie les informations : `id` (unique, sans espace), `title`,
   `category`, `year`, `tools`, `description`, `media`.
5. Sauvegarde.

L'œuvre apparaît automatiquement dans la galerie et dans les filtres
correspondant à sa catégorie. Les catégories possibles sont :
`character-design`, `animation`, `sketchbook`, `other`.

Pour qu'une œuvre apparaisse sur la page d'accueil, ajoute
`featured: true` à son bloc.

## Ajouter une vidéo

Dans le bloc de l'œuvre :

```js
type: "video",
media: "videos/mon-animation.mp4",
poster: "images/miniature.jpg"   // optionnel : image affichée avant lecture
```

## Ajouter plusieurs images à une même œuvre

Utilise la propriété `gallery` :

```js
gallery: [
  { src: "images/oeuvre-01.jpg", caption: "Version finale" },
  { src: "images/oeuvre-01-recherches.jpg", caption: "Recherches" }
]
```

Toutes ces images s'afficheront sur la page de détail de l'œuvre, dans l'ordre.

## Modifier les couleurs et les polices

Tout est regroupé en haut du fichier `style.css`, dans la section
`1. VARIABLES` :

```css
:root {
  --bg: #0b0a0d;        /* fond du site (noir) */
  --bg-2: #17151b;      /* fond des vignettes en attente */
  --fg: #efeaf0;        /* couleur du texte */
  --accent: #ef4b5f;    /* rouge — accent principal */
  --accent-2: #8b5cf6;  /* violet — accent secondaire */
  --font-display: "Fraunces", ...;  /* police des titres */
  --font-body: "Work Sans", ...;    /* police du texte courant */
}
```

Change ces valeurs, sauvegarde, et tout le site est mis à jour.

## Mettre un de tes dessins en fond de la page d'accueil

Sur la Home, un dessin peut apparaître en fond, derrière le titre (en
transparence, sous un léger voile sombre pour que le texte reste lisible).

Ouvre **`about.js`** et change cette ligne :

```js
heroBackground: "images/hero-bg-placeholder.svg",
```

Remplace le chemin par ton image (ex. `"images/mon-dessin.jpg"`), après
avoir mis le fichier dans `/images`. Choisis de préférence une image assez
large (1600px de large ou plus) et pas trop chargée en détails fins, pour
qu'elle reste lisible même en transparence derrière le texte.

## À propos de la galerie (façon Pinterest)

Les œuvres s'affichent en colonnes (3 sur desktop, 4 sur grand écran, 2 sur
tablette, 1 sur mobile), chaque image gardant ses proportions naturelles et
s'empilant dans la colonne — exactement comme sur Pinterest. C'est purement
géré en CSS (`column-count` dans `style.css`) : il n'y a rien à calculer ni
à ajuster, quelles que soient les proportions de tes images.

## Remplacer les images placeholder

Les images actuelles (fond beige avec le texte « Placeholder ») ne sont
que des exemples de mise en page. Remplace-les par tes propres fichiers
dans `/images`, en gardant le même nom (ou en mettant à jour le champ
`media` correspondant dans `works.js`).

## Déployer le site (Netlify + GitHub)

1. Crée un compte sur [GitHub](https://github.com) si tu n'en as pas.
2. Crée un nouveau dépôt (repository) et mets-y tous les fichiers de ce
   dossier (glisser-déposer via l'interface web GitHub fonctionne très bien,
   pas besoin de ligne de commande).
3. Va sur [Netlify](https://netlify.com) et crée un compte (tu peux te
   connecter directement avec ton compte GitHub).
4. Clique sur « Add new site » → « Import an existing project » → choisis
   ton dépôt GitHub.
5. Netlify te demande une commande de build : laisse ce champ **vide**
   (il n'y a rien à construire, ce sont déjà des fichiers finis). Le
   dossier à publier est la racine du projet (`.` ou vide).
6. Clique sur « Deploy ». Ton site est en ligne en quelques secondes.

À chaque fois que tu modifies un fichier et que tu le renvoies sur GitHub
(« push » ou simplement en le remplaçant via l'interface web GitHub),
Netlify republie automatiquement le site.

## Questions fréquentes

**Je veux changer l'ordre des œuvres dans la galerie.**
Change l'ordre des blocs dans le tableau `WORKS` de `works.js` : la galerie
suit exactement cet ordre.

**Je veux ajouter une nouvelle catégorie.**
C'est possible mais demande de toucher un peu de code (dans `work.html`
pour le bouton de filtre, et dans `script.js` dans la fonction
`categoryLabel`). Si tu n'es pas à l'aise, garde les 4 catégories
existantes, qui couvrent déjà large.

**Le site a l'air cassé quand je l'ouvre directement en double-cliquant.**
Certains navigateurs bloquent le chargement de fichiers JavaScript en
local pour des raisons de sécurité. Si `index.html` semble vide, essaie
d'utiliser l'extension **Live Server** dans VS Code (clic droit sur
`index.html` → « Open with Live Server »), ou publie directement sur
Netlify pour tester : ça fonctionnera normalement en ligne.
