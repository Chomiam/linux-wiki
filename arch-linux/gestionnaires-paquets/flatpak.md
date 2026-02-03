# Flatpak - Installation et utilisation

## Qu'est-ce que Flatpak ?

**Flatpak** est un système universel de gestion de paquets pour Linux qui permet d'installer des applications dans des environnements isolés appelés "sandbox". 

### Avantages de Flatpak

- **Universalité** : Fonctionne sur toutes les distributions Linux
- **Sécurité** : Isolation des applications (sandboxing) pour limiter l'accès système
- **Versions récentes** : Applications toujours à jour indépendamment de la distribution
- **Aucun conflit** : Les dépendances sont incluses dans chaque paquet
- **Facilité** : Installation simple sans risque pour le système

### Inconvénients

- **Taille** : Les paquets sont plus volumineux (incluent leurs dépendances)
- **Performance** : Légèrement plus lent au démarrage que les paquets natifs
- **Intégration** : Parfois moins bien intégré au système qu'un paquet natif

## Installation de Flatpak sur Arch Linux

### Installer Flatpak
```bash
sudo pacman -S flatpak
```

### Ajouter le dépôt Flathub (source principale)
```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

### Redémarrer la session
Après l'installation, redémarrez votre session pour que les applications Flatpak apparaissent dans le menu.

## Utilisation de Flatpak

### Rechercher une application
```bash
flatpak search nom_application
```

### Installer une application
```bash
flatpak install flathub com.example.Application
```

Exemple réel :
```bash
flatpak install flathub org.mozilla.firefox
```

### Lister les applications installées
```bash
flatpak list
```

### Mettre à jour toutes les applications
```bash
flatpak update
```

### Mettre à jour une application spécifique
```bash
flatpak update com.example.Application
```

### Lancer une application
```bash
flatpak run com.example.Application
```

### Désinstaller une application
```bash
flatpak uninstall com.example.Application
```

### Supprimer les données inutilisées
```bash
flatpak uninstall --unused
```

## Gestion des permissions (Flatseal)

Pour gérer finement les permissions des applications Flatpak, installez **Flatseal** :

```bash
flatpak install flathub com.github.tchx84.Flatseal
```

Flatseal permet de contrôler :
- L'accès aux fichiers et dossiers
- L'accès réseau
- L'accès aux périphériques (webcam, microphone)
- Les variables d'environnement

## Commandes avancées

### Voir les informations d'une application
```bash
flatpak info com.example.Application
```

### Voir les permissions d'une application
```bash
flatpak info --show-permissions com.example.Application
```

### Modifier les permissions depuis la ligne de commande
```bash
flatpak override --user --filesystem=home com.example.Application
```

### Lister les dépôts configurés
```bash
flatpak remotes
```

### Nettoyer le cache
```bash
flatpak uninstall --unused
flatpak repair
```

## Intégration avec le système

### Thèmes GTK/Qt
Pour que les applications Flatpak utilisent vos thèmes système :

```bash
sudo flatpak override --filesystem=~/.themes
sudo flatpak override --filesystem=~/.icons
sudo flatpak override --env=GTK_THEME=nom_du_theme
```

## Flatpak vs Pacman vs AUR

| Critère | Pacman | Flatpak | AUR |
|---------|--------|---------|-----|
| **Source** | Dépôts officiels Arch | Flathub | Utilisateurs |
| **Sécurité** | Élevée | Très élevée (sandbox) | Variable |
| **Versions** | Stables/récentes | Toujours récentes | Dernières versions |
| **Taille** | Optimale | Volumineuse | Optimale |
| **Intégration** | Parfaite | Bonne | Parfaite |
| **Maintenance** | Équipe Arch | Développeurs/communauté | Communauté |

---

📚 **Ressources utiles**
- [Site officiel Flatpak](https://flatpak.org/)
- [Flathub - Catalogue d'applications](https://flathub.org/)
- [ArchWiki - Flatpak](https://wiki.archlinux.org/title/Flatpak)