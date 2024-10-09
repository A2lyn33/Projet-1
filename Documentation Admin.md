# Document administrateur 

Sommaire

 - [1 Debian 12](#Installation-de-Debian-12)
 - [2Installation-et-configuration-des-clients NFS](ligne114)

## Prérequis technique

 -VirtualBox
 
 -ISO Debian server 12


## Installation et configuration 

 ### -1  Installation de Debian 12
  
  - Mettre à jour votre serveur avec votre utilisateur:

  - Sélectionnez Graphical install:

  - Sélectionner votre langue d'installation, dans mon cas le français:

  - Sélectionnez les paramètres régionaux, dans mon cas la Belgique:

  - On configure son clavier, 
    
  - On donne un nom au serveur, peu importe:

  - Laissez vide ou mettez localdomain, par exemple et continuez:

  - Choisissez un mot de passe fort pour le compte root, celui qui a tout les privilèges:

  - On va créer un compte utilisateur, différent du compte root précédemment créé, ce n'est pas votre login mais le nom 
     complet de l'utilisateur:

  - Maintenant on crée le login:

  - On crée un mot de passe fort pour notre utilisateur:

  - On choisi le mode de partitionnement, Assisté - utiliser un disque entier:
 
  - On sélectionne le disque ou sera installé Debian 12 serveur:

  - On va choisir l'option Tout dans une seule partition:

  - Sélectionnez Terminer le partitionnement et appliquer les changements:

  - On valide par Oui:

  - L'installation du système de base commence:

  - Choisir Non:

  - Choisir un miroir correspondant généralement au pays ou l'on se trouve:

  - Ici vous pouvez choisir deb.debian.org:

  - On laisse vide et on continue:

  - Si vous souhaitez participer à l'étude statistique sur l'utilisation des paquets, répondez non

  - Il ne faut pas d'environnement de bureau vu que l'on veut installer Debian 12 comme serveur, cochez et décochez
     suivant l'exemple. Nous avons besoin du SSH et on peut cocher les utilitaires usuels du système:

  - On choisi d'installer GRUB sur le disque principal:

  - On sélectionne le disque:

  - L'installation est terminée

  - Le serveur démarre:




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
Si tout s'est bien passé, après avoir validé la commande, vous aurez droit à un feu d'artifice pour confirmer que tout s'est bien passé. En fait non c'est tout l'inverse, vous allez revenir à la ligne tout simplement


Reboot du serveur:

reboot now
Mettre à jour votre serveur avec votre utilisateur:
Connectez-vous avec cette ligne de commande, remplacez zarev par votre nom d'utilisateur et 192.168.1.144 par l'IP de votre serveur:

ssh zarev@192.168.1.144
Lancez cette commande pour mettre à jour votre serveur. Il va vous demander votre mot de passe et ensuite exécuter votre commande:

--- 
---

### -2 Installation et configuration des clients NFS

### Installation du client NFS

   - Mettez à jour la liste des paquets :
```
sudo apt update
```
   - Installez le paquet nfs-common :
```
sudo apt install nfs-common
```

**(Ces étapes vous permettront d'installer et de configurer un client NFS sur votre système Ubuntu, en établissant une connexion stable avec le serveur NFS)** 


### Configuration du client NFS

   - Créez un point de montage pour le partage NFS :
```
sudo mkdir -p /mnt/nfs_share
```
   - Montez le partage NFS :

**(Remplacez "adresse_ip_serveur" par l'IP de votre serveur NFS et "/chemin/du/partage" par le chemin du répertoire partagé sur le serveur.)**
```
sudo mount adresse_ip_serveur:/chemin/du/partage /mnt/nfs_share
```
   - Vérifiez que le montage a réussi :
```
df -h (Vous devriez voir le partage NFS listé.)
```
   - Pour rendre le montage permanent, ajoutez une entrée dans /etc/fstab :
```
sudo nano /etc/fstab
```
- Ajoutez la ligne suivante :
(Remplacez "adresse_ip_serveur" par l'IP de votre serveur NFS et "/chemin/du/partage" par le chemin du répertoire partagé sur le serveur.)
```adresse_ip_serveur:/chemin/du/partage /mnt/nfs_share nfs defaults 0 0```

   - Testez la configuration fstab :
```
sudo mount -a
```

   - Pour améliorer la stabilité, vous pouvez ajouter des options de montage :
(Remplacez "adresse_ip_serveur" par l'IP de votre serveur NFS et "/chemin/du/partage" par le chemin du répertoire partagé sur le serveur.)
```adresse_ip_serveur:/chemin/du/partage /mnt/nfs_share nfs rw,soft,sync,timeo=5,retrans=2 0 0```

Options de montage NFS
***rw : lecture-écriture.
soft : échec rapide si le serveur ne répond pas.
sync : écrit les données sur le disque avant de terminer l'opération.
timeo=5 : attente de 0,5 seconde avant d'abandonner une requête.
retrans=2 : réessaie une requête jusqu'à 2 fois en cas d'échec.***

Ces options configurent comment le partage NFS se comporte lors du montage.

   - Appliquez les changements en remontant tous les partages :
```
sudo mount -a
```

Informations Nécessaires
Nom : Généralement, vous n’avez pas besoin d’un nom d’utilisateur ou d’un mot de passe pour accéder à un partage NFS, car il utilise des permissions basées sur l'adresse IP et les droits d'accès du système de fichiers.
Mot de passe : Pas nécessaire pour NFS ; l'accès est contrôlé par les permissions du système d'exploitation.
Adresse IP : Vous devez connaître l'adresse IP du serveur NFS pour pouvoir monter le partage.



---
# Configuration du Client NFS sur le Serveur Plex

1. Installer les Paquets NFS
Assurez-vous que le serveur Plex a les paquets nécessaires pour utiliser NFS. Ouvrez un terminal sur votre serveur Debian 12 et exécutez :
```
sudo apt update
sudo apt install nfs-common -y
```
nfs-common : Ce paquet contient les outils nécessaires pour monter des systèmes de fichiers NFS.
2. Créer un Point de Montage
Créez un répertoire qui servira de point de montage pour le partage NFS :
```
sudo mkdir -p /mnt/plex_media
```
mkdir -p : Crée le répertoire /mnt/plex_media. L'option -p permet de créer tous les répertoires parents nécessaires.
3. Monter le Partage NFS
Pour monter le partage NFS, utilisez la commande suivante :
(Remplacez adresse_ip_serveur par l'adresse IP de votre serveur NFS.
Remplacez /chemin/du/partage par le chemin du répertoire partagé sur le serveur NFS.)
```
sudo mount adresse_ip_serveur:/chemin/du/partage /mnt/plex_media
```
4. Vérifier le Montant
Pour vérifier que le partage est monté correctement, exécutez :
```
df -h
```
Cela affichera tous les systèmes de fichiers montés, et vous devriez voir votre partage NFS dans la liste.
5. Rendre le Montant Permanent
Pour que le montage soit persistant après un redémarrage, ajoutez une entrée dans le fichier /etc/fstab :
```
sudo nano /etc/fstab
```
Ajoutez la ligne suivante à la fin du fichier :
```adresse_ip_serveur:/chemin/du/partage /mnt/plex_media nfs defaults 0 0```

6. Tester la Configuration
Pour tester si tout fonctionne correctement, exécutez :
```
sudo mount -a
```
Cela montera tous les systèmes de fichiers mentionnés dans /etc/fstab.
7. Configurer Plex pour Utiliser le Partage NFS
Accédez à l'interface web de Plex :
```http://adresse_ip_de_votre_serveur:32400/web```
---
**Pour récupérer l'adresse IP d'un serveur NFS, suivez ces étapes :**
Vérifiez la configuration du serveur :
Si vous avez accès au serveur, exécutez la commande suivante dans le terminal :
```
ifconfig
```
Cherchez l'adresse IP sous la section inet adr: pour l'interface appropriée (généralement eth0 ou wlan0).

Utilisez la commande showmount :
Sur un client, exécutez la commande suivante pour afficher les partages NFS disponibles sur le serveur (remplacez adresse_ip_serveur par l'adresse IP ou le nom d'hôte) :
```
showmount -e adresse_ip_serveur
```
Cela affichera les partages NFS et vous permettra de confirmer l'adresse IP du serveur.

Consultez le routeur :
Si vous n'avez pas accès direct au serveur, connectez-vous à l'interface de votre routeur pour voir une liste des appareils connectés et leurs adresses IP.
Ces étapes vous permettront de localiser l'adresse IP du serveur NFS sur votre réseau.

Pour savoir votre adresse IP :

**Windows :**
```
ipconfig
```

**Linux :**
```
ip a
```

 -3 Installation Plex

 -4 Installation client

 -5 Configuration bibliothéque et methadonnées

 

## FAQ : Solutions aux problèmes connus et communs liés à l'installation et à la configuration 



  - Documentation admin
    - Prérequis techniques
    - Étapes d'installation et de configuration : instructions étape par étape
    - FAQ : solutions aux problèmes connus et communs liés à l’installation et à la configuration
