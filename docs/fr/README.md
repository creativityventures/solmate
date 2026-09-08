# Parcours francais de Solmate — Standards de tokens (ERC20)

Lecture commentee de la bibliotheque de briques Solidity Solmate, en francais, un mecanisme par chapitre.
Aucun code n'a ete installe, compile ni execute : ce parcours est purement documentaire.

1. [Presentation de Solmate](01-presentation.md)
2. [ERC20 : transfer, approve et l invariante de solde implicite](02-erc20.md)
3. [permit : approuver par signature hors chaine (EIP-2612)](03-permit.md)
4. [Les hooks internes _mint et _burn](04-mint-burn.md)
5. [ERC4626 : l interface commune des vaults tokenises](05-erc4626.md)
6. [deposit, mint, withdraw, redeem : quatre entrees, deux sens d arrondi](06-deposit-withdraw.md)
7. [Un risque assume : pas de protection native contre l attaque par inflation](07-inflation.md)
8. [ERC721 : un jeton non fongible minimaliste](08-erc721.md)
9. [SafeTransferLib : tolerer les jetons ERC20 non conformes](09-safetransferlib.md)
10. [Auth et Owned : deux motifs de controle d acces, du plus simple au plus flexible](10-auth.md)
11. [ReentrancyGuard et FixedPointMathLib : deux utilitaires transverses](11-reentrancy.md)
12. [Les outils complementaires : CREATE3, SSTORE2 et LibString](12-outils.md)
13. [Limites connues et perimetre de ce parcours](13-limites-et-perimetre.md)
