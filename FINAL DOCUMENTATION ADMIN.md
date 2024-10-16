# **Documentation Administrateur:**

## 1 Instalation et configuration du serveur débian 12
## 2 instalation et configuration du protocole NFS
## 3 Gestion des IP


 #### **Instalation et configuration du serveur débian 12 :**
* ##### Commencer par télécharger [Débian 12](https://www.debian.org/distrib/?ref=belginux.com) .
  * ##### Choisissez votre version en 64 et 32 bits et cli
* ##### Une fois l'ISO téléchargé il faudra une clé bootable, je vous renvoie à cette article [lecrabeinfo](https://lecrabeinfo.net/creer-cle-usb-installation-bootable-live-cd-linux-ubuntu-debian.html?ref=belginux.com)
* ##### Une fois booté selectioné **Graphical install**:
![image](https://belginux.com/content/images/2023/12/1.png)
* ##### Sélectionner votre langue d'installation :

 ![image](https://belginux.com/content/images/size/w1600/2023/12/2.png)
* ##### Sélectionnez les paramètres régionaux: 
![image](https://belginux.com/content/images/size/w1600/2023/12/3.png)
* ##### On configure son clavier :
![image ](https://belginux.com/content/images/size/w1600/2023/12/4.png)
* ##### On donne un nom au serveur, peu importe:

 ![image](https://belginux.com/content/images/size/w1600/2023/12/5.png)
 
 * ##### Laissez vide ou mettez localdomain : 
 ![image](https://belginux.com/content/images/size/w1600/2023/12/6-1.png)
* ##### Choisissez un mot de passe fort pour le compte root, celui qui a tout les privilèges:
![image](https://belginux.com/content/images/size/w1600/2023/12/7.png)
* ##### Création du compte Utilisateur :
![image](https://belginux.com/content/images/size/w1600/2023/12/8-1.png)
* ##### Création du Login :
 ![image](https://belginux.com/content/images/size/w1600/2023/12/9.png)
* ##### Mot de passe compte :
![image](https://belginux.com/content/images/size/w1600/2023/12/10.png)
* ##### On choisi le mode de partitionnement, Assisté - utiliser un disque entier:
![image](https://belginux.com/content/images/size/w1600/2023/12/11.png)
* ##### On sélectionne le disque ou sera installé Debian 12 serveur:
![image](https://belginux.com/content/images/size/w1600/2023/12/12-2.png)
* ##### On va choisir l'option Tout dans une seule partition:
![image](https://belginux.com/content/images/size/w1600/2023/12/Screenshot_20231207_150135.png)
* ##### Sélectionnez Terminer le partitionnement et appliquer les changements:
![image](https://belginux.com/content/images/size/w1600/2023/12/14.png)
* ##### On valide par Oui:
![image](https://belginux.com/content/images/size/w1600/2023/12/15.png)
* ##### L'instalation commence.
* ##### Choisir Non : 
* ![image](https://belginux.com/content/images/size/w1600/2023/12/17.png)
* ##### Choisir un miroir correspondant généralement au pays ou l'on se trouve.
* ##### Ici vous pouvez choisir deb.debian.org:
![image](https://belginux.com/content/images/size/w1600/2023/12/19.png)
* ##### On laisse vide et on continue
 ![image](https://belginux.com/content/images/size/w1600/2023/12/20.png)
*  ##### A vous de choisir.
*  ##### Il ne faut pas d'environnement de bureau vu que l'on veut installer Debian 12 comme serveur, cochez et décochez suivant l'exemple. Nous avons besoin du SSH et on peut cocher les utilitaires usuels du système:
  ![image](https://belginux.com/content/images/size/w1600/2023/12/22.png)
* ##### On choisi d'installer [GRUB](https://fr.wikipedia.org/wiki/GNU_GRUB) sur le disque principal.
* ##### Selectioné le disque :
 ![image](https://belginux.com/content/images/size/w1600/2023/12/24.png)
* ##### L'installation est terminée, retirez la clé USB du serveur et cliquez sur Continuer.
###### Toutes les captures ci dessus proviennes de [Belinux](https://belginux.com/installer-facilement-son-serveur-sous-debian-12/#se-connecter-au-serveur)

* ##### le serveur :
 ![image](https://cdn.discordapp.com/attachments/1292773669319344168/1296057607701921843/Fichier_bien_dispo_sur_serveur_Debian_12.bmp?ex=6710e735&is=670f95b5&hm=18f876b18217cc9d6f03d543d5ffce2ff9d5a14777cfb004fd5228331972bfd2&).
* #### **Configuration d'une IP fixe avec Débian 12:**
  * ##### Ouvrez le terminal et exécutez
````        
        sudo nano/etc/network/interfaces
````
  * ##### Configurez l'IP :
````        
        auto eth0
        idface eth0 inet static
        address 172.16.10.10
        netmask 255.255.255.0
        gateway 172.16.10.1             ##### **A VERIFIER**
        dns-nameservers 172.16.10.1
```` 
 * ##### Enregistrez et quitttez l'éditeur
  * ##### Redemarrez le service
````        
        sudo systemct1 resart systemd-networkd
````
![image](https://cdn.discordapp.com/attachments/1292773669319344168/1296057608725332021/Configuration_IP_Serveur_Debian_12.bmp?ex=6710e735&is=670f95b5&hm=ccf08117afc7edb3fa2bf7eddfec59e882148198a1d9a931207a4d91d2e1a298&)

### **Configuration et instalation du Protocole [NFS](https://fr.wikipedia.org/wiki/Network_File_System)**
 #### **Instalation du paquet :**
* ##### mettre à jour le cache des paquets:
````
      sudo apt-get update
````
* ##### Installer le paquet "nfs-kernel-server" :`
 
`````
sudo apt-get install nfs-kernel-server
`````
![image](https://www.it-connect.fr/wp-content-itc/uploads/2021/10/apt-get-install-nfs-server-debian.png)

###### la capture provient de [it-connect](https://www.it-connect.fr/le-protocole-nfs-pour-les-debutants/)
* ##### Configurer le démarrage automatique du service :
````    
   sudo systemctl enable nfs-server.service
````
 #### **Déclaration d'un partage NFS**

* ##### Créer le répertoire à partager :
````
        mkdir /srv/partagenfs
````
* ##### Appliquer les permissions :
````
        chown nobody:nogroup /srv/partagenfs/
        chmod 755 /srv/partagenfs/
````

* ##### Éditer le fichier de configuration /etc/exports :
 ````       
        sudo nano /etc/exports
````
* ##### Ajouter la ligne suivante :
````
        /srv/partagenfs 172.16.10.10/24(rw,sync,anonuid=65534,anongid=65534,no_subtree_check) 
````
![image](https://www.it-connect.fr/wp-content-itc/uploads/2021/10/serveur-nfs-exports-partage.png)
###### la capture provient de [it-connect](https://www.it-connect.fr/le-protocole-nfs-pour-les-debutants/)

* ##### Appliquer la configuration :
````
        exportfs -a
````

* ##### Vérifier les partages :
````
        showmount -e 172.16.10.10
`````
![image](https://www.it-connect.fr/wp-content-itc/uploads/2021/10/showmount-nfs-exemple.png)
###### la capture provient de [it-connect](https://www.it-connect.fr/le-protocole-nfs-pour-les-debutants/)
 #### **Connexion au partage NFS depuis un client Linux**

* ##### Installer le paquet client NFS :
````
        sudo apt-get install nfs-common
`````
* ##### Créer un point de montage :
````
        mkdir /media/partagenfs
````
* ##### Monter le partage manuellement :
````
        mount -t nfs4 172.16.10.10:/srv/partagenfs /media/partagenfs/
````
* ##### Pour un montage automatique, éditer /etc/fstab :
````
        sudo nano /etc/fstab
````
* ##### Ajouter la ligne :
````
        172.16.10.10:/srv/partagenfs /media/partagenfs nfs4 defaults,user,exec 0 0 
`````
* ##### Monter tous les partages définis dans fstab :
````
         sudo mount -a
````
#### **Capture des paquets NFS avec TCPDUMP**

* ##### Installer tcpdump :
````
        sudo apt-get install tcpdump
````
* ##### Lancer une capture sur les ports NFS :
````
        tcpdump port 2049 or port 111
````
* ##### Vérifier l'activité NFS depuis le client :
````
        ls /media/partagenfs
`````
