# Réponses

# Mission 5
1. **Identifiant court du premier commit : af5be84
2. **Commit de l’ajout de la page Contact : feat(contact): ajouter la structure de la page contact
3. **Nombre actuel de commits : 9 commits (1 de trop car corection du README, j'ai mal lue les conssignes)
4. **Commande pour afficher l’historique graphique : git log --oneline --graph --all

# Mission 8
 Commande choisie : git reset --mixed HEAD~1 Elle déplace la branche main sur le commit précédent, ce qui retire le commit « Test affichage » de l'historique. Le dernier commit est donc annulé.
Pourquoi les modifications sont toujours présentes : avec --mixed (comme avec --soft), reset ne modifie pas les fichiers de la zone de travail. La règle body { display: none; } est donc toujours dans style.css, simplement non commitée. Avec --mixed, elle sort aussi de la zone de staging.
Méthode qui aurait aussi supprimé les modifications : git reset --hard HEAD~1. Elle supprime le commit et remet aussi les fichiers à l'état du commit précédent, ce qui efface la modification.
Pourquoi cette méthode est acceptable ici : reset réécrit l'historique, ce qui n'est sans risque que si le commit n'a été partagé avec personne.
J'ai ensuite supprimé la règle incorrecte de style.css, et git status indique que le dépôt est propre.

# Mission 9
Commande utilisée : git revert --no-commit HEAD, suivie de git commit -m "revert: annuler l'ajout de la promotion".
Résultat : l'historique contient à la fois le commit « Ajout promotion » et un nouveau commit qui l'annule (git log --oneline les montre tous les deux).
Pourquoi la méthode est différente de celle de la mission 8 : ce commit a déjà été récupéré par d'autres membres de l'équipe. Un reset réécrirait l'historique et leur dépôt local ne correspondrait plus à celui du serveur, ce qui provoquerait des conflits et obligerait à un push forcé. revert n'efface rien : il ajoute un commit inverse, donc l'historique partagé reste cohérent pour tout le monde.

# Mission 10
Commandes : git stash -u pour mettre equipe.html de côté, puis git stash pop pour le récupérer.
L'option -u est nécessaire car equipe.html est un fichier non suivi, qu'un git stash simple ignorerait.
Le dossier redevient propre, ce qui permet de corriger le titre de index.html sur main et de le commiter, puis de reprendre le travail sur equipe.html.

# Mission 11
Commande utilisée : git cherry-pick <hash-du-commit-fix>, exécutée depuis la branche main.
Identifiant du commit récupéré : <hash-du-nouveau-commit-sur-main>. Le commit d'origine sur test/experiments avait le hash <hash-d-origine>. Le hash est différent car cherry-pick crée une copie du commit sur la branche actuelle.
Pourquoi une fusion classique n'était pas adaptée : un git merge test/experiments aurait ramené tous les commits de la branche, y compris les couleurs expérimentales (commit 1) et le texte de test dans le footer (commit 3). Seule la correction orthographique devait être récupérée.

## Questions finales

**1. Différence entre zone de travail, staging et historique ?**
La zone de travail contient mes fichiers en cours de modification. Le staging contient ce que j'ai ajouté avec `git add` pour le prochain commit. L'historique contient les commits enregistrés.

**2. Pourquoi une branche dédiée pour une fonctionnalité ?**
Elle isole le travail en cours, donc `main` reste stable, et on peut abandonner ou relire la fonctionnalité facilement.

**3. Différence entre les méthodes des missions 8 et 9 ?**
`reset` supprime des commits et réécrit l'historique, donc il est réservé aux commits non partagés. `revert` ajoute un commit qui annule l'ancien, sans rien supprimer, donc il convient aux commits partagés.

**4. Quand mettre ses modifications de côté (stash) ?**
Quand il faut changer de contexte (urgence, changement de branche) sans commiter un travail inachevé.

**5. Pourquoi un commit précis plutôt qu'une fusion complète ?**
Pour ne récupérer que la modification voulue, sans les autres commits de la branche.

**6. À quoi sert HEAD ?**
C'est le pointeur vers le commit (et la branche) sur lequel je suis actuellement.

**7. Que représente HEAD~2 ?**
Le commit situé deux crans avant HEAD.

**8. À quoi sert un tag ?**
À marquer un commit précis de façon fixe, en général pour une version (ex. `v1.0.0`).

**9. Pourquoi des commits petits et précis ?**
L'historique est lisible, les bugs sont plus faciles à localiser, et on peut annuler ou récupérer une modification précise.

**10. Pourquoi ne pas versionner certains fichiers ?**
Ils sont sensibles (`.env`), générés automatiquement (logs, cache) ou propres à ma machine, et ils alourdiraient ou pollueraient le dépôt.