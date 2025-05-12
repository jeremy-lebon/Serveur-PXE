# Projet PXE – Déploiement automatisé d'images Windows

## Présentation

Ce projet consiste à mettre en place un serveur PXE complet sous Windows Server permettant :

- Le démarrage de machines clientes sans OS via le réseau (PXE)
- La capture d'images Windows personnalisées à l’aide de WinPE et ImageX
- Le déploiement automatisé d'images via Windows Deployment Services (WDS)
- L’intégration optionnelle au domaine Active Directory

Le projet a été réalisé dans un environnement virtuel avec plusieurs machines simulant un environnement de production.

---

## Contenu du dépôt

- `Serveur PXE - Active Directory.pdf` – Énoncé du projet
- `Serveur PXE.pdf` – Documentation complète des étapes réalisées
- `unattend.xml` – Fichier de réponse utilisé pour l'installation automatisée
- `README.md` – Ce fichier de présentation

---

## Technologies utilisées

- Windows Server 2025 (preview)
- Active Directory (ADDS)
- DNS
- DHCP
- Windows Deployment Services (WDS)
- Windows ADK + WinPE
- ImageX
- VM Ware

---

## Fonctionnalités mises en place

- Attribution d'une IP statique au serveur (192.168.245.10)
- Configuration d’un service DHCP avec options PXE (60, 66, 67)
- Création d’un environnement WinPE personnalisé avec ImageX intégré
- Capture d’une image système Windows 11 (`install.wim`)
- Déploiement PXE avec `boot.wim` extrait de l’ISO Windows
- Ajout d’un script d'installation automatisée (`unattend.xml`)
- Sécurisation de l'environnement : accès restreints, pare-feu, VLAN isolé, vérification d'intégrité

---

## Problèmes rencontrés

- Boucle PXE due à l’absence de système installé et au boot PXE prioritaire
- Partage réseau inaccessible depuis WinPE (résolu par l’ajout de modules dans WinPE)
- Limite de partition MBR sur la machine cible empêchant la capture (résolu par ajout d’un second disque virtuel)
- Message de désapprobation WDS (comportement attendu dans les dernières versions de Windows Server)

---

## Sécurité

- Hash SHA-256 des images pour vérifier leur intégrité (`Get-FileHash`)
- Accès restreint au dossier `RemoteInstall` (droits limités)
- Ouverture stricte des ports nécessaires (UDP 69, DHCP, SMB)
- Utilisation d’un LAN segment isolé
- Mises à jour appliquées (Windows Server et ADK)

---

## Pour aller plus loin

- Intégration de Microsoft Deployment Toolkit (MDT) en remplacement de WDS
- Déploiement multiversion ou multirole via scripts supplémentaires
- Intégration complète avec un système de gestion de parc

---

## Auteur

Projet réalisé par Lebon Jérémy, étudiant en administration réseau et système.
