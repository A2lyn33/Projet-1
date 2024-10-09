# Installation et configuration des clients NFS

### Installation du client NFS

1. Mettez à jour la liste des paquets :
```
sudo apt update
```
2. Installez le paquet nfs-common :
```
sudo apt install nfs-common
```

---

**(Ces étapes vous permettront d'installer et de configurer un client NFS sur votre système Ubuntu, en établissant une connexion stable avec le serveur NFS)** 


### Configuration du client NFS

1. Créez un point de montage pour le partage NFS :
```
sudo mkdir -p /mnt/nfs_share
```
2. Montez le partage NFS :

**(Remplacez "adresse_ip_serveur" par l'IP de votre serveur NFS et "/chemin/du/partage" par le chemin du répertoire partagé sur le serveur.)**
```
sudo mount adresse_ip_serveur:/chemin/du/partage /mnt/nfs_share
```
3. Vérifiez que le montage a réussi :
```
df -h (Vous devriez voir le partage NFS listé.)
```
4. Pour rendre le montage permanent, ajoutez une entrée dans /etc/fstab :
```
sudo nano /etc/fstab
```
- Ajoutez la ligne suivante :
(Remplacez "adresse_ip_serveur" par l'IP de votre serveur NFS et "/chemin/du/partage" par le chemin du répertoire partagé sur le serveur.)
```adresse_ip_serveur:/chemin/du/partage /mnt/nfs_share nfs defaults 0 0```

5. Testez la configuration fstab :
```
sudo mount -a
```

6. Pour améliorer la stabilité, vous pouvez ajouter des options de montage :
(Remplacez "adresse_ip_serveur" par l'IP de votre serveur NFS et "/chemin/du/partage" par le chemin du répertoire partagé sur le serveur.)
```adresse_ip_serveur:/chemin/du/partage /mnt/nfs_share nfs rw,soft,sync,timeo=5,retrans=2 0 0```

Options de montage NFS
***rw : lecture-écriture.
soft : échec rapide si le serveur ne répond pas.
sync : écrit les données sur le disque avant de terminer l'opération.
timeo=5 : attente de 0,5 seconde avant d'abandonner une requête.
retrans=2 : réessaie une requête jusqu'à 2 fois en cas d'échec.***

Ces options configurent comment le partage NFS se comporte lors du montage.

7. Appliquez les changements en remontant tous les partages :
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
