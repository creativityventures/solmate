# Chapitre 12 — Les outils complementaires : CREATE3, SSTORE2 et LibString

Au-dela des jetons et du controle d'acces, Solmate fournit une poignee d'outils bas niveau plus specialises. `CREATE3.sol` combine `CREATE2` (deploiement a une adresse deterministe calculee a l'avance) avec un contrat intermediaire jetable, pour obtenir une adresse de deploiement qui ne depend plus du bytecode du contrat final — utile pour deployer la meme adresse sur plusieurs chaines meme quand le code differe legerement d'un reseau a l'autre.

`SSTORE2.sol` detourne le stockage de contrat (`SSTORE`, normalement reserve aux variables d'etat) en stockage de donnees arbitraires dans le **bytecode** d'un contrat jetable deploye juste pour les porter, puis relues via `EXTCODECOPY` : pour de grandes quantites de donnees rarement modifiees, cette approche peut couter significativement moins cher en gaz que le stockage classique en emplacements `SSTORE`.

`LibString.sol` et `MerkleProofLib.sol`, non detailles ici, completent la boite a outils : conversions de nombres en chaines de caracteres optimisees en gaz pour l'une, verification de preuves d'arbre de Merkle pour l'autre — un motif deja rencontre dans les parcours de distribution de recompenses d'autres protocoles de cette bibliotheque.

[Chapitre suivant : limites et perimetre](13-limites-et-perimetre.md)
