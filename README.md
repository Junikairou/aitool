# NEXORA — Répertoire d'outils IA

Un répertoire web francophone qui cartographie les meilleurs outils d'intelligence artificielle du marché, classés par catégorie et enrichis de fiches détaillées (fonctionnalités, tarifs, guides d'utilisation, FAQ).

**Site en ligne :** https://junikairou.github.io/aitool/
**Dépôt :** https://github.com/Junikairou/aitool

---

## Aperçu rapide

- **~65 outils IA référencés** répartis en 8 catégories : rédaction, image, vidéo, audio, code, productivité, agents, chat.
- **Vraies icônes** des outils récupérées via le service favicon de Google.
- **Fiche détaillée par outil** : description, fonctionnalités, tarifs, guide « Comment utiliser », FAQ dédiée.
- **Ressources** : actualités IA, comparatifs, guides pas-à-pas.
- **Recherche instantanée** (Ctrl+K) et mode sombre / clair.
- **Prêt pour Google AdSense** (emplacements bannière, sidebar, natifs, page détail).

## Techno

Un seul fichier : `index.html`. Zéro build, zéro dépendance. HTML + CSS + JS vanilla, données inline dans le script. S'ouvre en local par simple double-clic ou s'héberge n'importe où (GitHub Pages, Netlify, Vercel, OVH…).

## Utilisation en local

```bash
git clone https://github.com/Junikairou/aitool.git
cd aitool
# double-clic sur index.html ou :
python -m http.server 8000
```

## Activer AdSense

Dans `index.html`, remplacer partout :
- `ca-pub-XXXXXXXXXXXXXXXX` par votre ID éditeur AdSense
- Chaque `data-ad-slot="XXXXXXXXXX"` par l'ID de bloc correspondant

Les annonces ne s'affichent que sur un site en ligne validé par Google (pas en local).

## Ajouter un outil

Dans `index.html`, ajouter une entrée dans le tableau `TOOLS` :

```js
{ id:'monoutil', name:'Mon Outil', category:'image', badge:'new',
  tagline:"Une phrase d'accroche.",
  website:'https://monoutil.com', tags:['Tag1','Tag2'],
  desc:"Description détaillée…",
  features:["Fonction 1","Fonction 2"],
  pricing:[{p:'Free',price:'0 $',d:'Version gratuite'}] }
```

Optionnellement, ajouter un `howto` + `faq` dédiés dans `EXTRA_INFO`.

## Licence & mentions

Projet personnel. Les logos et marques cités appartiennent à leurs propriétaires respectifs. Les tarifs affichés sont indicatifs — toujours vérifier sur le site officiel de chaque outil.
