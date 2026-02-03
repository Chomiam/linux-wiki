# 📦 Gestionnaires de paquets - openSUSE Tumbleweed

## Vue d'ensemble

openSUSE Tumbleweed offre plusieurs outils pour gérer les paquets logiciels, chacun avec ses avantages spécifiques.

## 📋 Contenu

### Gestionnaires principaux
- [Zypper](./zypper.md) - Le gestionnaire de paquets en ligne de commande officiel
- [YaST](./yast.md) - L'outil de configuration système graphique

### Outils complémentaires
- [OPI](./opi.md) - Recherche et installation simplifiée depuis plusieurs sources ⚠️
- [Flatpak](./flatpak.md) - Applications universelles containerisées

### Méthodes avancées
- [Paquets inter-distributions](./paquets-autres-distributions.md) - Installation de paquets d'autres distributions

## 🎯 Quel outil utiliser ?

| Besoin | Outil recommandé |
|--------|------------------|
| Installation/mise à jour standard | `zypper` (CLI) ou YaST (GUI) |
| Logiciel non disponible dans les dépôts officiels | OPI (avec précaution) |
| Application moderne isolée du système | Flatpak |
| Paquet d'une autre distribution | Conversion avec `alien` ou extraction manuelle |
| Configuration système complète | YaST |

## ⚠️ Priorité des sources

1. **Dépôts officiels** (via Zypper/YaST) - Toujours privilégier en premier
2. **Flatpak** - Pour les applications modernes non critiques
3. **OPI** - Uniquement si nécessaire, avec vigilance sur la source
4. **Conversion de paquets** - En dernier recours, risque de conflits