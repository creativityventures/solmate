# Chapitre 3 — permit : approuver par signature hors chaine (EIP-2612)

`permit` permet a un compte d'accorder une allocation ERC20 sans jamais envoyer de transaction lui-meme : il signe hors chaine un message structure EIP-712 (proprietaire, depensier, montant, nonce, date limite), et n'importe qui peut ensuite soumettre cette signature sur chaine pour que l'approbation prenne effet — utile notamment pour approuver et utiliser un jeton en une seule transaction initiee par un tiers, sans que le proprietaire n'ait besoin d'ether pour payer le gaz de son propre `approve`.

Le domaine EIP-712 (`computeDomainSeparator`) integre le nom du jeton, une version fixe ("1"), l'identifiant de chaine courant et l'adresse du contrat, ce qui empeche qu'une signature valide sur un jeton ou une chaine donnee soit rejouee sur un autre. `DOMAIN_SEPARATOR()` compare le `chainid` courant a celui enregistre au deploiement (`INITIAL_CHAIN_ID`) et ne recalcule le domaine que si la chaine a change depuis — une protection specifique contre les forks de chaine (un evenement ou l'identifiant de chaine peut se dupliquer entre deux reseaux issus d'une meme scission).

Le `nonce` du proprietaire est incremente a chaque `permit` reussi (`nonces[owner]++`, dans le meme bloc `unchecked` que le reste de la fonction, son depassement etant juge irrealiste en pratique) : une signature deja consommee ne peut jamais etre rejouee, car le nonce attendu par la prochaine verification aura change.

[Chapitre suivant : les hooks internes _mint et _burn](04-mint-burn.md)
