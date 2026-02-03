# Pacman - Guide des commandes essentielles

## Qu'est-ce que Pacman ?

**Pacman** (Package Manager) est le gestionnaire de paquets officiel d'Arch Linux. Il permet d'installer, mettre à jour, supprimer et gérer les paquets depuis les dépôts officiels d'Arch Linux.

## Installation et mise à jour

### Mettre à jour le système complet
```bash
sudo pacman -Syu
```
- `-S` : Synchronise les paquets
- `-y` : Rafraîchit la base de données
- `-u` : Met à jour tous les paquets installés

### Installer un paquet
```bash
sudo pacman -S nom_du_paquet
```

### Installer plusieurs paquets
```bash
sudo pacman -S paquet1 paquet2 paquet3
```

### Forcer la mise à jour complète (avec téléchargement des bases)
```bash
sudo pacman -Syyu
```

## Recherche et informations

### Rechercher un paquet dans les dépôts
```bash
pacman -Ss mot_clé
```

### Rechercher un paquet installé localement
```bash
pacman -Qs mot_clé
```

### Afficher les informations d'un paquet (dépôt)
```bash
pacman -Si nom_du_paquet
```

### Afficher les informations d'un paquet installé
```bash
pacman -Qi nom_du_paquet
```

### Lister tous les paquets installés
```bash
pacman -Q
```

### Lister les paquets installés explicitement
```bash
pacman -Qe
```

### Lister les fichiers d'un paquet installé
```bash
pacman -Ql nom_du_paquet
```

### Trouver quel paquet possède un fichier
```bash
pacman -Qo /chemin/vers/fichier
```

## Suppression de paquets

### Supprimer un paquet
```bash
sudo pacman -R nom_du_paquet
```

### Supprimer un paquet et ses dépendances inutilisées
```bash
sudo pacman -Rs nom_du_paquet
```

### Supprimer un paquet, ses dépendances et fichiers de configuration
```bash
sudo pacman -Rns nom_du_paquet
```
**Recommandé** pour une suppression complète.

### Supprimer les paquets orphelins
```bash
sudo pacman -Rns $(pacman -Qtdq)
```

## Nettoyage du cache

### Nettoyer le cache (garder les 3 dernières versions)
```bash
sudo paccache -r
```

### Nettoyer tout le cache sauf les versions installées
```bash
sudo paccache -rk1
```

### Supprimer tout le cache
```bash
sudo pacman -Scc
```
⚠️ **Attention** : Supprime tous les paquets téléchargés.

## Gestion des fichiers de configuration

### Trouver les fichiers .pacnew et .pacsave
```bash
sudo find /etc -name "*.pacnew" -o -name "*.pacsave"
```

### Fusionner les fichiers de configuration
```bash
sudo pacdiff
```

## Astuces avancées

### Ignorer un paquet lors des mises à jour
Éditer `/etc/pacman.conf` et ajouter :
```
IgnorePkg = nom_du_paquet
```

### Télécharger un paquet sans l'installer
```bash
sudo pacman -Sw nom_du_paquet
```

### Lister les paquets installés depuis l'AUR
```bash
pacman -Qm
```

### Vérifier les dépendances cassées
```bash
pacman -Qk
```

## Résolution de problèmes

### Réparer la base de données corrompue
```bash
sudo rm /var/lib/pacman/db.lck
sudo pacman -Syyu
```

### Forcer la réinstallation d'un paquet
```bash
sudo pacman -S --overwrite '*' nom_du_paquet
```

---

📚 **Ressources utiles**
- [Wiki Arch Linux - Pacman](https://wiki.archlinux.org/title/Pacman)
- [ArchWiki - Pacman/Tips and tricks](https://wiki.archlinux.org/title/Pacman/Tips_and_tricks)