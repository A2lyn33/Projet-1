# Document administrateur   

## Prérequis technique

 -VirtualBox
 
 -ISO Debian server 12


## Installation et configuration 

 ### -1  Installation de Debian 12
  
  -Mettre à jour votre serveur avec votre utilisateur:

  -Sélectionnez Graphical install:

  -Sélectionner votre langue d'installation, dans mon cas le français:

  -Sélectionnez les paramètres régionaux, dans mon cas la Belgique:

  -On configure son clavier, 
    
  -On donne un nom au serveur, peu importe:

  -Laissez vide ou mettez localdomain, par exemple et continuez:

  -Choisissez un mot de passe fort pour le compte root, celui qui a tout les privilèges:

  -On va créer un compte utilisateur, différent du compte root précédemment créé, ce n'est pas votre login mais le nom 
     complet de l'utilisateur:

  -Maintenant on crée le login:

  -On crée un mot de passe fort pour notre utilisateur:

  -On choisi le mode de partitionnement, Assisté - utiliser un disque entier:
 
  -On sélectionne le disque ou sera installé Debian 12 serveur:

  -On va choisir l'option Tout dans une seule partition:

  -Sélectionnez Terminer le partitionnement et appliquer les changements:

  -On valide par Oui:

  -L'installation du système de base commence:

  -Choisir Non:

  -Choisir un miroir correspondant généralement au pays ou l'on se trouve:

  -Ici vous pouvez choisir deb.debian.org:

  -On laisse vide et on continue:

  -Si vous souhaitez participer à l'étude statistique sur l'utilisation des paquets, répondez oui, si non... non 😄:

  -Il ne faut pas d'environnement de bureau vu que l'on veut installer Debian 12 comme serveur, cochez et décochez
     suivant l'exemple. Nous avons besoin du SSH et on peut cocher les utilitaires usuels du système:

  -On choisi d'installer GRUB sur le disque principal:

  -On sélectionne le disque:

  -L'installation est terminée

  -Le serveur démarre:




Installer sudo
Une fois connecté nous allons commencer par installer sudo, mais comme vous pouvez le constater, notre utilisateur normal n'a pas les droits nécessaires:

apt install sudo

Pour pouvoir installer sudo nous allons nous connecter en root, une fois la commande su - validée, il vous demander votre mot de passe:

su -

Voilà, vous êtes connecté en root! Attention à ne pas faire n'importe quoi parce que justement, en root il est permis de tout faire.

Maintenant on installe sudo avec cette commande:

apt install sudo
Et cette fois-ci, ça fonctionne!


Ajouter votre utilisateur dans le groupe sudo et Docker
Afin que votre utilisateur puisse avoir des privilèges pour lancer certaines commandes qui demandent des droits plus élevés et d'utiliser Docker, il faudra donc ajouter votre utilisateur dans le groupe sudo et Docker. Remplacez zarev par votre utilisateur:

sudo usermod -aG sudo zarev && sudo groupadd docker && sudo usermod -aG docker zarev
Si tout s'est bien passé, après avoir validé la commande, vous aurez droit à un feu d'artifice pour confirmer que tout s'est bien passé. En fait non c'est tout l'inverse, vous allez revenir à la ligne tout simplement 😋


Reboot du serveur:

reboot now
Mettre à jour votre serveur avec votre utilisateur:
Connectez-vous avec cette ligne de commande, remplacez zarev par votre nom d'utilisateur et 192.168.1.144 par l'IP de votre serveur:

ssh zarev@192.168.1.144
Lancez cette commande pour mettre à jour votre serveur. Il va vous demander votre mot de passe et ensuite exécuter votre commande:

 


 -2 Configuration Protocole NFS


 -3 Installation Plex

 -4 Installation client

 -5 Configuration bibliothéque et methadonnées

 

## FAQ : Solutions aux problèmes connus et communs liés à l'installation et à la configuration 



  - Documentation admin
    - Prérequis techniques
    - Étapes d'installation et de configuration : instructions étape par étape
    - FAQ : solutions aux problèmes connus et communs liés à l’installation et à la configuration
