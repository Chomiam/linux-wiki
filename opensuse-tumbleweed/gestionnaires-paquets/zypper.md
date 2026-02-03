# Zypper - Gestionnaire de paquets openSUSE

![Zypper](https://en.opensuse.org/images/1/17/Zypper.png)

## Introduction

Zypper est le gestionnaire de paquets en ligne de commande d'openSUSE, équivalent de `apt` (Debian/Ubuntu) ou `pacman` (Arch). Il est puissant, rapide et offre une gestion avancée des dépendances.

## 🚀 Commandes essentielles

### Mise à jour du système

```bash
# Rafraîchir les dépôts
sudo zypper refresh
# ou version courte
sudo zypper ref

# Mettre à jour tous les paquets
sudo zypper update
# ou version courte
sudo zypper up

# Mise à jour distribution (changement de version)
sudo zypper dist-upgrade
sudo zypper dup
```

### Installation de paquets

```bash
# Installer un paquet
sudo zypper install nom-paquet
sudo zypper in nom-paquet

# Installer plusieurs paquets
sudo zypper in paquet1 paquet2 paquet3

# Installer avec confirmation automatique
sudo zypper in -y nom-paquet
```

### Recherche de paquets

```bash
# Rechercher un paquet
zypper search nom
zypper se nom

# Recherche détaillée
zypper se -d nom

# Rechercher dans les descriptions
zypper se -d --match-words mot-clé
```

### Informations sur les paquets

```bash
# Afficher les informations d'un paquet
zypper info nom-paquet
zypper if nom-paquet

# Lister les fichiers d'un paquet installé
rpm -ql nom-paquet

# Trouver quel paquet fournit un fichier
zypper search --provides /chemin/fichier
```

### Suppression de paquets

```bash
# Supprimer un paquet
sudo zypper remove nom-paquet
sudo zypper rm nom-paquet

# Supprimer avec dépendances orphelines
sudo zypper rm -u nom-paquet
```

## 📦 Gestion des dépôts

### Lister et gérer les dépôts

```bash
# Lister tous les dépôts
zypper repos
zypper lr

# Lister avec détails et URLs
zypper lr -d

# Ajouter un dépôt
sudo zypper addrepo URL nom-depot
sudo zypper ar URL nom-depot

# Supprimer un dépôt
sudo zypper removerepo nom-depot
sudo zypper rr nom-depot

# Activer/désactiver un dépôt
sudo zypper modifyrepo --enable nom-depot
sudo zypper modifyrepo --disable nom-depot
```

### Priorités des dépôts

```bash
# Définir la priorité d'un dépôt (plus le nombre est bas, plus la priorité est haute)
sudo zypper mr -p 90 nom-depot
```

## 🧹 Nettoyage du système

```bash
# Nettoyer le cache des paquets
sudo zypper clean
sudo zypper cc

# Supprimer les paquets orphelins
sudo zypper packages --orphaned
sudo zypper rm $(zypper packages --orphaned | awk '{print $5}')

# Supprimer les anciennes versions du kernel
sudo zypper se -si 'kernel*'
# Puis supprimer manuellement les anciennes versions
```

## 🔒 Verrouillage de paquets

```bash
# Empêcher la mise à jour d'un paquet
sudo zypper addlock nom-paquet
sudo zypper al nom-paquet

# Lister les paquets verrouillés
zypper locks
zypper ll

# Retirer le verrou
sudo zypper removelock nom-paquet
sudo zypper rl nom-paquet
```

## 🔍 Commandes avancées

### Gestion des patches

```bash
# Lister les patches disponibles
zypper patches

# Installer tous les patches de sécurité
sudo zypper patch --category security
```

### Patterns (groupes de paquets)

```bash
# Lister les patterns disponibles
zypper search -t pattern
zypper se -t pattern

# Installer un pattern
sudo zypper in -t pattern nom-pattern

# Exemples de patterns utiles
sudo zypper in -t pattern devel_basis  # Outils de développement
sudo zypper in -t pattern games        # Jeux
```

### Vérification et réparation

```bash
# Vérifier les dépendances
sudo zypper verify
sudo zypper ve

# Vérifier et réparer les problèmes
sudo zypper verify --dry-run
sudo zypper install --force-resolution
```

## 💡 Astuces et bonnes pratiques

### Alias utiles

Ajoutez ces alias à votre `~/.bashrc` ou `~/.zshrc` :

```bash
alias zr='sudo zypper refresh'
alias zu='sudo zypper update'
alias zdup='sudo zypper dup'
alias zi='sudo zypper install'
alias zs='zypper search'
alias zrm='sudo zypper remove'
alias zclean='sudo zypper clean --all'
```

### Mise à jour sécurisée

```bash
# Simuler une mise à jour pour voir ce qui va changer
sudo zypper dup --dry-run

# Puis effectuer la vraie mise à jour
sudo zypper dup
```

### Rétrograder un paquet

```bash
# Lister les versions disponibles
zypper se -s nom-paquet

# Installer une version spécifique
sudo zypper in nom-paquet-version
```

## ⚠️ Notes importantes

- Sur Tumbleweed, utilisez **`zypper dup`** plutôt que `zypper up` pour les mises à jour système complètes
- Les dépôts officiels sont toujours préférables aux dépôts tiers
- Faites un snapshot Snapper avant les grosses mises à jour (Tumbleweed le fait automatiquement)

## 🔗 Ressources

- [Documentation officielle Zypper](https://en.opensuse.org/SDB:Zypper_usage)
- [Zypper Cheat Sheet](https://en.opensuse.org/images/1/17/Zypper-cheat-sheet-1.pdf)