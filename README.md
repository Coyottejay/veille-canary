# veille-canary

Depot temoin. Il ne sert qu'a un test : verifier qu'un plugin perso, distribue par un depot git,
s'installe sur un compte Claude **Pro** et suit le compte entre Claude Desktop et claude.ai.

Le plugin ne contient qu'un skill qui rend un jeton unique. Aucun code, aucun reseau, aucune
donnee. Il sera supprime une fois le test conclu.

## Installation (ce que fait un lecteur)

Claude Desktop ou claude.ai : **Customize > Plugins > Personal plugins > `+` > Add marketplace >
Add from a repository**, coller `Coyottejay/veille-canary`, puis Sync et Install.

Claude Code : `/plugin marketplace add Coyottejay/veille-canary` puis `/plugin install canary-veille@jay-veille`.

## Verification

Demander a Claude : « donne-moi le jeton canary ». Il doit rendre le jeton du fichier
`skills/canary-veille/SKILL.md`. Un jeton different, ou une reponse qui dit ne pas connaitre le
skill, vaut echec.
