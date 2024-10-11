# Document administrateur 

Sommaire

  -1 Prérequis technique
  
  -2 Serveur Debian  
    - Installation debian 12  
    - Configuration IP fixe  
    - Installation NFS  
    - Installation Plex  
  
  -3 Installation de Ubuntu
     - Configuration IP fixe 
     
  -4 Installation de Windows 10
     - Configuration IP fixe 
     
 -5 Configuration avancée des bibliothèques et métadonnées
 
 -6 FAQ
     
   

## Prérequis technique

 -VirtualBox
 
 -ISO Debian server 12


## Installation et configuration 

 ### -1  Installation de Debian 12
  
  - Sélectionnez Graphical install:
  - Sélectionner votre langue d'installation,
  - Sélectionnez les paramètres régionaux,
  - On configure son clavier,  
  - On donne un nom au serveur,
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
Ici vous pouvez choisir deb.debian.org:
  - On laisse vide et on continue:
  - Si vous souhaitez participer à l'étude statistique sur l'utilisation des paquets, répondez non
  - Il ne faut pas d'environnement de bureau vu que l'on veut installer Debian 12 comme serveur, décochez toutes les cases sauf la case serveur ssh et la case utilitaires usuels du système qui devront rester cocher car nous en avons besoin pour notre serveur.
  - On choisi d'installer GRUB sur le disque principal: donc répondez oui 
  - On sélectionne le disque:
  - L'installation est terminée
  - Le serveur démarre:


 ### 2 -Configuration IP fixe 

  - Lancer le terminal
  - se connecter avec login : root et password : Azerty1* (ici pour le projet)
  - lancer les mises a jours avec : apt update
  - installer les outils réseau
```
sudo apt install net-tools
```
Cela mettra à jour votre liste de paquets et installera net-tools , Ifconfig , Netstat

 - Taper Ifconfig
```   
ifconfig
```
 - Taper Ip addr show
```
ip addr show
```
 - Taper ifup enp0s8
```
ifup enps08
```
  - Taper ip link set enp0s8 up
  - Taper ip addr show
  - Taper ifconfig
  - nano /etc/network/interfaces
  - Rajouter les lignes
```
allow-hotplug enp0s8
iface enp0s8 inet static
address 172.16.10.10
netmask 255.255.255.0
```
   - systemctl restart networking
     
--- 
---

### -3 Installation et configuration des clients NFS

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
---
---

 ### -4 Installation Plex

 # **Installer Plex sur débian et configuration**

* ### Importation Plex et téléchargement:

  *   ##### Importer la clé [GPG](https://fr.wikipedia.org/wiki/GNU_Privacy_Guard)  :
             sudo wget -O- https://downloads.plex.tv/plex-keys/PlexSign.key | gpg --dearmor | sudo tee /usr/share/keyrings/plex.gpg        
  
   
     * ##### Ajout du référenciel Plex APT (il permettra d'installer de faiire les MAJ ou supprimer Plex):
           echo deb [signed-by=/usr/share/keyrings/plex.gpg] https://downloads.plex.tv/repo/deb public main | sudo tee /etc/apt/sources.list.d/plexmediaserver.list 

    * ##### MAJ de APT et instalation de Plex:
          sudo apt install apt-transport-https
          sudo apt update
          sudo apt install plexmediaserver
          
   * ##### (optionnel) Vérifier l'execution de Plex:
         systemctl status plexmediaserver    

* ### Configurer PLEX MEDIA SERVER dans Debian :

   * ##### Création d'un répertoire de stockage multimédia 
         sudo mkdir -p /opt/plexmediaserver/{movies,series,photos}    
   * ##### Chemin de copie des fichiers multimédia:
            sudo chown -R $USER: /opt/plexmediaserver
    * ##### Création des droits Utilisateurs [755](https://www.wistee.fr/serveur-ftp/modifier-droits-chmod.html) :
                sudo chmod 755 -R /opt/plexmediaserver
    
* ### Configurer PLEX MEDIA SERVER sur [Plex1](https://app.plex.tv/auth/#!?clientID=kwfdkmlvv3fw59tr7egntt9b&context%5Bdevice%5D%5Bproduct%5D=Plex%20Web&context%5Bdevice%5D%5Bversion%5D=4.139.0&context%5Bdevice%5D%5Bplatform%5D=Chrome&context%5Bdevice%5D%5BplatformVersion%5D=129.0&context%5Bdevice%5D%5Bdevice%5D=Windows&context%5Bdevice%5D%5Bmodel%5D=hosted&context%5Bdevice%5D%5BscreenResolution%5D=1337x861%2C1920x1080&context%5Bdevice%5D%5Blayout%5D=desktop&context%5Bdevice%5D%5Bprotocol%5D=https&forwardUrl=https%3A%2F%2Fapp.plex.tv%2Fdesktop%2F%23%21%2Flogin%3FpinID%3D108682089&code=xthadj2tkm2bpfth1h6m8zyj6&language=fr) ou [Plex2](http://YOUR_SERVER_IP:32400/web) :
    * ##### Créer un compte et suivre les instructions.
    * ##### Pour REMOTE Plex:
    ![photo](https://trash-guides.info/Plex/Tips/images/plex-settings-icon.png)
    ![photo2](https://trash-guides.info/Plex/Tips/images/settings-settings.png)
    ![photo3](https://trash-guides.info/Plex/Tips/images/settings-remote-access.png)
##### 1 Assurez-vous d'être en paramettre avancés.
##### 2 Activer/Désactiver accès à distance 
##### 3 IP LAN/conteneur
##### 4 IP Public
##### 5 Specifiez manuellement si vous utilisez un docker ou sii vou souhaitez un          port fixe
##### 6 Entrez le port Plex que vous souhaitez utiliser(par defaut: 324000)
##### 7 Appliquer.
##### 8 Vitesse téléchargement
##### 9 Définir débit distant

## [credit instalation config ](https://www.it-connect.fr/installer-un-serveur-multimedia-plex-sous-debian-ou-ubuntu/)
## [credit remote](https://trash-guides.info/Plex/Tips/Plex-media-server/#remote-access)


 -4 Installation client

 -5 Configuration bibliothéque et methadonnées

 

## FAQ : Solutions aux problèmes connus et communs liés à l'installation et à la configuration 



  - Documentation admin
    - Prérequis techniques
    - Étapes d'installation et de configuration : instructions étape par étape
    - FAQ : solutions aux problèmes connus et communs liés à l’installation et à la configuration
