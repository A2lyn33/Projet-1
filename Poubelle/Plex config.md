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
