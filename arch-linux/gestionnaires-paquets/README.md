# 📦 Gestionnaires de paquets - Arch Linux

Guide complet pour gérer les logiciels sous Arch Linux.

## 📑 Contenu

- [Pacman](./pacman.md) - Le gestionnaire de paquets officiel
- [AUR Helpers (yay & paru)](./yay-paru.md) - Accéder aux paquets communautaires
- [Flatpak](./flatpak.md) - Applications conteneurisées

## 🎯 Quelle méthode choisir ?

| Méthode | Avantages | Utilisation recommandée |
|---------|-----------|------------------------|
| **Pacman** | Rapide, intégré, officiel | Paquets des dépôts officiels |
| **AUR (yay/paru)** | Vaste catalogue, communautaire | Logiciels non disponibles officiellement |
| **Flatpak** | Isolation, versions récentes | Applications desktop, compatibilité multi-distros |

## ⚡ Commandes rapides

```bash
# Mettre à jour le système
sudo pacman -Syu

# Installer un paquet
sudo pacman -S nom-paquet

# Rechercher un paquet
pacman -Ss terme-recherche

# AUR avec yay
yay -S paquet-aur

# Flatpak
flatpak install application
```
