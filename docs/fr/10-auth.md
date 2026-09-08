# Chapitre 10 — Auth et Owned : deux motifs de controle d acces, du plus simple au plus flexible

Solmate propose deux motifs distincts de controle d'acces, a choisir selon le besoin. `Owned.sol` est le plus simple : une seule adresse `owner`, un modificateur `onlyOwner`, une fonction de transfert de propriete — suffisant pour la grande majorite des contrats qui n'ont besoin que d'un unique administrateur.

`Auth.sol` va plus loin : au lieu de coder en dur la logique d'autorisation, chaque contrat qui en herite delegue la decision a un contrat externe interchangeable, une `Authority`, via `isAuthorized`. Le modificateur `requiresAuth` verifie d'abord cette autorite externe puis, seulement si elle refuse, verifie si l'appelant est le proprietaire — un ordre delibere justifie par un commentaire : verifier l'autorite en premier permet de changer dynamiquement les permissions sans jamais avoir a modifier le contrat protege lui-meme, meme pour retirer les privileges du proprietaire s'il le souhaite.

`setAuthority`, elle, verifie l'inverse en premier (le proprietaire, puis l'autorite courante) : le commentaire associe explique que cet ordre garantit que le proprietaire peut toujours remplacer une autorite meme si celle-ci est devenue defaillante ou consomme trop de gaz — une clause de secours volontaire pour ne jamais rester bloque avec une autorite cassee. `RolesAuthority`/`MultiRolesAuthority`, dans `src/auth/authorities/`, fournissent des implementations concretes d'`Authority` basees sur des roles numerotes, hors du detail de ce parcours.

[Chapitre suivant : ReentrancyGuard et la mathematique en virgule fixe](11-reentrancy.md)
