# Pacman - Gestionnaire de paquets officiel

![Pacman](https://wiki.archlinux.org/images/c/c9/Pacman.png)

Pacman est le gestionnaire de paquets d'Arch Linux, simple, rapide et puissant.

## 🔧 Commandes essentielles

### Mise à jour du système
```bash
# Mettre à jour la base de données et tous les paquets
sudo pacman -Syu

# Forcer le rafraîchissement de toutes les bases de données
sudo pacman -Syyu
```

### Installation de paquets
```bash
# Installer un ou plusieurs paquets
sudo pacman -S paquet1 paquet2

# Installer sans confirmation
sudo pacman -S --noconfirm paquet

# Réinstaller un paquet
sudo pacman -S --overwrite '*' paquet
```

### Recherche de paquets
```bash
# Rechercher dans les dépôts
pacman -Ss terme

# Rechercher dans les paquets installés
pacman -Qs terme

# Afficher les informations d'un paquet
pacman -Si paquet        # Dépôt
pacman -Qi paquet        # Installé
```

### Suppression de paquets
```bash
# Supprimer un paquet
sudo pacman -R paquet

# Supprimer avec les dépendances inutilisées
sudo pacman -Rs paquet

# Supprimer avec config et dépendances
sudo pacman -Rns paquet
```

### Nettoyage
```bash
# Nettoyer le cache (garder 3 versions)
sudo paccache -rk3

# Supprimer tous les paquets du cache
sudo pacman -Scc

# Supprimer les orphelins
sudo pacman -Rns $(pacman -Qtdq)
```

## ⚙️ Configuration

Fichier de configuration : `/etc/pacman.conf`

### Options utiles à activer

```ini
# Activer la couleur
Color

# Afficher le Pac-Man en animation
ILoveCandy

# Téléchargements parallèles
ParallelDownloads = 5

# Activer multilib (paquets 32-bit sur système 64-bit)
[multilib]
Include = /etc/pacman.d/mirrorlist
```

## 🪞 Gestion des miroirs

### Avec reflector (recommandé)
```bash
# Installer reflector
sudo pacman -S reflector

# Sélectionner les 20 miroirs les plus rapides en France
sudo reflector --country France --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist

# Automatiser avec un timer systemd
sudo systemctl enable --now reflector.timer
```

## 📊 Informations système

```bash
# Lister tous les paquets installés
pacman -Q

# Lister les paquets explicitement installés
pacman -Qe

# Lister les paquets orphelins
pacman -Qdt

# Voir les fichiers d'un paquet
pacman -Ql paquet

# Trouver à quel paquet appartient un fichier
pacman -Qo /chemin/fichier
```

## 🔐 Vérification et intégrité

```bash
# Vérifier l'intégrité de tous les paquets
sudo pacman -Qk

# Vérification approfondie
sudo pacman -Qkk
```

## 🚨 Dépannage

### Base de données corrompue
```bash
sudo rm /var/lib/pacman/db.lck
sudo pacman -Syu
```

### Conflits de fichiers
```bash
# Forcer l'écrasement
sudo pacman -S --overwrite '*' paquet
```

### Restaurer un paquet supprimé
```bash
# Si encore dans le cache
sudo pacman -U /var/cache/pacman/pkg/paquet-version.pkg.tar.zst
```

## 📚 Ressources

- [Wiki officiel Pacman](https://wiki.archlinux.org/title/Pacman)
- [Pacman Rosetta](https://wiki.archlinux.org/title/Pacman/Rosetta) - Équivalences avec autres gestionnaires
