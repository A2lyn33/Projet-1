## -Explication des choix techniques :

### **Utilisation d'un protocole NFS,** 

**1** Principalement utilisé sous systéme UNIX, mais des versions existe pour les autres OS, Mac et Pc.

**2** Facilite le stockage de donné multimédia sur un serveur et ça gestion en local:
 * #### **Bonne gestion de la monté en charge**
    ##### (*demande soudaine de données*):
   * Réduction du trafic par **groupement de requêtes**.

    * Délégation (le client gère le fichier en local)

* #### **Systémes de maintenances simplifiés**:
 
    * **Migration** : le serveur NFS est migré de la machine A vers la machine B de manière transparente 		pour le client
    * **Réplication** : le serveur A est répliqué sur la machine B

* #### **Gestion de la sécurit**é:
    * ((-Négociation du niveau de sécurité entre le client et le serveur
-Sécurisation simple, support de Kerberos5, certificats SPKM et LIPKEY4
-Chiffrement des communications possible (kerberos 5p par exemple)))

 * #### **Reprises des incidents**
    * La gestion de la reprise sur incident est intégrée du côté client et du côté serveur.

* #### **Compatibilités**:

    * NFSv4 peut être utilisé sous Unix et sous MS-Windows. Il est disponible sur Mac depuis Mac OS X 	Lion (10.7)5.
-Support de plusieurs protocoles de transports (TCP, 

### **Gestion Bibliothéques et méthadonnés**:

 * Cepoint en option permet de gérer des options invisible dansle menu setting de Plex Media Serveur, via l'éditeur de registre windows.
