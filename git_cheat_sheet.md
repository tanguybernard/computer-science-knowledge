# Git Cheat Sheet, A flow with rebase

Prenons __develop__ comme branche principale


## Le flow

1. Régulièrement, je vais sur la branche __develop__ et je récupère les changements que je vais ensuite insérer dans ma branche

        git checkout develop
        git pull --rebase

2. Je switch sur ma feature branche


Soit Créer une branche depuis une autre(ici "develop")

    git checkout -b myFeatureBranch develop

Soit branche déjà crée, je vais dessus

    git checkout -b myFeatureBranch
    
    # shortcut: switch sur la branche précèdente  (develop -> feature  dans notre cas)
    git checkout -

3. Stash (Si nécessaire)

Enregistrer son travail temporairement avant le rebase

        git stash

4. Je rebase develop dans ma branche

        git rebase develop
    
5. Si conflits je les résouds et je continue le rebase

        git rebase --continue

6. Une fois l'opération terminé je pousse mes changements

        git push

Si vos changements ont déjà été poussés auparavant et ont été _rebasé_, votre historique a donc de nouveau changé.
Il faudra donc forcer le push

    git push --force-with-lease
    
Pourquoi _--force-with-lease_ plutôt que _--force_

Réponse simple: plus sécurisé

Réponse détaillé:

http://weiqingtoh.github.io/force-with-lease/

7. Récupération les modifications temporaires

        git stash pop

## La statégie de fusion dans branche (develop et master)

Le fast-forward (pas de commit de merge)

        --ff-only


## Et si on squashé ?

Il peut arriver lors d'un développement de passer et repasser et re-repasser sur un fichier et cela peut générer énormément de bruits surtout lorsque l'on pousse tous les commits. 

Voyez un peu :

        ad4h5fc   feat(physician): add new function to sort physician by they lastname     
        fbde9fd   docs(readme): add Readme.md
        70aaed5   docs(readme): update Readme
        ccf2779   docs(readme): update Readme again
        8c706b5   docs(readme): update Readme again and again

Pour éviter tout ce bruit, il existe un moyen simple: __le rebase interactif__

Si je rebase depuis develop, voici la syntaxe:

        git rebase -i develop
        
On voudra peut-être faire un rebase interactif depuis un commit spécifique (souvent on part du plus vieux):

        git rebase -i 8c706b5


Cela vas nous permettre d'éditer notre suite de commits. On voit que pour le moment tout les commits sont picks:

        pick  fbde9fd   docs(readme): add Readme.md
        pick  70aaed5   docs(readme): update Readme
        pick  ccf2779   docs(readme): update Readme again
        pick  8c706b5   docs(readme): update Readme again and again
        
        
Le rebase interactif va nous permettre de les éditer et dans notre cas, de garder simplement le premier.
On squashera donc le reste, qui correspond à notre bruit.

        pick  fbde9fd   docs(readme): add Readme.md
        squash  70aaed5   docs(readme): update Readme
        squash  ccf2779   docs(readme): update Readme again
        squash  8c706b5   docs(readme): update Readme again and again

Une fois squash, on pourra pousser notre travail, et voici donc la suite de commits qui apparaîtra:

        ad4h5fc   feat(physician): add new function to sort physician by they lastname     
        fbde9fd   docs(readme): add Readme.md

Bcp plus propre ;)

## Un cherry-pick ?

Git possède la commande cherry-pick qui permet de sélectionner un commit quelconque et de l’appliquer sur la branche actuelle.

        git checkout mybranchToApllyTheCommit
        git cherry-pick d42c389f


## Et si on taggé ?

En precisant le hash du commit:

    git tag v2.6.0 9fceb02

Ne pas oublier de pousser le tag:

    git push origin v2.6.0

Tou les tags

    git push origin --tags

## Modifier un commit

Ajouter les fichiers au commit que vous voulez fixer. 

    git add <files>

Expliquer à git qu'on veut fix un commit.

    git commit --fixup <votre_sha1_de_commit>

_Un nouveau commit prefixé par __fixup!__ est crée à la suite de vos commits (donc mal placé pour le moment)._

Le rebase sait qu’il devra faire un fixup de ce dernier commit préfixé, il se charge donc de le positionner où il faut dans la liste.

    git rebase -i --autosquash <votre_sha1_de_commit>~
    
_~ pour qu’il soit inclut dans le rebase_

Plus qu'a valider le rebase et __push --force__

## Mettre a jour un fichier sur un commit en particulier

