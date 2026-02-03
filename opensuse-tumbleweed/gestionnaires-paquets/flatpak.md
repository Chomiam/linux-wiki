# Flatpak sur openSUSE Tumbleweed

![Flatpak](https://flatpak.org/img/flatpak-logo.svg)

## Introduction

Flatpak est un système de gestion de paquets pour applications Linux qui offre plusieurs avantages :
- **Isolation** : Les applications tournent dans un sandbox sécurisé
- **Universalité** : Même paquet pour toutes les distributions
- **Mises à jour indépendantes** : Pas liées aux mises à jour système
- **Versions récentes** : Applications souvent plus à jour que les dépôts distro

## 📥 Installation de Flatpak

```bash
# Installer Flatpak
sudo zypper install flatpak

# Ajouter le dépôt Flathub (principal dépôt d'applications)
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

# Redémarrer la session pour activer les intégrations
```

## 🚀 Utilisation basique

### Rechercher des applications

```bash
# Rechercher une application
flatpak search nom-application

# Exemple
flatpak search firefox
flatpak search gimp
```

### Installer des applications

```bash
# Installer une application
flatpak install flathub com.application.ID

# Exemples courants
flatpak install flathub org.mozilla.firefox
flatpak install flathub com.spotify.Client
flatpak install flathub com.discordapp.Discord
flatpak install flathub org.gimp.GIMP
flatpak install flathub org.blender.Blender
flatpak install flathub com.obsproject.Studio  # OBS Studio
```

### Lancer des applications

```bash
# Lancer depuis le menu d'applications (recommandé)
# ou en ligne de commande
flatpak run com.application.ID

# Exemple
flatpak run org.mozilla.firefox
```

### Mettre à jour

```bash
# Mettre à jour toutes les applications Flatpak
flatpak update

# Mettre à jour une application spécifique
flatpak update com.application.ID
```

### Supprimer des applications

```bash
# Désinstaller une application
flatpak uninstall com.application.ID

# Désinstaller avec suppression des données
flatpak uninstall --delete-data com.application.ID

# Nettoyer les runtimes inutilisés
flatpak uninstall --unused
```

## 📋 Gestion des applications

### Lister les applications installées

```bash
# Lister toutes les applications Flatpak
flatpak list

# Lister uniquement les applications (pas les runtimes)
flatpak list --app

# Format détaillé avec colonnes
flatpak list --app --columns=name,application,version,size
```

### Informations sur une application

```bash
# Voir les détails d'une application
flatpak info com.application.ID

# Voir les permissions
flatpak info --show-permissions com.application.ID
```

## 🔧 Configuration avancée

### Gérer les permissions (Flatseal)

```bash
# Installer Flatseal (outil graphique de gestion des permissions)
flatpak install flathub com.github.tchx84.Flatseal
```

Flatseal permet de modifier les permissions de chaque application Flatpak :
- Accès au système de fichiers
- Accès réseau
- Accès aux périphériques
- Variables d'environnement
- Et bien plus

### Modifier les permissions en ligne de commande

```bash
# Donner accès à un dossier spécifique
flatpak override com.application.ID --filesystem=/chemin/vers/dossier

# Exemples
flatpak override org.gimp.GIMP --filesystem=~/Images
flatpak override org.blender.Blender --filesystem=~/Projets

# Retirer un accès
flatpak override com.application.ID --nofilesystem=/chemin/vers/dossier

# Réinitialiser les overrides
flatpak override --reset com.application.ID
```

### Gérer les dépôts

```bash
# Lister les dépôts configurés
flatpak remotes

# Ajouter un dépôt
flatpak remote-add nom-depot url

# Supprimer un dépôt
flatpak remote-delete nom-depot

# Modifier un dépôt
flatpak remote-modify nom-depot --url=nouvelle-url
```

## 🎮 Applications Flatpak populaires

### Navigateurs

```bash
flatpak install flathub org.mozilla.firefox
flatpak install flathub com.google.Chrome
flatpak install flathub com.brave.Browser
flatpak install flathub org.chromium.Chromium
```

### Multimédia

```bash
flatpak install flathub org.videolan.VLC
flatpak install flathub com.spotify.Client
flatpak install flathub org.audacityteam.Audacity
flatpak install flathub org.kde.kdenlive  # Montage vidéo
flatpak install flathub com.obsproject.Studio  # OBS
```

### Création graphique

```bash
flatpak install flathub org.gimp.GIMP
flatpak install flathub org.inkscape.Inkscape
flatpak install flathub org.blender.Blender
flatpak install flathub org.krita.Krita
```

### Communication

```bash
flatpak install flathub com.discordapp.Discord
flatpak install flathub org.signal.Signal
flatpak install flathub org.telegram.desktop
flatpak install flathub com.slack.Slack
```

### Gaming

```bash
flatpak install flathub com.valvesoftware.Steam
flatpak install flathub net.lutris.Lutris
flatpak install flathub org.libretro.RetroArch
flatpak install flathub com.heroicgameslauncher.hgl
```

## 🧹 Maintenance et nettoyage

```bash
# Nettoyer les runtimes inutilisés
flatpak uninstall --unused

# Voir l'espace disque utilisé
flatpak list --app --columns=name,size
du -sh ~/.var/app/*

# Nettoyer le cache
rm -rf ~/.var/app/*/cache/*

# Réparer l'installation Flatpak
flatpak repair
```

## 💡 Avantages et inconvénients

### ✅ Avantages

- **Sécurité** : Isolation via sandbox
- **Stabilité** : N'affecte pas le système de base
- **Universalité** : Fonctionne sur toutes les distributions
- **Fraîcheur** : Applications souvent plus récentes
- **Coexistence** : Peut cohabiter avec des versions système

### ❌ Inconvénients

- **Taille** : Applications plus volumineuses (runtimes partagés)
- **Performance** : Légère surcharge (généralement négligeable)
- **Intégration** : Parfois moins bien intégrée au système
- **Permissions** : Nécessite une configuration pour certains accès

## 🎯 Quand utiliser Flatpak ?

### ✅ Recommandé pour

- Applications graphiques modernes
- Logiciels propriétaires (Discord, Spotify, etc.)
- Applications qui nécessitent des versions récentes
- Isoler des applications potentiellement à risque
- Tester des applications sans affecter le système

### ❌ À éviter pour

- Outils système bas niveau
- Serveurs et démons
- Outils en ligne de commande
- Logiciels déjà disponibles et bien maintenus dans les dépôts officiels

## 🔗 Ressources

- [Flathub - Magasin d'applications](https://flathub.org/)
- [Documentation officielle Flatpak](https://docs.flatpak.org/)
- [Flatseal sur Flathub](https://flathub.org/apps/com.github.tchx84.Flatseal)
- [Flatpak sur openSUSE Wiki](https://en.opensuse.org/Flatpak)