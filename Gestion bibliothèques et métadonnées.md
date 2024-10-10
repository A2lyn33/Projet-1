## Configuration des bibliothéques et des méthadonnées ==>Plex Media Serveur

### **1 Ouvrir l'éditeur de registre Windows:**
* #### Naviger dans:
    >HKEY_CURRENT_USER/Software/Plex, Inc./Plex Media Server
* #### Créer une nouvelle entrée:
  * ##### Pour la **création** d'une nouvelle valeur utiliser uniquement :
    ##### 1° **Valeur chaine** (string value), sert à entrer du texte, comme des chemins de fichiers, des adresses IP, ou des noms.
    ##### 2°  Utilisez **DWORD (32-bit) Value** pour les options qui sont des nombres (comme un intervalle en secondes) ou des booléens (1 pour oui/activé et 0 pour non/désactivé).

* #### Choix des options *(entrée les option suivantes à la créations du fichier)*
    ##### **GESTION BIBLIOTHEQUE**
    * ##### **autoEmptyTrash** : Définit si la "corbeille" est vidée automatiquement après chaque analyse de                    bibliothèque.
        ##### Valeur **1** pour **activer**
    * ##### **FSEventLibraryUpdatesEnabled** : Permet de lancer automatiquement une analyse de la bibliothèque          lorsque des modifications sont détectées dans les dossiers de la bibliothèque.
        ##### Valeur **1** pour **activer**
    * ##### **FSEventLibraryPartialScanEnabled** : Ne scanne que les dossiers qui ont changé lorsque des                    modifications sont détectées (nécessite FSEventLibraryUpdatesEnabled).
         ##### Valeur **1** pour **activer**
    * ##### **ScheduledLibraryUpdatesEnabled** : Active ou désactive les analyses programmées des bibliothèques.
        ##### **0** pour **désactiver** ou **1** pour **activer**
    * ##### **ScheduledLibraryUpdateInterval** : Spécifie l'intervalle (en secondes) entre les analyses programmées         des bibliothèques (nécessite ScheduledLibraryUpdatesEnabled).
        ##### exemple : **120** => **2** minutes
    ##### **GESTION METADONNEES**
    * ##### **AlbumSort** : Définit le tri par défaut des albums selon des critères comme l’année ou le titre(les          options peuvent être **years,title,etc..** )
        ##### exemple **year:desc** trier les album par années dans l'ordre décroissant.
    * ##### **ArticleStrings** : Liste de mots considérés comme des articles grammaticaux à retirer lors du tri des            titres (exemple : "the", "a", etc.)
         ##### exemple : **the**, **das**, **der**, **a**, **an**, **el**, **la**
    * ##### **TranscoderPhotoFileSizeLimitMiB** : Taille maximale des fichiers photo pouvant être tagués ou transcodés.
        ##### Valeur : **100** => **100Mio**
# [CREDIT](https://support.plex.tv/articles/201105343-advanced-hidden-server-settings/)
