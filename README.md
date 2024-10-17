# **Documentation Générale:**

* # **SOMMAIRE:**
  * ##### [résentation du projet et objectifs finaux](https://github.com/WildCodeSchool/TSSR-2409-P1-G4-Serveur-de-contenus-multimedia/blob/main/FINAL%20DOCUMENTATION%20GENERALE.md#pr%C3%A9sentation-du-projet-et-objectifs-finaux-)
  * ##### [Introduction](https://github.com/WildCodeSchool/TSSR-2409-P1-G4-Serveur-de-contenus-multimedia/blob/main/FINAL%20DOCUMENTATION%20GENERALE.md#introduction-)
  * ##### [Choix techniques](https://github.com/WildCodeSchool/TSSR-2409-P1-G4-Serveur-de-contenus-multimedia/blob/main/FINAL%20DOCUMENTATION%20GENERALE.md#choix-techniques-)
  * ##### [Difficultées rencontrées](https://github.com/WildCodeSchool/TSSR-2409-P1-G4-Serveur-de-contenus-multimedia/blob/main/FINAL%20DOCUMENTATION%20GENERALE.md#difficult%C3%A9es-rencontr%C3%A9es-1)
  * ##### [Solutions trouvées](https://github.com/WildCodeSchool/TSSR-2409-P1-G4-Serveur-de-contenus-multimedia/blob/main/FINAL%20DOCUMENTATION%20GENERALE.md#solutions-trouv%C3%A9es-)
  * ##### [Amélioration possible](https://github.com/WildCodeSchool/TSSR-2409-P1-G4-Serveur-de-contenus-multimedia/blob/main/FINAL%20DOCUMENTATION%20GENERALE.md#am%C3%A9lioration-possible-)
* ### **Présentation du projet et objectifs finaux :**

  * ##### Ce **projet** à pour but la mise en place d'un **serveur** (_débian12_) mutimédia, avec l'utiilsation de **PMS** comme interface graphique ainsi que de la gestion des option. Ce serveur doit être **utilisable par tous les OS**.
  * ##### Les **objectifs** sont l'instalation du serveur **Débian 12**, **la recherche de solution** pour le partage de fichiers   multimédias, **configurations** de différents **OS**,instalations et configuration de **PMS**, et pour finir une **utilisations simple** du logiciel PMS pour le **transfert**, le **visionnage** et le **partage** de fichier multimedias.
 * ### **Introduction :**
   * ##### Nous avons décider de nous **diviser les taches**, pour nous permettre de menner à bien ce projet, les prochains points de la présentation sont les différents **membre du projet**, ainsi que leurs **rôles** sur les deux sprints. 
   * ##### **Adeline**:
     *  ##### **Sprint 1** : Recherche des informations et installation serveur débian, et cliens Windows        
      * ##### **Sprint 2** : PO Instalations Protocole NFS et PMS, Réalisation de la slide pour presentation finale. 
   * ##### **Julien:** 
     * ##### **Sprint 1** : Recherche des informations protocole NFS et instalation, installation serveur Débian, et 	client Ubuntu. 
      * ##### **Sprint 2**: SM Instalations Protocole NFS et PMS, configuration bibliothéque et métadonnées.
   * ##### **Bruno:** 
     * ##### **Sprint 1** : 1PO Rédaction de toute la documentation, Utilisateur, Install,Doc Générale
     * ##### **Sprint 2** : Instalations Protocole NFS et PMS
   * ##### **Martin:** 
     * ##### **Sprint 1** :  SM Recherche Instalation et paramétrage Plex, gestion des bibliothéque et métadonnés. 
     * ##### **Sprint 2** : Recherche pour l'équipe, et rédaction de la documentation .
 * ### **Choix Techniques :**
 
   ##### Pour répondre aux demande du sujet, ainsi qu'aux défis liés au projet voici les différent choix techniques:
* #####   **Serveur Debian 12 :**
   * ##### **enp0s3 (NAT)** : Configurée en DHCP pour accéder à Internet.
   * ##### **enp0s8 (Interne)** : IP statique `172.16.10.10`, pour la communication avec le client.-
* ##### **Client Ubuntu :**
   * #####  **enp0s3 (NAT)** : DHCP pour l'accès Internet.
   * ##### **enp0s8 (Interne)** : IP statique `172.16.10.20`, pour se connecter au serveur.

  

* ### **Difficultées rencontrées:**
* #####   **Connexion Réseau** : Difficulté à établir une connexion simultanée au réseau local et à Internet.
* ##### **Routage** : Mauvaise gestion du trafic entre les cartes réseau, empêchant la communication fluide.
* #####  **Droits NFS** : Le client Ubuntu ne pouvait pas ajouter de fichiers sur le partage NFS du serveur, faute de permissions adéquates.
  
* ### **Solutions trouvées :**
 * ##### **Cartes Réseau** : Configuration identique sur les deux machines :
  * ##### **enp0s3 (NAT)** pour Internet via DHCP.
  * ##### **enp0s8 (Interne)** avec des IP statiques (`172.16.10.10` et `172.16.10.20`) pour la connexion locale.
* ##### **Routage** : Routes statiques pour le réseau interne via `enp0s8` et passerelle par défaut sur `enp0s3` pour l'Internet.
* ##### **Droits NFS** : Alignement des permissions utilisateur sur le serveur et le client, permettant aux deux machines de lire et écrire sur le partage NFS. Cela a permis au client de déposer des fichiers directement sur le serveur.
 
* ### **Amélioration possible :**
   * ##### Amélioration de la sécurité sur le serveur
