### Rapport Synthétique : Configuration d'un Serveur Multimédia Plex sur Debian 12

#### 1. **Objectif**
Mettre en place un serveur Plex sur Debian 12, accessible depuis un client Ubuntu via un réseau local, tout en ayant accès à Internet pour les mises à jour. Un partage NFS a été configuré pour permettre le stockage et l'accès aux fichiers multimédias.

#### 2. **Configuration Réseau**
- **Serveur Debian 12 :**
  - **enp0s3 (NAT)** : Configurée en DHCP pour accéder à Internet.
  - **enp0s8 (Interne)** : IP statique `172.16.10.10`, pour la communication avec le client.
- **Client Ubuntu :**
  - **enp0s3 (NAT)** : DHCP pour l'accès Internet.
  - **enp0s8 (Interne)** : IP statique `172.16.10.20`, pour se connecter au serveur.

#### 3. **Problèmes Rencontrés**
- **Connexion Réseau** : Difficulté à établir une connexion simultanée au réseau local et à Internet.
- **Routage** : Mauvaise gestion du trafic entre les cartes réseau, empêchant la communication fluide.
- **Droits NFS** : Le client Ubuntu ne pouvait pas ajouter de fichiers sur le partage NFS du serveur, faute de permissions adéquates.

#### 4. **Solutions Apportées**
- **Cartes Réseau** : Configuration identique sur les deux machines :
  - **enp0s3 (NAT)** pour Internet via DHCP.
  - **enp0s8 (Interne)** avec des IP statiques (`172.16.10.10` et `172.16.10.20`) pour la connexion locale.
- **Routage** : Routes statiques pour le réseau interne via `enp0s8` et passerelle par défaut sur `enp0s3` pour l'Internet.
- **Droits NFS** : Alignement des permissions utilisateur sur le serveur et le client, permettant aux deux machines de lire et écrire sur le partage NFS. Cela a permis au client de déposer des fichiers directement sur le serveur.

#### 5. **Conclusion**
Les ajustements réseau et permissions NFS ont permis d'établir une communication stable entre le serveur Debian et le client Ubuntu, tout en assurant un accès fiable à Internet et au partage de fichiers pour Plex.
