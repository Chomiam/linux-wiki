# 📦 Gestionnaires de paquets - openSUSE Tumbleweed

Guide complet pour gérer les logiciels sous openSUSE Tumbleweed.

## 📑 Contenu

- [Zypper](./zypper.md) - Le gestionnaire de paquets en ligne de commande
- [YaST](./yast.md) - L'outil de configuration système graphique
- [OPI](./opi.md) - Recherche et installation depuis multiples sources
- [Flatpak](./flatpak.md) - Applications conteneurisées
- [Installation inter-distributions](./install-autres-distros.md) - Méthodes pour installer des paquets d'autres distributions

## 🎯 Quelle méthode choisir ?

| Méthode | Avantages | Utilisation recommandée |
|---------|-----------|------------------------|
| **Zypper** | Rapide, puissant, intégré | Gestion quotidienne, scripts |
| **YaST** | Interface graphique, complet | Configuration système, débutants |
| **OPI** | Accès simplifié OBS/Packman | Paquets communautaires, codecs |
| **Flatpak** | Isolation, versions récentes | Applications desktop isolées |
| **AppImage/Alien** | Compatibilité inter-distros | Paquets .deb/.rpm d'autres distros |

## ⚡ Commandes rapides

```bash
# Mettre à jour le système
sudo zypper dup

# Installer un paquet
sudo zypper install nom-paquet

# Rechercher un paquet
zypper search terme

# OPI pour rechercher partout
opi terme-recherche

# Flatpak
flatpak install application
```

## 🔒 Hiérarchie de sécurité recommandée

1. **Dépôts officiels** (zypper/YaST) - Le plus sûr
2. **OBS officiels** (via OPI avec prudence) - Vérifié par la communauté
3. **Flatpak** (Flathub) - Isolé mais vérifier la source
4. **OBS personnels** (via OPI) - ⚠️ Vérifier la réputation
5. **Paquets externes** (.rpm/.deb) - ⚠️ Risque maximal
