# AUR (Arch User Repository) - Guide d'installation et utilisation

## Qu'est-ce que l'AUR ?

L'**AUR (Arch User Repository)** est un dépôt communautaire géré par les utilisateurs d'Arch Linux. Il contient des milliers de paquets non disponibles dans les dépôts officiels, notamment des logiciels propriétaires, des versions de développement et des applications moins populaires.

### Comment fonctionne l'AUR ?

L'AUR ne contient **pas de binaires précompilés**, mais des **PKGBUILD** (scripts de construction) créés par la communauté. Quand vous installez un paquet AUR, votre système :
1. Télécharge le PKGBUILD
2. Compile le programme depuis les sources
3. Installe le paquet résultant

## ⚠️ AVERTISSEMENT DE SÉCURITÉ

### Risques de l'AUR

1. **Pas de vérification officielle** : Les paquets ne sont pas validés par l'équipe Arch Linux
2. **Code potentiellement malveillant** : N'importe qui peut soumettre un PKGBUILD
3. **Paquets obsolètes** : Certains mainteneurs abandonnent leurs paquets
4. **Dépendances cassées** : Les mises à jour système peuvent casser les paquets AUR
5. **Compilation depuis sources** : Risques de build malveillant ou corrompu

### Bonnes pratiques de sécurité

✅ **Toujours vérifier le PKGBUILD avant installation**
✅ **Lire les commentaires sur la page AUR du paquet**
✅ **Vérifier la réputation du mainteneur**
✅ **Privilégier les paquets populaires et bien maintenus**
✅ **Vérifier la date de dernière mise à jour**
✅ **Ne jamais installer en tant que root**

❌ **Ne jamais exécuter un PKGBUILD sans l'avoir lu**
❌ **Éviter les paquets avec peu de votes ou sans commentaires**
❌ **Ne pas utiliser `yay -S --noconfirm` (désactive les vérifications)**

## Installation d'un helper AUR

Les helpers AUR facilitent l'installation depuis l'AUR. Les plus populaires sont **Yay** et **Paru**.

### Option 1 : Installer Yay

```bash
# Installer les dépendances nécessaires
sudo pacman -S --needed git base-devel

# Cloner le dépôt Yay
cd /tmp
git clone https://aur.archlinux.org/yay.git
cd yay

# Vérifier le PKGBUILD (IMPORTANT !)
less PKGBUILD

# Compiler et installer
makepkg -si
```

### Option 2 : Installer Paru

```bash
# Installer les dépendances nécessaires
sudo pacman -S --needed git base-devel

# Cloner le dépôt Paru
cd /tmp
git clone https://aur.archlinux.org/paru.git
cd paru

# Vérifier le PKGBUILD (IMPORTANT !)
less PKGBUILD

# Compiler et installer
makepkg -si
```

## Utilisation de Yay

### Rechercher un paquet
```bash
yay -Ss nom_du_paquet
```

### Installer un paquet
```bash
yay -S nom_du_paquet
```
**Yay affichera le PKGBUILD** et demandera confirmation.

### Mettre à jour le système (AUR inclus)
```bash
yay -Syu
```
ou simplement :
```bash
yay
```

### Supprimer un paquet AUR
```bash
yay -Rns nom_du_paquet
```

### Nettoyer les paquets inutiles
```bash
yay -Yc
```

### Voir les statistiques des paquets
```bash
yay -Ps
```

## Utilisation de Paru

Les commandes Paru sont similaires à Yay :

### Installer un paquet
```bash
paru -S nom_du_paquet
```

### Mettre à jour tout le système
```bash
paru -Syu
```
ou :
```bash
paru
```

### Rechercher un paquet
```bash
paru -Ss nom_du_paquet
```

### Afficher les nouvelles sur les paquets
```bash
paru -Pw
```

## Installation manuelle depuis l'AUR (sans helper)

Pour une sécurité maximale, vous pouvez installer manuellement :

```bash
# 1. Installer les outils nécessaires
sudo pacman -S --needed git base-devel

# 2. Cloner le dépôt du paquet
cd /tmp
git clone https://aur.archlinux.org/nom_du_paquet.git
cd nom_du_paquet

# 3. LIRE LE PKGBUILD (CRITIQUE !)
less PKGBUILD
cat .SRCINFO

# 4. Vérifier les commentaires sur la page AUR
# https://aur.archlinux.org/packages/nom_du_paquet

# 5. Compiler et installer
makepkg -si
```

## Vérifier un PKGBUILD

### Points à vérifier dans un PKGBUILD :

```bash
# Ouvrir le PKGBUILD
less PKGBUILD
```

✅ **Source officielle** : Les `source=()` pointent vers le site officiel
✅ **Checksum** : Présence de `sha256sums` ou `sha512sums`
✅ **Commandes standards** : Pas de commandes suspectes (`curl | bash`, `wget ... | sh`)
✅ **Dépendances raisonnables** : `depends=()` et `makedepends=()`

🚨 **Signes suspects** :
- Téléchargements depuis des domaines inconnus
- Commandes exécutées avec `sudo` dans le PKGBUILD
- Téléchargements sans vérification de checksum
- Scripts obscurs ou obfusqués

## Maintenance des paquets AUR

### Lister les paquets AUR installés
```bash
pacman -Qm
```

### Vérifier les paquets orphelins
```bash
yay -Qtd
```

### Nettoyer le cache de build
```bash
yay -Sc
```

## Dépannage

### Erreur de clé GPG
```bash
gpg --recv-keys KEYID
```

### Conflit de fichiers
```bash
yay -S --overwrite '*' nom_du_paquet
```

### Reconstruire un paquet après mise à jour système
```bash
yay -S nom_du_paquet --rebuild
```

## Yay vs Paru

| Fonctionnalité | Yay | Paru |
|----------------|-----|------|
| **Langage** | Go | Rust |
| **Performance** | Rapide | Très rapide |
| **Interface** | Simple | Plus détaillée |
| **Affichage PKGBUILD** | Oui | Oui (avec coloration) |
| **News Arch** | Non | Oui |
| **Popularité** | Plus populaire | En croissance |

## Ressources et alternatives

### Rechercher sur l'AUR
- [AUR Web Interface](https://aur.archlinux.org/)
- Vérifiez les commentaires, votes et date de dernière mise à jour

### Alternatives à l'AUR
- **Flatpak** : Pour les applications avec sandbox
- **Snap** : Alternative universelle (moins utilisée sur Arch)
- **AppImage** : Applications portables
- **Compilation manuelle** : Pour un contrôle total

---

⚠️ **RAPPEL SÉCURITÉ**

L'AUR est puissant mais potentiellement dangereux. Suivez TOUJOURS ces règles :
1. Lisez le PKGBUILD avant installation
2. Vérifiez les commentaires sur la page AUR
3. Ne faites confiance qu'aux paquets bien maintenus
4. Privilégiez les dépôts officiels quand c'est possible

📚 **Ressources utiles**
- [ArchWiki - AUR](https://wiki.archlinux.org/title/Arch_User_Repository)
- [ArchWiki - AUR helpers](https://wiki.archlinux.org/title/AUR_helpers)
- [AUR Official Website](https://aur.archlinux.org/)