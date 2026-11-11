# Modéliser son terrain dans SketchUp pour JARDIN

JARDIN peut reprendre le terrain, les zones de sol et les constructions dessinés dans SketchUp. Ce guide explique comment préparer le modèle, peindre les zones et exporter.

Il faut SketchUp 2024 ou plus récent et l’extension **Export JARDIN**.

## Installer l’extension

1. Télécharger `jardin_export.rbz` depuis la [dernière version](https://github.com/paulox-nol/JARDIN-app/releases/latest).
2. Dans SketchUp : **Extensions → Gestionnaire d’extensions → Installer l’extension**, puis choisir le fichier `.rbz`.
3. Le menu **Extensions → JARDIN** apparaît, avec trois commandes :

| Commande | Effet |
| --- | --- |
| Créer les matières JARDIN | Ajoute les matières de sol avec leur couleur. Celles qui existent déjà ne sont pas modifiées. |
| Vérifier le modèle pour JARDIN | Contrôle le modèle et affiche un compte rendu. Rien n’est écrit ni modifié. |
| Exporter pour JARDIN… | Fait les mêmes contrôles, puis écrit le fichier à ouvrir dans JARDIN. |

## En bref

1. Placer l’origine des axes au milieu du jardin.
2. Ranger le modèle en deux groupes : `JARDIN_TERRAIN` et `JARDIN_OBJETS`.
3. Créer les matières (**Extensions → JARDIN → Créer les matières JARDIN**).
4. Découper le terrain le long des limites de zones, puis peindre chaque face.
5. Nommer chaque objet.
6. **Exporter pour JARDIN…**, puis, dans JARDIN, **Importer SketchUp…**

## 1. L’origine, le nord et le lieu

- L’origine des axes de SketchUp devient le point de départ de JARDIN. Choisir un point fixe **à l’intérieur du terrain**, par exemple un angle de la maison. Pour déplacer les axes sans bouger le dessin : clic droit sur les axes → **Placer**.
- **Ne plus déplacer l’origine** une fois des arbres plantés dans JARDIN : ils seraient décalés d’autant.
- Le terrain peut avoir n’importe quelle forme, dans un carré de **150 × 150 m** au plus. Hors de ses faces, on ne peut ni planter ni tracer d’espace.
- **Nord et lieu** : régler le nord avec la barre d’outils *Nord solaire*, et le lieu dans **Fenêtre → Infos sur le modèle → Géolocalisation**. JARDIN les reprend pour le soleil et les ombres.

## 2. Ranger le modèle

Dans la fenêtre **Structure**, au premier niveau du modèle :

| Groupe | Contenu |
| --- | --- |
| `JARDIN_TERRAIN` | Uniquement les faces du sol (maillage du bac à sable, triangulé ou non). Pas de murs. |
| `JARDIN_OBJETS` | Facultatif. Un groupe ou composant **nommé** par objet : maison, clôture, portail, abri… |

Tout le reste du modèle (personnages, cotes, essais) est ignoré. Les **faces verticales** (muret, marche, soutènement) ne vont pas dans le terrain : JARDIN lit le sol comme une seule hauteur par point. Les ranger dans un objet, par exemple « Muret du potager ».

## 3. Peindre le terrain : les zones

Chaque zone de sol est une matière SketchUp. **C’est le nom de la matière qui compte** : il dit à JARDIN quel sol dessiner (herbe, chemin, eau…). La couleur sert seulement à voir dans SketchUp à peu près l’aspect qu’aura le jardin en été.

| Nom de la matière | Zone dans JARDIN | Aspect en été | R, V, B | Hexa |
| --- | --- | --- | --- | --- |
| `sol-herbe` | Pelouse, prairie, clairière | herbe vert-jaune, fleurs blanches | 161, 166, 99 | `#A1A663` |
| `sol-foret` | Sol de forêt | vert olive sombre, feuilles mortes | 89, 105, 53 | `#596935` |
| `sol-chemin` | Chemin de terre ou de gravier | gris-beige pâle, bordure herbeuse | 187, 186, 169 | `#BBBAA9` |
| `sol-asphalte` | Asphalte | gris anthracite | 98, 102, 98 | `#626662` |
| `sol-beton` | Béton, dallage | pour l’instant comme l’asphalte | 98, 102, 98 | `#626662` |
| `sol-eau` | Ruisseau, mare | bleu-vert animé, berge sombre | 43, 91, 101 | `#2B5B65` |
| `sol-roche` | Roche affleurante | strates gris-beige, mousse | 155, 148, 126 | `#9B947E` |

La commande **Créer les matières JARDIN** les ajoute toutes avec ces couleurs.

**Variantes** : ajouter un tiret et un mot, par exemple `sol-herbe-prairie`, `sol-herbe-pelouse` ou `sol-eau-mare`. Chaque variante devient une zone séparée dans JARDIN, avec ses propres réglages de décor (densité d’herbe, de fleurs, de pierres…). Elle se dessine comme sa famille : lui donner la même couleur ou une nuance proche. Noms en minuscules, sans accent ni espace.

**Textures** : inutile d’en mettre sur le terrain. JARDIN ne lit que le nom de la matière et dessine lui-même l’herbe, les fleurs, la litière, les pierres, les berges, l’ombre au pied des arbres et la neige en hiver, selon la saison.

### Règles de peinture

- **Peindre les faces elles-mêmes**, pas le groupe.
- **Toutes les faces du terrain doivent être peintes** avec une matière `sol-…`. Une face oubliée, ou peinte d’une autre matière, bloque l’export : l’extension sélectionne alors les faces en cause pour les montrer.
- **Découper avant de peindre** : une zone suit les arêtes du maillage. Dessiner le contour du chemin ou de la mare à plat au-dessus du terrain, puis **Bac à sable → Projeter** sur le terrain, et peindre l’intérieur. Sans découpage, un chemin étroit traversant de grands triangles disparaît en partie.
- **Largeur minimale conseillée : 50 cm.** L’herbe déborde un peu sur les bords des revêtements.
- Pour vérifier : **Affichage → Style de face → Ombré**. Une face blanche ou bleu-gris n’est pas peinte.

## 4. Les objets

### Nommer

- **Un objet = un groupe ou un composant placé directement dans `JARDIN_OBJETS`.** Ce qu’il contient n’a pas besoin de nom.
- Le nommer dans **Infos sur l’entité → Nom d’instance**, avec un **nom unique** qui dit quoi et où : « Maison », « Clôture sud », « Abri 1 », « Abri 2 »…
- **Regrouper ce qui forme un tout** : tous les poteaux et lisses d’une clôture dans un seul groupe « Clôture sud ».
- Renommer ou déplacer un objet ne casse rien : JARDIN le reconnaît. Supprimer puis redessiner, ou copier-coller, crée un nouvel objet.
- **Dallage ou terrasse au sol** : à fleur de terrain, c’est une zone `sol-beton`. Surélevé (terrasse sur plots, marches), c’est un objet.

### Couleurs et textures des objets

- JARDIN reprend **la couleur de chaque face**, quel que soit le nom de la matière, et l’éclaire avec son soleil.
- **Une texture est remplacée par sa couleur moyenne** : une façade en briques texturées devient une façade brique unie. Un verre transparent reste transparent.
- Une face non peinte prend la couleur de son groupe s’il est peint, sinon un blanc cassé.
- Palette conseillée, mate et proche du style de JARDIN (facultative) :

| Matière | R, V, B | Hexa |
| --- | --- | --- |
| Crépi, enduit | 217, 210, 195 | `#D9D2C3` |
| Tuile | 154, 78, 54 | `#9A4E36` |
| Ardoise, zinc | 94, 98, 102 | `#5E6266` |
| Pierre | 179, 170, 150 | `#B3AA96` |
| Bois naturel | 156, 122, 84 | `#9C7A54` |
| Bois sombre, lasure | 91, 69, 50 | `#5B4532` |
| Métal peint (portail, clôture) | 63, 74, 68 | `#3F4A44` |
| Verre (opacité 35 %) | 169, 195, 196 | `#A9C3C4` |

### Alléger

- Utiliser des **composants** pour ce qui se répète (poteaux, lames, piquets) : ils sont envoyés une seule fois.
- L’extension avertit au-delà de **50 000 triangles par objet** et de **150 000 au total**. Remplacer les modèles téléchargés très détaillés (voitures, mobilier) par des volumes simples, puis **Infos sur le modèle → Statistiques → Purger les éléments inutilisés**.
- Ce qui est **masqué** (géométrie ou balise cachée) n’est pas exporté : pratique pour écarter un objet sans le supprimer.

## 5. Vérifier et exporter

Lancer **Extensions → JARDIN → Vérifier le modèle pour JARDIN**. Une **erreur** bloque l’export et sélectionne les faces en cause ; un **avertissement** laisse le choix.

| Contrôle | Effet |
| --- | --- |
| Groupe `JARDIN_TERRAIN` absent | Erreur |
| Groupe `JARDIN_OBJETS` absent | Avertissement : terrain seul |
| Face du terrain non peinte, ou matière hors liste | Erreur |
| Faces du terrain superposées | Erreur |
| Terrain de plus de 150 m de côté | Erreur |
| Objet sans nom, ou deux objets du même nom | Erreur |
| Face presque verticale dans le terrain | Avertissement : remplacée par une pente raide |
| Origine des axes hors du terrain | Avertissement |
| Face peinte seulement au dos | Avertissement |
| Zone plus étroite que 50 cm | Avertissement |
| Objet trop lourd, masqué ou vide | Avertissement |

Quand tout est bon : **Extensions → JARDIN → Exporter pour JARDIN…** L’extension écrit un seul fichier `<nom du modèle>.jardin-sketchup.json`, à l’endroit choisi.

## 6. Importer dans JARDIN

- **Premier import** : dans JARDIN, **Échap → Réglages → Importer SketchUp…**, choisir le fichier, lire le bilan, puis **Appliquer le site**. Le terrain, les zones et les objets apparaissent. **Enregistrer** les inclut dans le fichier `.jardin`, qui se suffit ensuite à lui-même.
- **Faire évoluer le modèle** : modifier dans SketchUp, réexporter, puis **Réimporter SketchUp…** JARDIN affiche ce qui a changé (objets ajoutés, déplacés ou retirés, zones nouvelles, arbres désormais hors du terrain ou sur l’eau…) avant d’appliquer. Les arbres, fiches et espaces de gestion restent en place.
- **Garder les mêmes axes et les mêmes noms de matières** d’un export à l’autre. Renommer une matière crée une nouvelle zone ; JARDIN propose alors de reprendre les réglages de l’ancienne.
- Les décors de chaque zone se règlent ensuite dans **Jardin → Sol du site SketchUp**, saison par saison.

## Limites actuelles

- Une paroi verticale (ressaut de roche) devient une pente raide.
- Béton et asphalte ont le même aspect.
