# VOID.SYNDICATE

Site vitrine statique, esthétique "dossier classifié" — ticker en direct, fil d'actualités, veille cyber, prestations et présentation d'équipe.

> ⚠️ Projet de fiction à but pédagogique. Aucune entité, groupe ou victime réelle n'est impliquée.

---

## 🖥️ Aperçu

Une seule page (`index.html`), scroll fluide entre 5 sections : hero, actualités, veille, services, équipe. Pas de framework, pas de build — HTML/CSS statique pur, pensé pour tourner n'importe où sans dépendance.

<img width="1823" height="935" alt="image" src="https://github.com/user-attachments/assets/6934524d-ff0a-4855-bcb3-9c612e15fade" />

---

## 📁 Structure du repo

```
.
├── index.html      # structure et contenu de la page
├── style.css       # design system complet (couleurs, typo, layout, animations)
└── README.md
```

Les fichiers sont volontairement séparés (contenu / présentation) plutôt que fusionnés en un seul fichier, pour rester lisible et faciliter les futures modifs de design sans toucher au markup.

---

## 🎨 Design system

**Palette** — définie en variables CSS (`:root`) dans `style.css` :

| Variable | Valeur | Usage |
|---|---|---|
| `--void` | `#0b0b0d` | fond principal |
| `--panel` | `#141416` | fond des blocs (veille, cartes équipe) |
| `--paper` | `#1c1c1f` | surfaces secondaires, hover |
| `--line` | `#26262a` | bordures, séparateurs |
| `--bone` | `#e8e6e1` | texte principal |
| `--dim` | `#8a8a8f` | texte secondaire |
| `--blood` | `#b8323f` | accent principal (tags, liens actifs, tampon) |
| `--amber` | `#d98f2b` | accent secondaire (métadonnées, ticker) |

**Typographie** — deux familles seulement :
- `Georgia / Times New Roman` (serif) pour le corps de texte → registre "rapport", lisible et posé.
- `Courier New` (monospace) pour tout ce qui relève de la donnée brute : dates, tags, ticker, rôles d'équipe, numérotation des services → registre "terminal / dossier technique".

Ce contraste serif/mono porte toute l'identité visuelle : le texte "humain" en serif, la donnée "système" en mono.

---

## 🧩 Détail des sections (`index.html`)

### `#ticker`
Bandeau défilant en haut de page. Le défilement est géré en CSS pur : le `<span>` interne est dupliqué visuellement par un `padding-left: 100%` et animé via `@keyframes scroll` (translation de `0` à `-100%`). Aucun JS nécessaire.

### `nav`
Barre de navigation sticky (`position: sticky; top:0`) avec `backdrop-filter: blur(6px)` pour un effet de flou au scroll — nécessite un fond semi-transparent (`rgba(11,11,13,0.92)`) pour fonctionner.

### `#hero`
Titre principal + accroche + 3 métriques clé (`.hero-meta`). Le tampon rouge (`.stamp`) utilise `transform: rotate(-3deg)` pour casser la rigidité de la grille et évoquer un tampon physique sur un dossier papier.

### `#actus`
Liste d'actualités en grille CSS `120px 1fr` (date à gauche, contenu à droite) — chaque `.news-item` est une entrée indépendante, facile à dupliquer pour ajouter une actu.

### `#veille`
Grille 2 colonnes (`.feed`) de brèves de veille cyber, fond `--panel` pour distinguer visuellement cette section du reste de la page.

### `#services`
Grille responsive (`auto-fit, minmax(250px,1fr)`) de 4 prestations numérotées. Le fond de la grille (`--line`) sert de bordure entre les cellules sans avoir à gérer des `border` individuelles — technique du "gap coloré".

### `#equipe`
Cartes membres avec avatar généré en CSS pur (`repeating-linear-gradient` en diagonale + glyphe unicode centré). Aucune image externe : les avatars sont 100% CSS/texte, ce qui évite toute dépendance et garde le site auto-suffisant.

---

## 🔧 Faire tourner le site en local

Aucune installation requise :

```bash
# Option 1 — ouvrir directement
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows

# Option 2 — via un serveur local (recommandé pour éviter les soucis de chemins relatifs)
python3 -m http.server 8000
# puis ouvrir http://localhost:8000
```

---

## ✏️ Modifier le contenu

- **Ajouter une actu** → dupliquer un bloc `.news-item` dans `#actus`.
- **Ajouter une brève de veille** → dupliquer un bloc `.feed-item` dans `#veille`.
- **Ajouter un membre** → dupliquer un bloc `.member` dans `#equipe`, changer le glyphe (`.avatar-glyph`), le rôle et le pseudo.
- **Changer la palette** → tout est centralisé dans `:root` en haut de `style.css`, aucune couleur n'est codée en dur ailleurs dans les composants.

---

## 📱 Responsive

Un seul breakpoint (`max-width: 720px`) suffit ici : la grille des news passe en une colonne, celle de la veille aussi, et les paddings de section sont resserrés. Le reste (services, équipe) utilise déjà des grilles `auto-fit`, donc elles s'adaptent nativement sans media query dédiée.