Sur ma branche (log sur une ligne (pas d'auteur, pas de Date)):

    git log --oneline

Result :

    2e68 (HEAD -> ma-branche) chore: update dev dependencies
    c325 chore: do something
    22a5 feat: refactor and add featues
    b386 docs: update credits

Je veux modifier le commit _feat: refactor and add featues_, car j'ai ajouté des données erronées dans le changelog.

Je vais executer un rebase interactif.

    git rebase -i HEAD~3
    
or
    
    git rebase -i b386 

Dans l'éditeur, j'ajoute le mot clé __break__ :
    
    pick 22a5 feat: refactor and add featues
    break
    pick c325 chore: do something
    pick 2e68 chore: update dev dependencies
    
Sortir _:wq_

Nous sommes stoppé au commit qui nous intéresse

    Stopped at 22a5... feat: refactor and add featues
    
Nous pouvons alors modifier, ajouter ou supprimer des fichiers.

Puis on ammend ce commit:

    git commit -a --amend --no-edit
    # --no-edit because we don't want to edit the message

Finalement on continue le rebase  et on push:

    git rebase --continue
    git push --force-with-lease
    
    

Si nous voulions modifier le dernier commit, alors nous aurions juste besoin d'effectuer les modifications puis d'amend le commit simplement.

    git add modified_file
    git commit --amend --no-edit
    git push --force-with-lease
    
    
    
Credits :

https://pawamoy.github.io/posts/howto-edit-git-commit-contents/

        
## Quelqu'un a développé sur ma branche, je ne suis plus à jour

        git reset --hard @{u}
        
Basically, @{u} is just shorthand for the upstream branch that your current branch is tracking. For example, this typically equates to origin/[my-current-branch-name]. It's nice because it's branch agnostic.

Make sure to **git fetch** first to get the latest copy of the remote branch.

## N'oublions pas de supprimer la branche une fois le travail terminé

        git push origin --delete the_remote_branch


## Je veux commit un fichier en plusieurs partis

Je l'ajoute avec l'option -p (--patch)

    git add -p <filename>
        
On découpe par morceau

    s
        
Ensuite on en selectionne un.

    y
        
Et on passe les autres

    n
        
On commit

    git commit -m "commit un morceau" <filename>
        

Puis on continue

Si un problème on peut reset:

    git reset -p


## Montre les commits pas encore poussé de ma branche

    git log @{u}..

Windows :

    git log "@{u}.."

## Je veux réordonner mes commits (Attention pas de dependances, de chgts sur les mêmes fichiers sur 2 commits qui se suivent)

NB: C'est juste un couper/coller.

J'aimerai que le "fix" soit devant le "update" pour ensuite les squashé ensemble

    * 367eb93 (HEAD -> master) Fix text
    * 30c1d6a Add newFile.png
    * 70228b2 update master.txt

We want to change the history for 3 commits, so we are going to execute git rebase -i HEAD~3.

    pick 70228b2 update master.txt
    pick 30c1d6a Add newFile.png
    pick 367eb93 Fix text  => Le commit push le plus récent

Nous allons couper le __pick 367eb93 Fix text__ et le copier devant le __pick 70228b2 update master.txt__.

    pick 70228b2 update master.txt
    pick 367eb93 Fix text
    pick 30c1d6a Add newFile.png
    
    

Sauvegarde et quitte l'editor car nous avons terminé le reordering. 

En executant: 

    git log --oneline 

On s'assure de reordonnancement :


    * 08497a9 (HEAD -> master) Add newFile.png
    * ba137dd Fix text
    * c8502f8 update master.txt

On pourra ensuite squasher les 2 dernier :)


https://belev.dev/some-of-the-most-used-git-interactive-rebase-options

## Credits

Explication du git rebase en fr, il y a même des dessins ;)

https://www.miximum.fr/blog/git-rebase/

Pour un terminal encore mieux, avec des plugins et des raccourcis bien pratiques (git, npm, docker...)

https://ohmyz.sh/

- git checkout --> gco
- git status --> gst
- git rebase develop --> grbd

... bref il y a plein d'alias

https://github.com/robbyrussell/oh-my-zsh/blob/master/plugins/git/git.plugin.zsh

Squash

https://www.ekino.com/articles/comment-squasher-efficacement-ses-commits-avec-git

Fixup

https://medium.com/just-tech-it-now/git-commit-fixup-corriger-editer-un-commit-simplement-dd6c7d9026cd

Autres

https://blog.octo.com/git-dans-la-pratique-22/
    
