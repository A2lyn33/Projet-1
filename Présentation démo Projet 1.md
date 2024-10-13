# Déroulement de la Démo Plex Media Server
---
## 1. Introduction rapide :

- **Expliquez le contexte :** 
  "Nous allons montrer comment mettre en place et configurer un serveur de gestion de contenus multimédia en utilisant Plex Media Server sur un serveur Debian. Vous verrez aussi comment accéder et consommer ces contenus depuis un client Ubuntu."

- **Présentez les machines :** 
  Détaillez l'IP du serveur et du client.

## 2. Accès au serveur Debian :

### Connexion au serveur et afficher l'adresse IP :
- **Montrez que l'IP est correctement définie avec cette commande :**
```
ip a
```
- **Configuration réseau :**
Affichez le fichier de configuration réseau que vous avez modifié :
```
sudo nano /etc/network/interfaces
```
***Montrez la section où vous avez défini l'adresse IP statique. Expliquez brièvement.***

---
## 3 Installation de Plex Media Server :
### Vérifier l'état du service Plex :
- **Montrez que le service Plex est actif :**
```
sudo systemctl status plexmediaserver
```
***Démo : Expliquez que Plex est configuré pour démarrer automatiquement avec le serveur.***

Montrez comment mettre à jour Plex (si nécessaire) :
```
sudo apt update && sudo apt upgrade
```
***Démo : Expliquez l'importance de maintenir le serveur à jour pour la sécurité et les nouvelles fonctionnalités.***

## 4. Accès à l'interface web Plex :
### Ouvrir l'interface Plex depuis le client Ubuntu :
- **Sur le client Ubuntu, ouvrez un navigateur et accédez à :**

- PLEX
- **http://172.16.10.10:32400/web**
- ***Démo : Montrez l'écran de connexion et la page d'accueil de Plex.***

**Configuration des bibliothèques :**
Naviguer vers : Settings > Libraries et montrer comment ajouter des bibliothèques :

- Cliquez sur Add Library.
- Choisissez un type de contenu (par exemple, "Films").
- Sélectionnez un dossier sur le serveur Debian contenant des films.
- Expliquez comment Plex scanne automatiquement les dossiers pour détecter les nouveaux fichiers.

***Démo : Ouvrez une bibliothèque que vous avez déjà ajoutée et montrez quelques films avec les métadonnées récupérées. Montrez les affiches, les synopsis, et autres détails.***

## 5. Configuration avancée :
### Configuration des métadonnées :
- **Naviguer vers : Settings > Libraries > Manage Library > Edit Library**

- Montrez comment personnaliser les paramètres de récupération des métadonnées.
- Expliquez l'importance des métadonnées pour organiser le contenu.

***Démo : Montrez un exemple de film ou de série avec des métadonnées complètes (affiche, titre, synopsis, casting).***

**Configuration des mises à jour automatiques :**
Naviguer vers : Settings > Library Activez les options pour scanner automatiquement les nouvelles données ajoutées.

***Démo : Expliquez que ceci permet à Plex de garder les bibliothèques à jour sans intervention manuelle.***

## 6. Configuration réseau et sécurité :
### Montrez le pare-feu sur le serveur Debian :
```
sudo ufw status
```
**Expliquez que Plex nécessite l'ouverture du port 32400, que vous avez configuré ainsi :**
```
sudo ufw allow 32400/tcp
```
**Sécuriser l'accès avec HTTPS :**
Si vous avez configuré un certificat SSL (par exemple via Nginx), expliquez cela brièvement. Sinon, mentionnez que c'est une étape recommandée pour protéger l'accès distant.

## 7. Accès aux médias depuis le client Ubuntu :
### Accéder et lire un média :
- Naviguer vers : Films ou Séries
- Sélectionnez un film et démarrez la lecture.
- Montrez les options de sous-titres, de qualité de streaming, etc.

***Démo : Expliquez que Plex adapte la qualité en fonction de la bande passante disponible, et montre comment naviguer facilement dans la bibliothèque.***

## 8. Maintenance et gestion :
### Montrer comment mettre à jour Plex via le terminal :
- **Expliquez l'importance de vérifier les mises à jour :**
```
sudo apt update && sudo apt upgrade
```
**Configurer des sauvegardes :**
Mentionnez brièvement que les configurations et les métadonnées peuvent être sauvegardées, soit manuellement en copiant les dossiers de Plex, soit en configurant des scripts de sauvegarde automatiques.
