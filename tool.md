# AI Need Tools — Handoff (à donner à n'importe quelle IA)

Ce document sert de brief complet pour reprendre le projet depuis zéro avec n'importe quelle IA (Claude, ChatGPT, Gemini…). Il contient : le pitch, les règles, les emplacements à modifier, l'historique et le backlog.

---

## 0. Règles impératives (à respecter par toute IA sur ce projet)

- **Toujours poser des questions via `AskUserQuestion`** — peu importe quand, quitte à en poser 20. Même en cas de doute minuscule, même si tu penses avoir compris. Ça évite les allers-retours de correction.
- **Réduire au maximum la consommation de tokens** de l'utilisateur.
- **Être concis, clair, compréhensible et efficace** dans les propos.
- **Une modification du site impacte tous les comptes**, sauf preuve du contraire.
- **Toujours pousser sur GitHub** après une modification, sauf preuve du contraire.
- **Toute incohérence détectée doit être remontée en `AskUserQuestion`** avant d'agir.

---

## 1. Pitch du projet

Répertoire web francophone d'outils IA. Un seul fichier `index.html`, vanilla HTML/CSS/JS, aucune dépendance, aucun build. Monétisation prévue via Google AdSense. Hébergement gratuit via GitHub Pages.

- **Site :** https://aineedtools.com (domaine custom, voir `CNAME`) — sinon https://junikairou.github.io/aitool/
- **Repo :** https://github.com/Junikairou/aitool
- **Branche principale :** `main`
- **Compte GitHub :** `Junikairou`
- **Email git :** `jkairou@gmail.com`

## 2. Structure du dépôt

```
aitool/
├── index.html          # ~1900 lignes — TOUT est ici (HTML, CSS, JS, données)
├── ads.txt             # fichier AdSense (ID éditeur à mettre à jour)
├── CNAME               # domaine custom GitHub Pages (aineedtools.com)
├── README.md           # présentation courte du projet
└── tool.md             # ce document
```

## 3. Structure interne de `index.html`

| Zone | Lignes approx. | Rôle |
|---|---|---|
| `<style>` | 20 – 470 | Tous les styles CSS + variables de thème (dark/light) |
| `<body>` markup | 470 – 550 | Layout : sidebar, topbar, hero, home/detail/resource views, footer |
| `CATEGORIES` | ~555 | 8 catégories (id, label, icon) |
| `TOOLS` | ~575 – 1110 | Tableau des outils IA (id, name, category, tagline, website, desc, features, pricing…) |
| `EXTRA_INFO` | ~1115 – 1440 | Guides « Comment utiliser » + FAQ par outil (indexé par `id`) |
| `RESOURCES` | ~1690 – 1730 | Contenu des pages Actualités, Comparatifs, Guides |
| Render + logique | 1450 – 1929 | Rendu, recherche, thème, routing par hash |

## 4. Règles de contenu

### Ton
- Français, professionnel mais accessible, jamais marketing agressif.
- Pas de superlatifs vides (« révolutionnaire », « incontournable »).
- Tarifs indicatifs, préciser toujours qu'ils peuvent évoluer.

### Fiche outil (obligatoire)
Chaque entrée du tableau `TOOLS` doit contenir :

```js
{
  id: 'kebab-case-unique',
  name: 'Nom officiel',
  category: 'redaction' | 'image' | 'video' | 'audio' | 'code' | 'productivite' | 'agents' | 'chat',
  badge: 'hot' | 'new' | '',        // 'hot' = populaire, 'new' = récent
  tagline: "Une phrase d'accroche courte.",
  website: 'https://…',             // URL officielle (sert aussi au favicon)
  tags: ['Tag1', 'Tag2', 'Tag3'],   // 2 à 4 tags
  desc: "Paragraphe de description (2-3 phrases).",
  features: ["Fonction 1", "Fonction 2", "Fonction 3", "Fonction 4"], // 3-5 items
  pricing: [
    { p: 'Nom plan', price: 'X $/mois', d: 'Ce que couvre le plan' },
    // …
  ]
}
```

