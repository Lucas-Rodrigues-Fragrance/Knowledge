# Guide — Connecter Obsidian à ce dépôt via le plugin Obsidian Git

Ce guide vous permet de synchroniser automatiquement votre coffre Obsidian avec
ce dépôt GitHub. Une fois en place, chaque modification de vos notes pourra être
envoyée ici, où je pourrai les lire, les organiser et les enrichir.

---

## A. Choisir votre situation de départ

**Cas 1 — Vous partez de zéro (pas encore de coffre, ou coffre vide)**
→ Clonez ce dépôt et ouvrez-le comme coffre. Suivez la **section B**.

**Cas 2 — Vous avez déjà un coffre Obsidian rempli de notes**
→ Vous allez transformer votre coffre existant en dépôt relié à celui-ci.
Suivez la **section C**. (Recommandé pour ne rien perdre.)

---

## B. Cas 1 — Repartir de ce dépôt (coffre neuf)

1. Installez **Git** sur votre machine si ce n'est pas déjà fait
   (https://git-scm.com).
2. Clonez le dépôt dans un dossier de votre choix :
   ```bash
   git clone <URL_DU_DEPOT> Knowledge
   ```
3. Dans Obsidian → *Open another vault* → *Open folder as vault* → choisissez
   le dossier `Knowledge`.
4. Passez ensuite à la **section D** (installation du plugin).

---

## C. Cas 2 — Relier votre coffre existant

1. Installez **Git** sur votre machine (https://git-scm.com).
2. Ouvrez un terminal **dans le dossier de votre coffre** existant, puis :
   ```bash
   git init
   git remote add origin <URL_DU_DEPOT>
   git fetch origin
   # Récupère le squelette (README, .gitignore, dossiers) sans écraser vos notes :
   git merge origin/main --allow-unrelated-histories
   ```
   > En cas de conflit, conservez vos versions : vos notes priment toujours.
3. Passez à la **section D**.

---

## D. Installer et configurer le plugin Obsidian Git

1. Dans Obsidian : *Paramètres* → *Options des modules complémentaires (Community
   plugins)* → activez les modules → *Browse*.
2. Cherchez **« Obsidian Git »** (auteur : Vinzent), installez-le, puis activez-le.
3. Ouvrez les paramètres du plugin et réglez (suggestions) :
   - **Vault backup interval (minutes)** : `10` (commit + push automatique).
   - **Auto pull on startup** : activé (récupère les modifications faites ici).
   - **Commit message** : `vault backup: {{date}}` (par défaut, convient).
4. Authentification GitHub : la première synchro vous demandera vos identifiants.
   Utilisez un **Personal Access Token** GitHub (Settings → Developer settings →
   *Fine-grained tokens*) avec accès *Contents: Read and Write* sur ce dépôt.

---

## E. Vérifier que ça marche

1. Créez une note de test, par ex. `00-Inbox/test-sync.md`.
2. Lancez la commande Obsidian (Ctrl/Cmd+P) → **« Obsidian Git: Commit-and-sync »**.
3. Rafraîchissez ce dépôt sur GitHub : la note doit apparaître.

---

## F. Sur mobile (optionnel)

Le plugin Obsidian Git fonctionne aussi sur l'application mobile, mais demande
parfois une configuration de token plus délicate. Faites d'abord fonctionner le
poste de bureau, puis ajoutez le mobile.

---

## Notes importantes

- **Synchronisation = sauvegarde + collaboration**, pas un coffre-fort secret :
  tout ce que vous synchronisez ici devient visible dans le dépôt. N'y mettez pas
  de données sensibles (identifiants, documents personnels confidentiels).
- Le `.gitignore` du dépôt ignore déjà les fichiers de config locaux bruyants
  d'Obsidian (`workspace.json`, caches), pour des synchros propres.
- Conflits Git : si vous éditez sur deux machines sans synchroniser entre les
  deux, un conflit peut survenir. Le plugin vous alertera ; en cas de doute,
  demandez-moi de vous aider à le résoudre.
