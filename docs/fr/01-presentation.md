# Chapitre 1 — Presentation de Solmate

Solmate n'est pas un protocole applicatif comme les autres parcours de cette bibliotheque : c'est une collection de briques de base ("building blocks") reutilisables pour ecrire des contrats Solidity — jetons ERC20/ERC721/ERC4626/ERC1155/ERC6909, controle d'acces, protection contre la reentrance, mathematiques en virgule fixe. Son readme la resume en trois mots : "modern, opinionated, and gas optimized".

Le trait distinctif de Solmate, par rapport aux implementations plus prudentes d'OpenZeppelin, est d'assumer explicitement des compromis de securite pour gagner en gaz : moins de verifications explicites (`require`), des blocs `unchecked` pour desactiver la protection anti-depassement de Solidity 0.8 quand une invariante mathematique rend le depassement impossible, une gestion volontairement minimaliste de certains standards. Chaque compromis est documente par un commentaire au fil du code, jamais laisse implicite.

Ce parcours s'appuie sur le depot cloné a la date d'ecriture. Fichiers centraux : `src/tokens/ERC20.sol`, `src/tokens/ERC721.sol`, `src/tokens/ERC4626.sol`, `src/auth/Auth.sol` et `Owned.sol`, `src/utils/SafeTransferLib.sol`, `src/utils/ReentrancyGuard.sol`, `src/utils/FixedPointMathLib.sol`.

Rien n'a ete installe, compile ni execute pour ecrire ces chapitres.

[Chapitre suivant : ERC20, le coeur gas-optimise](02-erc20.md)
