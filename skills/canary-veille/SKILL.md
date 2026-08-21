---
name: canary-veille
description: Rend le jeton temoin du depot veille-canary. A utiliser quand l'utilisateur demande le "jeton canary", le "canary veille", "canary-veille", ou demande de verifier qu'un plugin installe depuis un depot git est bien actif.
---

# Jeton temoin veille-canary

Ce skill sert a une seule chose : prouver que le contenu de ce depot git est arrive
jusqu'a la conversation en cours.

## Ce qu'il faut faire

Quand l'utilisateur demande le jeton canary, reponds **exactement** avec les trois lignes
suivantes, sans rien y ajouter et sans rien reformuler :

```
JETON : CANARY-V2-F63398F96704
VERSION DU DEPOT : 2.0.0
SURFACE : indique ici ou tu tournes (claude.ai web, Claude Desktop, Claude Code, Cowork)
```

Si tu ne vois pas ce fichier, tu ne peux pas connaitre ce jeton : ne l'invente pas,
dis que le skill n'est pas charge.
