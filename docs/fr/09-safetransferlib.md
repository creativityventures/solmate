# Chapitre 9 — SafeTransferLib : tolerer les jetons ERC20 non conformes

De nombreux jetons ERC20 en circulation ne respectent pas exactement la norme : certains ne retournent aucune valeur booleenne depuis `transfer`/`transferFrom` (par exemple l'USDT historique), d'autres retournent des donnees de taille incorrecte. Une interaction naive avec ces jetons via l'interface `IERC20` standard de Solidity peut echouer a decoder la valeur de retour et faire echouer toute la transaction meme quand le transfert a reellement reussi.

`SafeTransferLib.sol` contourne ce probleme en appelant les fonctions de transfert directement en assembleur bas niveau (`call`), puis en interpretant le succes de l'appel independamment de la presence ou de l'absence de donnees de retour : si l'appel a reussi et que les donnees de retour sont soit vides, soit un booleen vrai, l'operation est consideree comme reussie. L'avertissement en tete de fichier ("Use with caution! Some functions... knowingly create dirty bits at the destination of the free memory pointer") signale explicitement que cette optimisation manipule la memoire de facon non standard, un compromis assume au nom de la compatibilite et du gaz.

`safeTransferETH` applique le meme principe aux transferts d'ether natif : un simple `call` bas niveau avec verification du booleen de succes, plutot que `transfer`/`send` dont la limite de gaz fixe est aujourd'hui consideree fragile face a des contrats destinataires dont les couts de reception varient.

[Chapitre suivant : Auth et Owned, deux motifs de controle d acces](10-auth.md)
