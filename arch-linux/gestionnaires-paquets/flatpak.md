# Flatpak sur Arch Linux

![Flatpak](https://flatpak.org/img/logo.svg)

Flatpak permet d'installer des applications conteneurisées, isolées du système principal, avec leurs propres dépendances.

## 📥 Installation

```bash
# Installer Flatpak
sudo pacman -S flatpak

# Ajouter Flathub (dépôt principal)
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# Redémarrer la session pour appliquer les changements
```

## 🔧 Utilisation de base

### Recherche et installation
```bash
# Rechercher une application
flatpak search nom

# Installer une application
flatpak install flathub com.application.Name

# Installation sans confirmation
flatpak install -y flathub com.application.Name
```

### Exécution
```bash
# Lancer une application
flatpak run com.application.Name

# Les applications apparaissent aussi dans le menu des applications
```

### Gestion des applications
```bash
# Lister les applications installées
flatpak list --app

# Mettre à jour toutes les applications
flatpak update

# Mettre à jour une application spécifique
flatpak update com.application.Name

# Désinstaller une application
flatpak uninstall com.application.Name

# Désinstaller avec les données
flatpak uninstall --delete-data com.application.Name
```

## 🧹 Maintenance

```bash
# Nettoyer les runtimes inutilisés
flatpak uninstall --unused

# Réparer une installation
flatpak repair

# Voir l'espace disque utilisé
flatpak list --app --columns=application,size
du -sh ~/.var/app/*
```

## ⚙️ Permissions et sandboxing

### Voir les permissions
```bash
# Permissions d'une application
flatpak info --show-permissions com.application.Name
```

### Modifier les permissions avec Flatseal
```bash
# Installer Flatseal (interface graphique)
flatpak install flathub com.github.tchx84.Flatseal

# Lancer Flatseal
flatpak run com.github.tchx84.Flatseal
```

### Modifier les permissions en ligne de commande
```bash
# Donner accès à un dossier
flatpak override com.application.Name --filesystem=/chemin/dossier

# Retirer l'accès réseau
flatpak override com.application.Name --unshare=network

# Réinitialiser les permissions
flatpak override --reset com.application.Name
```

## 🎨 Intégration avec le système

### Thèmes GTK/Qt
```bash
# Installer les thèmes pour Flatpak
flatpak install flathub org.gtk.Gtk3theme.Breeze
flatpak install flathub org.kde.KStyle.Adwaita

# Les applications utiliseront automatiquement le thème système
```

### Polices
```bash
# Donner accès aux polices système
flatpak override --filesystem=~/.local/share/fonts:ro
flatpak override --filesystem=/usr/share/fonts:ro
```

## 🚀 Applications populaires sur Flathub

```bash
# Navigateurs
flatpak install flathub org.mozilla.firefox
flatpak install flathub com.brave.Browser

# Communication
flatpak install flathub com.discordapp.Discord
flatpak install flathub org.telegram.desktop

# Multimédia
flatpak install flathub org.videolan.VLC
flatpak install flathub org.gimp.GIMP
flatpak install flathub org.inkscape.Inkscape
flatpak install flathub com.spotify.Client

# Bureautique
flatpak install flathub org.libreoffice.LibreOffice
flatpak install flathub md.obsidian.Obsidian

# Développement
flatpak install flathub com.vscodium.codium
flatpak install flathub com.github.gittyup.Gittyup

# Gaming
flatpak install flathub com.valvesoftware.Steam
flatpak install flathub net.lutris.Lutris
```

## ⚖️ Avantages vs Inconvénients

### ✅ Avantages
- Isolation et sandboxing pour la sécurité
- Applications toujours à jour
- Même version sur toutes les distributions
- Pas de conflit de dépendances

### ⚠️ Inconvénients
- Taille plus importante (runtimes inclus)
- Peut être plus lent au démarrage
- Certaines intégrations système limitées
- Nécessite configuration pour accès fichiers

## 🔄 Flatpak vs Pacman/AUR

**Utiliser Pacman/AUR quand :**
- Le paquet est dans les dépôts officiels
- Vous voulez une intégration système maximale
- L'espace disque est limité

**Utiliser Flatpak quand :**
- Application propriétaire ou non empaquetée
- Vous voulez la dernière version
- Isolation/sécurité importante
- Application multimédia ou gaming

## 🛠️ Dépannage

### Application qui ne démarre pas
```bash
# Voir les logs
flatpak run --verbose com.application.Name

# Réinstaller le runtime
flatpak update --force org.freedesktop.Platform
```

### Thème non appliqué
```bash
# Forcer le thème GTK
flatpak override --env=GTK_THEME=nom-theme
```

### Accès fichiers refusé
```bash
# Donner accès au dossier home
flatpak override com.application.Name --filesystem=home

# Ou utiliser Flatseal pour gérer graphiquement
```

## 📚 Ressources

- [Flathub](https://flathub.org/) - Dépôt principal
- [Documentation Flatpak](https://docs.flatpak.org/)
- [Flatseal](https://flathub.org/apps/details/com.github.tchx84.Flatseal) - Gestionnaire de permissions
