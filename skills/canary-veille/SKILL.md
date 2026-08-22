---
name: canary-veille
description: Lit le flux de veille public de Jay et rend un condense court sur les fuites de donnees, leaks, incidents securite. Sert aussi de test - il prouve qu'un skill installe depuis un depot git arrive a lire une URL fixe sur le web. A utiliser quand l'utilisateur demande "veille", "jeton canary", "canary veille", ou demande de verifier qu'un plugin installe depuis un depot git est bien actif.
---

# Veille — flux public

## Ce qu'il faut faire

1. Recupere l'URL suivante avec l'outil de recherche/lecture web (web fetch) :

```
https://coyottejay.github.io/veille-canary/feed/latest.json
```

2. C'est un JSON. Il contient `generated_at`, `canary`, et `items[]`
   (`title`, `summary`, `url`, `tags`).

3. Si l'utilisateur a donne un mot apres la commande, ne garde que les items dont `tags`
   contient ce mot. Sinon, garde tout.

4. Reponds **exactement** dans ce format, sans rien ajouter :

```
CANARY DU FLUX : <la valeur du champ canary, telle quelle>
GENERE LE : <la valeur de generated_at>
VERSION DU SKILL : 3.0.0
SURFACE : <ou tu tournes : claude.ai web, Claude Desktop, Claude Code, Cowork>
ITEMS : <nombre d'items retenus>
```

Puis, pour chaque item retenu, une puce :

```
- **<title>** — <summary en une phrase> [lien](<url>) `<tags separes par des espaces>`
```

## Regles

- La valeur de `canary` **n'est pas dans ce fichier**. Le seul moyen de la connaitre est
  d'aller lire l'URL. Ne l'invente jamais.
- Si la lecture de l'URL echoue, dis-le en une ligne : `ECHEC : <la raison>`. N'invente
  aucun contenu, ne remplace pas par une recherche web generale.
- Court. Pas d'analyse, pas de recommandation, pas de conclusion.
