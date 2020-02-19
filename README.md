# Désinscription massive de listes de diffusion

Le script ``unsubscribe.sh`` permet de se désinscrire massivement de listes de diffusion indésirables de type publicitaire. Il se base sur le champ ``List-Unsubscribe`` défini par la RFC 2369 (juillet 1998) et généralement présent dans les courriels publicitaires français. Ce champ contient des liens ``<mailto:>`` et/ou ``<http:>`` (ou ``<https:>``). Certains pourriels utilisent à la place le champ non standard ``X-List-Unsubscribe`` : il sera également détecté par notre script.

## Installation

* Ce script a été testé avec le logiciel de courriel Mozilla Thunderbird mais devrait fonctionner avec tout logiciel conservant les courriels dans des fichiers texte.
* Ce script ``bash`` est essentiellement basé sur les commandes ``grep`` et ``wget``. Il devrait donc fonctionner sur n'importe quel système de type UNIX, y compris MSYS2 sous Windows. Avec un autre shell, quelques modifications mineures devraient suffire : en particulier, l'option ``-o pipefail`` peut être retirée sans problème.
* Cloner le dépôt GitHub ou télécharger et extraire le zip dans un répertoire.

## Utilisation

* Dans votre logiciel de courriel, par sécurité effacez du répertoire qui sera utilisé les éventuels courriels pouvant présenter un risque (hameçonnage...).
* Il faut que les courriels aient été vraiment téléchargés (l'affichage du sujet du courriel ne suffit pas). Dans Thunderbird, s'ils n'ont pas été lus, il suffit de délectionner l'ensemble des courriels et avec le bouton droit de cliquer sur "Relever les messages sélectionnés".
* Utilisez l'éventuelle fonction "compacter les dossiers" afin d'éliminer définitivement du fichier les courriels déjà "effacés" (en fait simplement effacés de l'index).
* Repérez dans le système de fichiers le fichier ou le répertoire contenant les courriels à traiter. Vous pouvez aussi travailler sur des copies de ces fichiers.
* Lancez le script soit en lui fournissant un fichier :

```bash
$ ./unsubscribe.sh  ~/.thunderbird/rfjzi2xb.default/Mail/pop.aliceadsl.fr/Junk
```
* soit en lui fournissant un répertoire dont il analysera tous les fichiers, sous-répertoires inclus :

```bash
$ ./unsubscribe.sh ~/.monlogicieldemail/Junk/
```

Le script affiche sa progression avec un point par lien (ou un zéro en cas d'échec de la connexion), puis affiche ses statistiques. Les sorties de la commande ``wget`` sont ajoutées au fichier ``unsubscribe.log`` et les fichiers téléchargés sont enregistrés dans le répertoire ``téléchargés``. L'ensemble de ces fichiers vous permettra d'éventuellement identifier les désinscriptions qui ont échoué.

## Limitations

Ce script échouera avec un petit pourcentage de pourriels car :

* certains courriels contiennent un lien ``<mailto:>`` mais pas de lien ``<http:>``,  
* certaines pages de désinscription demandent de confirmer en cliquant sur un bouton,
* les pourriels qui nous proviennent de l'étranger ne proposent généralement pas de champ ``List-Unsubscribe``.

## Références
* https://www.rfc-editor.org/info/rfc2369 
* https://litmus.com/blog/the-ultimate-guide-to-list-unsubscribe
* https://www.gnu.org/software/wget/ 
* La syntaxe de ce script a été vérifiée par l'utilitaire shellcheck : https://www.shellcheck.net/

-----

Vincent MAGNIN, premier commit : 2020-02-16



