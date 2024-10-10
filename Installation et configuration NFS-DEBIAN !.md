# **Installation et configuration d'un serveur NFS sous Debian** ---> https://www.it-connect.fr/le-protocole-nfs-pour-les-debutants/
---
##### **```A. Installation du paquet```**
---
***Mettre à jour le cache des paquets :***
```
sudo apt-get update
```
***Installer le paquet "nfs-kernel-server" :***
```
sudo apt-get install nfs-kernel-server
```
***Configurer le démarrage automatique du service :***
```
sudo systemctl enable nfs-server.service
```
##### **```B. Déclaration d'un partage NFS```**
---
***Créer le répertoire à partager :***
```
mkdir /srv/partagenfs
```
***Appliquer les permissions :***
```
chown nobody:nogroup /srv/partagenfs/
chmod 755 /srv/partagenfs/
```
***Éditer le fichier de configuration /etc/exports :***
```
sudo nano /etc/exports
```
***Ajouter la ligne suivante :***
```
/srv/partagenfs 172.16.10.10/24(rw,sync,anonuid=65534,anongid=65534,no_subtree_check) 
```
***Appliquer la configuration :***
```
exportfs -a
```
***Vérifier les partages :***
```
showmount -e 172.16.10.10
```
##### **```C. Connexion au partage NFS depuis un client Linux```**
---
***Installer le paquet client NFS :***
```
sudo apt-get install nfs-common
```
***Créer un point de montage :***
```
mkdir /media/partagenfs
```
***Monter le partage manuellement :***
```
mount -t nfs4 172.16.10.10:/srv/partagenfs /media/partagenfs/
```
***Pour un montage automatique, éditer /etc/fstab :***
```
sudo nano /etc/fstab
```
***Ajouter la ligne :***

```
172.16.10.10:/srv/partagenfs /media/partagenfs nfs4 defaults,user,exec 0 0 
```
***Monter tous les partages définis dans fstab :***
```
sudo mount -a
```
##### **```D. Capture des paquets NFS avec TCPDUMP```**
---
***Installer tcpdump :***
```
sudo apt-get install tcpdump
```
***Lancer une capture sur les ports NFS :***
```
tcpdump port 2049 or port 111
```
***Vérifier l'activité NFS depuis le client :***
```
ls /media/partagenfs
```
***Cette documentation couvre les étapes essentielles pour installer, configurer et utiliser un serveur NFS sous Debian, ainsi que la connexion depuis un client Linux et la capture de paquets pour le débogage.***
