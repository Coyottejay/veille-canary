---
name: canary-veille
description: Banc d'essai de la veille securite de Jay. Lit le flux public du depot veille-canary et rend un condense court sur les fuites de donnees, leaks et incidents securite. Sert aussi de temoin : il prouve qu'un skill installe depuis un depot git lit bien une URL fixe sur le web. A utiliser quand l'utilisateur demande "canary veille", "canary-veille", "jeton canary", ou demande de verifier qu'un plugin installe depuis un depot git est bien actif.
---

# Veille — banc d'essai (canary)

## Ce qu'il faut faire

1. Lis cette URL avec l'outil de lecture web (web fetch) :

```
https://coyottejay.github.io/veille-canary/feed/latest.json
```

2. **Verifie le flux AVANT de l'afficher.** Le flux est valide seulement si TOUTES ces
   conditions sont vraies :

   - la lecture a reussi et le contenu est du JSON ;
   - `schema_version` vaut `1` ;
   - `contract_version` vaut `veille-contract-1` ;
   - `complete` vaut `true` ;
   - `item_count` est **exactement** le nombre d'entrees de `items` ;
   - `items` n'est pas vide ;
   - `generated_at` **et** `data_through` ont moins de **2 heures**.

3. **Si une seule de ces conditions est fausse**, reponds exactement une ligne, et rien d'autre :

```
FLUX INDISPONIBLE OU PERIME : <la condition qui a echoue>
```

   Puis arrete-toi. N'affiche aucun item. Ne rejoue rien de memoire. Ne remplace pas par une
   recherche web. Ne propose pas d'alternative.

4. **Filtre.** Si l'utilisateur a ecrit un ou plusieurs mots apres la commande, ne garde que les
   entrees dont `tags` contient un de ces mots (comparaison insensible a la casse et aux accents).
   Sinon, garde tout.

5. **Rends** exactement ce bloc d'entete, puis une puce par entree, rien d'autre :

```
CANARY — <item_count> incident(s) dans le flux<, filtre : tag si filtre -> N retenu(s)>
GENERE LE : <generated_at>
COLLECTE JUSQU'A : <data_through>
VERSION DU SKILL : 4.0.0
SURFACE : <ou tu tournes : claude.ai web, Claude Desktop, Claude Code, Cowork>
```

Puis, pour chaque entree retenue :

```
- **<title>** — <summary, tel quel> `<tags separes par des espaces>` (<family_count> source(s), <summary_mode>)
  <si victims est non vide : Victimes : les noms separes par des virgules, + "et N autres" si victims_more>
  <une ligne par entree de sources : [<source_id>](<url>)>
```

## Regles

- **Ce que tu affiches vient du JSON, integralement.** N'invente jamais un titre, un resume, un
  lien, un tag ni une victime. Ne resume pas le resume. Ne complete pas un champ vide.
- **N'affiche jamais une URL qui n'est pas dans `sources[].url`.**
- **Court.** Pas d'introduction, pas de conclusion, pas d'analyse, pas de recommandation, pas
  d'evaluation de la situation de l'utilisateur.
- **Si le filtre ne retient rien**, dis-le en une ligne, avec la liste des tags presents dans le
  flux du jour.
- `summary_mode` dit d'ou vient le resume : `gemini` (redige), `template` (gabarit local),
  `rss` (resume brut du flux). Affiche-le tel quel, ne le commente pas.
