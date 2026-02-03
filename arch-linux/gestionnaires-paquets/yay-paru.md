# AUR Helpers - yay & paru

![AUR](https://wiki.archlinux.org/images/thumb/e/e6/Aur-logo.png/400px-Aur-logo.png)

Les AUR helpers facilitent l'installation de paquets depuis l'Arch User Repository (AUR), un dépôt communautaire contenant des milliers de paquets non officiels.

## 🎯 Yay vs Paru

| Caractéristique | Yay | Paru |
|----------------|-----|------|
| Langage | Go | Rust |
| Popularité | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| Vitesse | Rapide | Très rapide |
| Fonctionnalités | Complètes | Complètes + |
| Revue PKGBUILD | Manuel | Interactif |

**Recommandation** : Les deux sont excellents. Yay est plus populaire, Paru est plus moderne avec de meilleures fonctions de sécurité.

## 📥 Installation

### Yay
```bash
# Installer les dépendances
sudo pacman -S --needed git base-devel

# Cloner et installer
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd ..
rm -rf yay
```

### Paru
```bash
# Installer les dépendances
sudo pacman -S --needed git base-devel

# Cloner et installer
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
cd ..
rm -rf paru
```

## 🔧 Utilisation

### Commandes identiques à pacman
```bash
# Mettre à jour le système + AUR
yay -Syu    # ou paru -Syu

# Rechercher un paquet
yay -Ss terme

# Installer un paquet
yay -S nom-paquet

# Supprimer un paquet
yay -R nom-paquet

# Nettoyer les orphelins
yay -Yc
```

### Commandes spécifiques AUR
```bash
# Installer depuis AUR uniquement
yay -S --aur paquet

# Lister les paquets AUR installés
yay -Qm

# Mettre à jour uniquement les paquets AUR
yay -Sua

# Afficher les statistiques AUR
yay -Ps
```

## ⚙️ Configuration

### Yay
```bash
# Éditer la configuration
yay --save --answerclean None --answerdiff None --removemake

# Options recommandées
yay --save --cleanafter --batchinstall
```

### Paru
Fichier : `~/.config/paru/paru.conf`

```ini
[options]
BottomUp
SudoLoop
CleanAfter
BatchInstall
NewsOnUpgrade

[bin]
FileManager = ranger
```

## 🔍 Recherche et informations

```bash
# Recherche avec détails
yay -Ss '^package-name$'

# Informations complètes
yay -Si paquet

# Voir les commentaires AUR
yay -Sc paquet    # avec paru
```

## 🛡️ Sécurité et bonnes pratiques

### ⚠️ Points d'attention

1. **Toujours lire les PKGBUILD** avant d'installer
2. **Vérifier les commentaires** sur la page AUR du paquet
3. **Préférer les paquets populaires** et bien maintenus
4. **Vérifier la date de dernière mise à jour**

### Avec Paru (revue interactive)
```bash
# Paru propose automatiquement de voir le PKGBUILD
paru -S paquet
# Répondre 'Yes' pour examiner les fichiers
```

### Avec Yay (manuel)
```bash
# Voir le PKGBUILD avant installation
yay -G paquet
cd paquet
less PKGBUILD
# Si OK :
makepkg -si
```

## 🧹 Maintenance

```bash
# Nettoyer le cache de build
yay -Sc    # ou paru -Sc

# Supprimer les dépendances inutilisées
yay -Yc

# Nettoyer les paquets orphelins
yay -Rns $(yay -Qtdq)

# Voir les paquets obsolètes (non maintenu)
paru -Gd
```

## 🔧 Dépannage

### Erreur de signature GPG
```bash
# Importer la clé manquante
gpg --recv-keys ID_CLE

# Ou installer sans vérification (déconseillé)
yay -S --skippgpcheck paquet
```

### Build qui échoue
```bash
# Nettoyer et réessayer
rm -rf ~/.cache/yay/paquet
yay -S paquet

# Forcer la reconstruction
yay -S --rebuild paquet
```

### Conflit de dépendances
```bash
# Ignorer temporairement les dépendances
makepkg -si --nodeps
```

## 📊 Statistiques

```bash
# Statistiques du système
yay -Ps

# Nombre de paquets installés depuis AUR
yay -Qm | wc -l

# Paquets AUR les plus volumineux
yay -Qm | while read pkg _; do echo $(pacman -Qi $pkg | grep 'Installed Size' | cut -d':' -f2 | sed 's/ //g') $pkg; done | sort -h
```

## 🌟 Paquets AUR populaires

Quelques exemples de logiciels courants disponibles sur AUR :

```bash
# Navigateurs
yay -S google-chrome
yay -S brave-bin

# Communication
yay -S discord
yay -S slack-desktop

# Développement
yay -S visual-studio-code-bin
yay -S jetbrains-toolbox

# Multimédia
yay -S spotify
yay -S obs-studio-git

# Gaming
yay -S steam
yay -S heroic-games-launcher-bin
```

## 📚 Ressources

- [AUR Official](https://aur.archlinux.org/)
- [Yay GitHub](https://github.com/Jguer/yay)
- [Paru GitHub](https://github.com/morganamilo/paru)
- [AUR Helpers Comparison](https://wiki.archlinux.org/title/AUR_helpers)
