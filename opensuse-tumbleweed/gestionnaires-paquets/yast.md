# YaST - Yet another Setup Tool

![YaST](https://en.opensuse.org/images/8/89/Yast2-gtk-wizard.png)

## Introduction

YaST (Yet another Setup Tool) est l'outil de configuration système emblématique d'openSUSE. Il offre une interface graphique (et textuelle) pour gérer pratiquement tous les aspects du système, y compris les paquets logiciels.

## 🎯 Accès à YaST

### Interface graphique

```bash
# Lancer YaST Control Center
sudo yast2

# Lancer directement le gestionnaire de logiciels
sudo yast2 sw_single
```

### Interface texte (ncurses)

```bash
# Utile en SSH ou sans environnement graphique
sudo yast
```

## 📦 Gestion des logiciels avec YaST

### Gestionnaire de logiciels (sw_single)

Le module de gestion des logiciels offre plusieurs vues :

1. **Vue par groupes** - Logiciels organisés par catégories
2. **Vue dépôts** - Voir les paquets par source
3. **Vue recherche** - Recherche avancée avec filtres
4. **Vue patterns** - Installer des groupes de logiciels cohérents
5. **Vue mises à jour** - Voir uniquement les mises à jour disponibles

### Fonctionnalités principales

- **Installation** : Cocher les paquets souhaités
- **Suppression** : Décocher ou clic droit → Supprimer
- **Mise à jour** : Onglet "Mises à jour" puis "Tout mettre à jour"
- **Informations détaillées** : Description, dépendances, taille, version
- **Résolution automatique des dépendances**

## 🔧 Modules YaST utiles pour la gestion système

### Gestion des dépôts (repositories)

```bash
sudo yast2 repositories
```

Permet de :
- Ajouter/supprimer des dépôts
- Activer/désactiver des dépôts
- Modifier les priorités
- Importer les clés GPG
- Rafraîchir les métadonnées

### Gestionnaire de patchs

```bash
sudo yast2 online_update
```

Gère les mises à jour de sécurité et patches système.

### Gestion des services

```bash
sudo yast2 services-manager
```

Démarrer, arrêter, activer ou désactiver les services système.

### Configuration réseau

```bash
sudo yast2 lan
```

### Partitionnement

```bash
sudo yast2 disk
```

### Bootloader (GRUB)

```bash
sudo yast2 bootloader
```

## 💡 Avantages de YaST

### Points forts

- **Interface unifiée** pour toute la configuration système
- **Résolution intelligente** des conflits de dépendances
- **Gestion complète** des dépôts graphiquement
- **Rollback facilité** via Snapper (intégré)
- **Mode expert** pour les utilisateurs avancés
- **Accessible en SSH** via l'interface texte

### Cas d'usage idéaux

- Configuration initiale du système
- Gestion des dépôts de manière visuelle
- Résolution de conflits complexes de dépendances
- Configuration matérielle (imprimantes, réseau, etc.)
- Utilisateurs préférant une interface graphique

## 🖱️ Raccourcis et astuces

### Dans le gestionnaire de logiciels

- **Ctrl+F** : Rechercher
- **Tab** : Naviguer entre les sections
- **Barre d'espace** : Sélectionner/désélectionner un paquet
- **Clic droit** sur un paquet : Menu contextuel avec options avancées
- **"Versions"** (onglet) : Voir toutes les versions disponibles

### Filtres de recherche avancés

- Recherche par **nom**
- Recherche dans les **descriptions**
- Recherche par **dépendances**
- Filtrer par **statut** (installé, non installé, mise à jour disponible)
- Filtrer par **dépôt**

## 📋 Commandes YaST en ligne de commande

```bash
# Lister les modules YaST disponibles
sudo yast2 --list

# Lancer un module spécifique
sudo yast2 nom-module

# Exemples de modules courants
sudo yast2 sw_single          # Gestionnaire de logiciels
sudo yast2 repositories       # Gestion des dépôts
sudo yast2 online_update      # Mises à jour en ligne
sudo yast2 system_settings    # Paramètres système
sudo yast2 firewall           # Configuration pare-feu
sudo yast2 users              # Gestion des utilisateurs
```

## ⚖️ YaST vs Zypper : Quand utiliser quoi ?

| Critère | YaST | Zypper |
|---------|------|--------|
| **Interface** | Graphique/Texte | Ligne de commande |
| **Vitesse** | Plus lent | Rapide |
| **Scriptabilité** | Limitée | Excellente |
| **Résolution conflits** | Assistance graphique | Messages texte |
| **Configuration système** | Complète | Limitée aux paquets |
| **Idéal pour** | Débutants, config complexe | Experts, automatisation |

## 🔗 Ressources

- [Documentation YaST](https://doc.opensuse.org/documentation/leap/reference/html/book-reference/cha-yast-gui.html)
- [YaST Development](https://yast.opensuse.org/)
- [Wiki openSUSE - YaST](https://en.opensuse.org/Portal:YaST)