# OPI - OBS Package Installer

## Introduction

OPI (OBS Package Installer) est un outil qui simplifie la recherche et l'installation de paquets depuis plusieurs sources, notamment :
- **OBS** (Open Build Service) - le service de build communautaire d'openSUSE
- **Packman** - dépôt de codecs et logiciels multimédia
- **Flathub** - applications Flatpak

## 📥 Installation d'OPI

```bash
# OPI est généralement préinstallé sur Tumbleweed
# Sinon, l'installer via zypper
sudo zypper install opi
```

## 🚀 Utilisation basique

```bash
# Rechercher et installer un paquet
opi nom-paquet

# Exemples
opi codecs          # Cherche les codecs multimédia
opi chrome          # Cherche Google Chrome
opi vscode          # Cherche Visual Studio Code
```

### Flux d'utilisation

1. OPI recherche le paquet dans différentes sources
2. Affiche une liste numérotée de résultats
3. Vous sélectionnez le numéro correspondant
4. OPI ajoute le dépôt (si nécessaire) et installe le paquet

## ⚠️ AVERTISSEMENTS IMPORTANTS

### Risques des dépôts communautaires

> **ATTENTION** : Les paquets de l'OBS (Open Build Service) proviennent de la communauté et ne sont **pas** maintenus officiellement par openSUSE.

#### Risques potentiels

- **Sécurité** : Pas de revue de sécurité systématique
- **Stabilité** : Peut causer des conflits avec des paquets officiels
- **Maintenance** : Le mainteneur peut abandonner le projet
- **Dépendances** : Peut ajouter des dépôts tiers avec priorité élevée
- **Mises à jour** : Risque de casser le système lors d'un `zypper dup`

#### Sources de confiance (ordre de préférence)

1. ✅ **Dépôts officiels openSUSE** (repo-oss, repo-update)
2. ✅ **Packman** (dépôt tiers établi et réputé pour le multimédia)
3. ⚠️ **OBS projets populaires** (vérifier le nombre de téléchargements et l'activité)
4. ⚠️ **OBS projets home:** (dépôts personnels, à éviter si possible)

## 🛡️ Bonnes pratiques avec OPI

### Avant d'installer avec OPI

```bash
# 1. Vérifier d'abord dans les dépôts officiels
zypper search nom-paquet

# 2. Chercher une alternative Flatpak (plus isolée)
flatpak search nom-paquet

# 3. Seulement ensuite, utiliser OPI si vraiment nécessaire
opi nom-paquet
```

### Vérifier la source avant d'installer

Quand OPI affiche les résultats, examinez :

- **Le nom du dépôt** : Préférez les projets officiels ou Packman
- **home:utilisateur** : Dépôts personnels → Risque plus élevé
- **Nombre de résultats** : Un projet très téléchargé est généralement plus fiable
- **Date de dernière mise à jour** : Évitez les projets abandonnés

### Gérer les dépôts ajoutés par OPI

```bash
# Lister tous les dépôts avec priorités
zypper lr -P

# Après installation, désactiver le dépôt si vous ne voulez plus de mises à jour automatiques
sudo zypper mr --disable nom-depot

# Ou le supprimer complètement
sudo zypper rr nom-depot

# Abaisser la priorité d'un dépôt tiers (99 = priorité basse)
sudo zypper mr -p 99 nom-depot
```

## 📦 Cas d'usage courants

### Codecs multimédia (Packman)

```bash
# Packman est un dépôt fiable pour les codecs
opi codecs

# Ou manuellement :
sudo zypper ar -cfp 90 https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Tumbleweed/ packman
sudo zypper dup --from packman --allow-vendor-change
```

### Logiciels propriétaires populaires

```bash
# Ces logiciels ne sont pas dans les dépôts officiels
opi chrome          # Google Chrome
opi vscode          # Visual Studio Code
opi spotify         # Spotify
opi teams           # Microsoft Teams
```

### Logiciels de développement

```bash
opi docker          # Docker (vérifier source)
opi nodejs-lts      # Node.js versions LTS
```

## 🔍 Commandes OPI avancées

```bash
# Rechercher sans installer
opi --search nom-paquet

# Voir l'aide
opi --help
opi -h
```

## ⚖️ OPI vs Alternatives

| Méthode | Sécurité | Facilité | Isolation | Idéal pour |
|---------|----------|----------|-----------|------------|
| **Dépôts officiels** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | N/A | Logiciels standards |
| **Flatpak** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Applications graphiques |
| **OPI (Packman)** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐ | Codecs, multimédia |
| **OPI (OBS officiel)** | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐ | Logiciels spécialisés |
| **OPI (home:)** | ⭐⭐ | ⭐⭐⭐⭐ | ⭐ | Dernier recours |

## 🎯 Recommandations finales

### ✅ Utilisez OPI pour

- Codecs multimédia depuis Packman
- Logiciels propriétaires bien établis (Chrome, VSCode)
- Projets OBS avec bonne réputation et activité récente

### ❌ Évitez OPI pour

- Logiciels disponibles dans les dépôts officiels
- Logiciels critiques pour la sécurité
- Dépôts home: inconnus ou peu maintenus
- Logiciels disponibles en Flatpak

### 🛠️ Procédure recommandée

```bash
# 1. Chercher dans l'officiel
zypper se paquet

# 2. Chercher en Flatpak
flatpak search paquet

# 3. Si vraiment nécessaire, OPI avec vigilance
opi paquet
# Vérifier la source avant de confirmer !

# 4. Après installation, vérifier les dépôts ajoutés
zypper lr -d
```

## 🔗 Ressources

- [OPI GitHub](https://github.com/openSUSE/opi)
- [OBS - Open Build Service](https://build.opensuse.org/)
- [Packman Repository](http://packman.links2linux.org/)
- [Guide de gestion des dépôts openSUSE](https://en.opensuse.org/Package_repositories)