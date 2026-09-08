# Chapitre 11 — ReentrancyGuard et FixedPointMathLib : deux utilitaires transverses

`ReentrancyGuard.sol` tient en moins de vingt lignes : un unique emplacement de stockage `locked` (initialise a 1 plutot qu'a 0, un detail qui economise du gaz car changer un emplacement de stockage de zero a une valeur non nulle coute plus cher que de changer entre deux valeurs non nulles), et un modificateur `nonReentrant` qui verrouille avant d'executer la fonction protegee et deverrouille juste apres. Le meme motif que le `nonReentrant` deja rencontre dans Uniswap v3, Aave v3 ou MakerDAO, ici reduit a sa plus simple expression.

`FixedPointMathLib.sol` fournit les operations de multiplication et division en virgule fixe deja rencontrees sous d'autres noms dans plusieurs parcours de ce compte (le `factor` d'Aave/Comet, le `WAD` de MakerDAO) : `mulWadDown`/`mulWadUp`/`divWadDown`/`divWadUp`, toutes construites sur `mulDivDown`/`mulDivUp`, des fonctions bas niveau qui evitent le depassement intermediaire d'un produit `x * y` avant division en travaillant directement sur 512 bits via l'astuce mathematique de Remco Bloemen (multiplication pleine precision par decomposition en mots de 256 bits), implementee ici entierement en assembleur pour le gaz minimal.

`SignedWadMath.sol`, non detaille ici, etend ces operations aux nombres signes, utile par exemple pour des calculs de decroissance de prix dans le temps (encheres neerlandaises) qui peuvent legitimement devenir negatifs avant d'etre plafonnes a zero par l'appelant.

[Chapitre suivant : les outils complementaires : CREATE3, SSTORE2, LibString](12-outils.md)
