# Chapitre 6 — deposit, mint, withdraw, redeem : quatre entrees, deux sens d arrondi

ERC4626 offre deux façons symetriques de deposer (`deposit`, ou l'appelant fixe le montant d'actifs et recoit un nombre de parts calcule ; `mint`, ou l'appelant fixe le nombre de parts souhaite et paie le montant d'actifs correspondant) et deux façons symetriques de retirer (`withdraw` fixe les actifs recus, `redeem` fixe les parts brulees). Chacune de ces quatre fonctions utilise une fonction de previsualisation dediee (`previewDeposit`, `previewMint`, `previewWithdraw`, `previewRedeem`) dont le sens d'arrondi est toujours choisi au benefice du vault et de ses detenteurs existants, jamais du deposant ou du sortant.

`deposit` verifie explicitement que les parts calculees ne sont pas nulles (`require(... != 0, "ZERO_SHARES")`) car `previewDeposit` arrondit vers le bas : un depot trop petit pourrait sinon faire perdre silencieusement des actifs a un deposant sans lui donner la moindre part en echange. `redeem` porte la meme verification symetrique cote actifs (`ZERO_ASSETS`) pour la meme raison. `mint` et `withdraw`, elles, arrondissent deja vers le haut par construction et n'ont donc pas besoin de cette garde.

Chaque fonction de depot transfere les actifs **avant** de frapper les parts (`safeTransferFrom` puis `_mint`), avec un commentaire explicite rappelant qu'inverser cet ordre exposerait a une reentrance possible avec des jetons de type ERC-777 dont les hooks de transfert s'executent avant que le solde ne soit effectivement debite.

[Chapitre suivant : l attaque par inflation, un risque assume](07-inflation.md)
