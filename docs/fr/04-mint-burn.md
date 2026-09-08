# Chapitre 4 — Les hooks internes _mint et _burn

`_mint` et `_burn` sont des fonctions internes, jamais exposees publiquement par `ERC20.sol` lui-meme : c'est au contrat qui herite d'`ERC20` de decider quand et sous quelles conditions creer ou detruire des jetons (droits d'acces, limites, evenements metier). Ce choix de conception delegue toute la logique de politique monetaire au contrat derive, tandis que Solmate ne fournit que la mecanique comptable minimale (mise a jour de `totalSupply` et `balanceOf`, emission de l'evenement `Transfer` standard avec l'adresse zero comme origine ou destination).

Comme pour `transfer`, les incrementations/decrementations qui accompagnent `_mint`/`_burn` sont enveloppees dans des blocs `unchecked` justifies par la meme invariante globale : la somme des soldes ne peut jamais depasser `totalSupply`, donc si le solde d'un compte est preleve avant que `totalSupply` ne soit lui-meme decremente dans `_burn`, ce dernier ne peut pas sous-deborder.

Ce commentaire de tete de fichier, "Do not manually set balances without updating totalSupply", resume le contrat implicite entre `ERC20.sol` et ses contrats derives : toute manipulation directe de `balanceOf` en dehors de `_mint`/`_burn`/`transfer`/`transferFrom` romprait l'invariante dont dependent les optimisations `unchecked` de tout le fichier.

[Chapitre suivant : ERC4626, l interface commune des vaults](05-erc4626.md)
