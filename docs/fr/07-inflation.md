# Chapitre 7 — Un risque assume : pas de protection native contre l attaque par inflation

A la difference de la bibliotheque `SharesMathLib` de Morpho Blue (egalement documentee pour ce compte), qui ajoute systematiquement des parts et actifs virtuels a chaque conversion pour neutraliser l'attaque par inflation d'un vault ERC-4626 fraichement cree, l'implementation de Solmate ne comporte aucune protection de ce type : `convertToShares` sur un vault vide retourne les actifs deposes comme nombre de parts, point final, sans offset protecteur.

Cela signifie qu'un attaquant pourrait, en theorie, deposer un montant minimal pour obtenir la premiere part puis transferer directement des actifs au vault (hors de la fonction `deposit`) pour gonfler artificiellement `totalAssets()` par rapport a `totalSupply`, faisant perdre par arrondi une part significative de la valeur des deposants suivants. Solmate documente cette classe de risques ailleurs dans le depot (README et commentaires des tests) mais ne l'empeche pas dans le contrat lui-meme.

Ce choix illustre bien la philosophie generale de Solmate resumee au chapitre 1 : fournir la brique la plus simple et la moins couteuse en gaz possible, a charge pour le contrat qui l'integre de decider s'il a besoin d'une protection supplementaire (par exemple en deposant lui-meme une petite quantite d'actifs a l'initialisation du vault) plutot que de payer systematiquement le cout de cette protection meme quand elle n'est pas necessaire.

[Chapitre suivant : ERC721, un NFT minimaliste](08-erc721.md)
