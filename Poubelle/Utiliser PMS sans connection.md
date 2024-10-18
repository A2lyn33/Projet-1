## **Utilisation de Plex à sans connection internet**


* #### **Renter l'adresse IP de la machine sur laquelle est installé PMS**:
    * ##### Utiliser la notice Gestion des bibliothéque et de méthadonné:
    * ##### Ouvrir éditeur registre Windows:
>HKEY_CURRENT_USER/Software/Plex, Inc./Plex Media Server

* ##### Nouveau fichier en "valeur de chaine".
* ##### Editer l'option "allowedNetworks", il doit être inscrit au moment de la création du fichier, il n'est plus modifiable par la suite.
*  ##### Rentrer l'adresse du cliens : 172.16.10.20/24, dans modifier ficher.



Source [Utiliser plex sans internet](https://www.howtogeek.com/303282/how-to-use-plex-media-server-without-internet-access/)
