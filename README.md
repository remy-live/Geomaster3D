# GéoMaster 3D

Éditeur de figures de géométrie dans l'espace, pensé pour préparer des exercices et
des figures de cours en un clic. Tout tient dans un seul fichier `index.html` :
aucune installation, aucun serveur, aucune dépendance.

## Utilisation

Ouvrez `index.html` dans un navigateur récent. C'est tout.

Le fichier fonctionne aussi bien en local (double-clic) que déposé sur n'importe
quel hébergement statique (GitHub Pages, un ENT, une clé USB…).

## Ce que l'on peut construire

| Objets | |
|---|---|
| Solides | pavé droit, prisme droit, pyramide, cylindre, cône, sphère |
| Éléments plans | point, segment, polygone/face, texte libre |

Chaque figure se construit par clics successifs, avec un aperçu fantôme qui suit le
curseur. Les arêtes cachées sont automatiquement tracées en pointillés selon
l'orientation des faces.

### Mise en forme

- **Nommer les sommets** : les lettres sont attribuées automatiquement (A, B, C… puis
  A', B'…) sans jamais réutiliser un nom déjà pris. Elles se déplacent à la souris et
  se renomment par double-clic.
- **Codage des longueurs** : marques simples, doubles, triples, croix et cercles sur
  n'importe quelle arête (outil « Codage des longueurs », ou clic droit sur l'arête).
- **Codage automatique** : détecte les arêtes de même longueur dans toute la figure et
  leur attribue un codage cohérent.
- **Styles** : couleur, trait plein ou pointillé arête par arête, remplissage uni ou
  hachuré, opacité, ordre d'affichage (avant/arrière-plan).

### Aides au tracé

- Aimantation sur les sommets existants et sur la grille (maintenir <kbd>Maj</kbd>
  pour la désactiver ponctuellement).
- Grilles points, carreaux, isométrique, ou aucune.
- Zoom molette, déplacement à la molette ou <kbd>Espace</kbd> + glisser, recentrage
  automatique sur la figure.

## Exports

| Format | Usage |
|---|---|
| **SVG** | vectoriel, recadré sur la figure, réimportable dans Inkscape ou LibreOffice |
| **PDF** | vectoriel, une page recadrée sur la figure, libellés en vrai texte sélectionnable |
| **PNG** | rendu ×3 sur fond blanc, net à l'impression et au vidéoprojecteur |
| **Presse-papier** | l'image directement collable dans un traitement de texte |
| **TikZ** | document LaTeX complet, prêt à compiler |
| **`.geo`** | le projet lui-même, pour le rouvrir et le modifier plus tard |

Les exports reprennent les couleurs de la figure et ignorent la surbrillance de
sélection, la grille et les poignées d'édition.

Le PDF est écrit directement par l'application, sans bibliothèque : traits, courbes
de Bézier et hachures sont de vrais objets vectoriels, et le texte utilise une police
standard non embarquée. Seuls les caractères absents de l'encodage WinAnsi sont
remplacés par un point d'interrogation.

## Raccourcis clavier

| | |
|---|---|
| <kbd>Ctrl</kbd>+<kbd>Z</kbd> / <kbd>Ctrl</kbd>+<kbd>Y</kbd> | annuler / refaire |
| <kbd>Échap</kbd> | abandonner la figure en cours de construction |
| <kbd>Suppr</kbd> | supprimer la sélection |
| <kbd>Espace</kbd> + glisser | déplacer la vue |
| <kbd>Ctrl</kbd>+<kbd>+</kbd> / <kbd>−</kbd> / <kbd>0</kbd> | zoomer / dézoomer / recentrer |
| <kbd>Ctrl</kbd>+<kbd>S</kbd> / <kbd>Ctrl</kbd>+<kbd>O</kbd> | enregistrer / ouvrir un projet |
| <kbd>Maj</kbd> | désactiver l'aimant le temps d'un clic |
| <kbd>F1</kbd> | aide et raccourcis |

## Tablette et TBI

L'interface est pilotable au doigt et au stylet : appui pour dessiner, appui long
pour ouvrir les propriétés d'un objet, pincer pour zoomer, deux doigts pour se
déplacer.

## Sauvegarde automatique

La figure en cours est conservée dans le navigateur : fermer l'onglet par erreur ne
la perd pas, elle est rechargée à l'ouverture suivante. Pour archiver ou partager un
travail, utilisez malgré tout l'export `.geo`, seul format transférable d'une machine
à l'autre.

## Structure du projet

`index.html` contient tout : styles, balisage et logique.

- `Utils` — primitives de dessin SVG (marques de codage, croix, tangentes d'ellipse).
- `Solid` — classe de base : identité, sélection, couleur, étiquettes, translation.
- `FreePoint`, `Segment`, `PolyFace`, `FreeText` — objets plans.
- `Polyhedron` → `Prism`, `Pyramid` — solides à faces planes, avec détection des
  arêtes cachées par orientation des faces.
- `Cylinder`, `Cone`, `Sphere` — solides de révolution.
- `App` — état, historique, entrées pointeur/clavier, rendu et exports.

Chaque objet sait se sérialiser via `getData()` ; `App.loadState()` fait le chemin
inverse. C'est ce couple qui porte à la fois l'annulation, la sauvegarde automatique
et le format `.geo`.

## Licence

Creative Commons Attribution – Pas d'Utilisation Commerciale – Partage dans les
Mêmes Conditions 4.0 International (CC BY-NC-SA 4.0) — voir [LICENSE](LICENSE).
