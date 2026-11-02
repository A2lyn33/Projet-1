# Serveur multimédia sous Debian
**Projet collectif de formation · Wild Code School · 2024**

Mettre à disposition des contenus multimédias depuis un serveur Debian 12, avec Plex Media Server et des clients Windows et Ubuntu.

## Ma contribution — Adeline

- **Sprint 1 :** recherche d'informations, installation du serveur Debian et du client Windows.
- **Sprint 2 :** rôle de Product Owner, participation à l'installation des protocoles NFS et SMB, réalisation du support de présentation finale.

Ces contributions reprennent la répartition consignée dans la documentation d'origine. Le résultat présenté est un travail d'équipe.

## Environnement et choix techniques

| Élément | Configuration documentée |
| --- | --- |
| Serveur | Debian 12, Plex Media Server |
| Clients | Windows et Ubuntu |
| Accès Internet | Interface NAT, adresse obtenue par DHCP |
| Réseau interne du serveur | `enp0s8`, adresse `172.16.10.10` |
| Réseau interne du client Ubuntu | `enp0s8`, adresse `172.16.10.20` |
| Partages étudiés | NFS et SMB |

Les adresses appartiennent au laboratoire de formation. Elles doivent être adaptées à un autre environnement.

## Difficultés et solutions consignées

| Difficulté | Solution documentée par l'équipe |
| --- | --- |
| Accès au réseau local et à Internet | Séparation des interfaces : NAT pour Internet et réseau interne pour les échanges entre machines. |
| Routage entre interfaces | Vérification des routes du réseau interne et de la passerelle utilisée pour Internet. |
| Écriture impossible sur le partage NFS | Alignement des permissions utilisateur côté serveur et côté client. La documentation rapporte ensuite un dépôt de fichiers fonctionnel depuis le client. |

## Documentation

- [Installation et administration](INSTALL.md)
- [Guide utilisateur Plex](USER_GUIDE.md)
- [Dépôt collectif d'origine](https://github.com/WildCodeSchool/TSSR-2409-P1-G4-Serveur-de-contenus-multimedia)
- [Brouillons et supports de travail historiques](Poubelle/)

Les documents d'installation et leurs captures correspondent au contexte de 2024. Ils comprennent des ressources externes citées ; toutes les images ne sont pas des captures personnelles.

## Équipe

| Membre | Rôles et contributions documentés |
| --- | --- |
| Adeline | Debian, client Windows, NFS/SMB, Product Owner au sprint 2, présentation finale |
| Julien | Debian, client Ubuntu, NFS/SMB, bibliothèques et métadonnées, Scrum Master au sprint 2 |
| Bruno | Documentation générale, installation et utilisation ; NFS/SMB ; Product Owner au sprint 1 |
| Martin | Plex, bibliothèques et métadonnées, recherche et documentation ; Scrum Master au sprint 1 |

## Limites et suite possible

La présentation a été relue en novembre 2026 ; l'environnement complet n'a pas été redéployé à cette occasion.

Pour une nouvelle démonstration : joindre les versions exactes, un schéma, un test d'accès depuis chaque client et des captures personnelles. Les améliorations envisagées dans le projet initial étaient le renforcement de la sécurité et un serveur de secours.

[Retour au portfolio](https://github.com/A2lyn33)