### Fiche outil (recommandé — pour l'affichage riche)
Ajouter aussi dans `EXTRA_INFO` :

```js
EXTRA_INFO = {
  'monoutil': {
    howto: [
      { t: "Méthode 1 : titre", steps: ["étape 1", "étape 2", "…"] },
      // …
    ],
    faq: [
      { q: "Question ?", a: "Réponse claire et concise." },
      // …
    ]
  }
}
```

### Règles techniques strictes
- **Guillemets JS** : si une chaîne contient une apostrophe (`d'usage`), utiliser des doubles guillemets `"…"`. Sinon guillemets simples `'…'`.
- **`id` unique** : jamais deux outils avec le même `id`, jamais deux clés dupliquées dans `EXTRA_INFO`.
- **Icônes** : générées automatiquement via `https://www.google.com/s2/favicons?domain=…&sz=128` à partir de `website`. Pas d'image à uploader.
- **Pas de dépendance externe** : ne pas ajouter de librairie JS/CSS.

## 5. Fonctionnalités déjà en place

- 8 catégories, ~65 outils.
- Vraies favicons + fallback initiales sur dégradé.
- Recherche instantanée (nom, tagline, tags).
- Mode sombre / clair.
- Fiche détaillée : description, fonctionnalités, comment utiliser, tarifs, FAQ, outils similaires.
- 3 pages Ressources fonctionnelles : Actualités, Comparatifs (avec tableaux), Guides.
- Routing par hash (`#tool-<id>`), navigation back/forward navigateur.
- Emplacements AdSense : bannière haut, sidebar, milieu de flux, carte native dans grille, colonne latérale de détail.
- Responsive (breakpoint 960 px, sidebar en menu burger).

## 6. À faire (backlog)

Priorité haute
- [ ] Configurer les vrais IDs AdSense (`ca-pub-…` + `data-ad-slot`) après validation Google.
- [ ] Compléter `ads.txt` avec l'ID éditeur AdSense.
- [ ] Activer GitHub Pages sur la branche `main`.

Priorité moyenne
- [ ] Ajouter les catégories manquantes : SEO, éducation, santé, finance, juridique.
- [ ] Compléter `EXTRA_INFO` (howto + FAQ) pour les outils qui n'en ont pas encore.
- [ ] Rendre la newsletter réelle (bouton « Soumettre un outil » → formulaire Netlify Forms ou Formspree).
- [ ] Système de tri : par popularité, par prix, par date d'ajout.
- [ ] Page « À propos » et mentions légales / CGU / RGPD.

Priorité basse / idées
- [ ] Score / note communautaire par outil.
- [ ] Section « Nouveautés de la semaine ».
- [ ] Sitemap.xml auto pour le SEO.
- [ ] Version anglaise (i18n).
- [ ] Migration vers données externes (JSON) si le fichier dépasse 3000 lignes.

## 7. Historique des grandes modifications

| Date | Commit | Contenu |
|---|---|---|
| 2026-07-29 | `225a5b7` | +25 outils, favicons réels, ressources fonctionnelles, howto + FAQ par outil, suppression `files.zip` |
| — | `67423c5` | Version initiale complète (~40 outils, thème dark/light, AdSense placeholders) |

## 8. Commandes utiles

```bash
# Lancer un serveur local
python -m http.server 8000

# Commit + push
git add -A
git commit -m "Message"
git push origin main
```

## 9. Comment reprendre avec une nouvelle IA

Copier-coller ce texte dans le premier message :

> Je travaille sur AI Need Tools, un répertoire d'outils IA en un fichier `index.html` vanilla. Lis `tool.md` et `README.md` dans le dépôt pour tout le contexte. Suis strictement les règles de contenu et techniques (guillemets JS, id unique, pas de dépendance). Ma tâche : [décrire].
