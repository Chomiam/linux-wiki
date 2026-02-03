# Archinstall - Guide d'installation détaillé

## Qu'est-ce qu'Archinstall ?

**Archinstall** est l'installateur officiel d'Arch Linux qui simplifie le processus d'installation. Il offre une interface interactive en ligne de commande qui guide l'utilisateur à travers toutes les étapes d'installation tout en permettant une personnalisation complète du système.

### Avantages d'Archinstall

- **Officiel** : Maintenu par l'équipe Arch Linux
- **Rapide** : Installation en 10-15 minutes
- **Guidé** : Interface interactive avec explications
- **Flexible** : Permet une personnalisation avancée
- **Fiable** : Réduit les erreurs d'installation manuelle

## Pré-requis

### Matériel minimum
- **RAM** : 512 Mo minimum (2 Go recommandé)
- **Stockage** : 2 Go minimum (20 Go recommandé)
- **Architecture** : x86_64 (64 bits)

### Avant de commencer

1. **Télécharger l'ISO Arch Linux** depuis [archlinux.org](https://archlinux.org/download/)
2. **Créer une clé USB bootable** avec Rufus (Windows), Etcher (multi-plateforme) ou `dd` (Linux)
3. **Sauvegarder vos données** si vous installez sur un disque existant
4. **Vérifier la connexion réseau** (câble Ethernet recommandé)

## Démarrage de l'installation

### 1. Booter sur la clé USB

- Redémarrez l'ordinateur
- Accédez au menu de boot (généralement F12, F2, F8 ou Suppr)
- Sélectionnez la clé USB Arch Linux
- Choisissez "Arch Linux install medium"

### 2. Configuration du clavier français

Par défaut, le clavier est en QWERTY (US). **Pour utiliser un clavier AZERTY français** :

```bash
# Charger le layout français
loadkeys fr
```

**Autres layouts disponibles** :
```bash
# Lister tous les layouts disponibles
ls /usr/share/kbd/keymaps/**/*.map.gz | less

# Exemples d'autres layouts :
loadkeys be-latin1  # Belge
loadkeys cf          # Canadien français
loadkeys ch-fr       # Suisse romand
```

**Pourquoi c'est important** : Sans cette commande, les touches de votre clavier ne correspondront pas (A/Q inversés, M inaccessible, etc.).

### 3. Configuration du WiFi avec iwctl

**Si vous êtes connecté par câble Ethernet**, vous pouvez passer cette étape.

**Pour connecter au WiFi** :

```bash
# Lancer l'outil de configuration WiFi
iwctl
```

Une fois dans l'interface `iwctl`, voici les commandes :

```bash
# 1. Lister les interfaces réseau disponibles
device list
```
**Résultat** : Affiche vos interfaces (généralement `wlan0`)

```bash
# 2. Scanner les réseaux WiFi disponibles
station wlan0 scan
```
**Note** : La commande ne retourne rien, c'est normal. Elle lance simplement le scan.

```bash
# 3. Afficher les réseaux détectés
station wlan0 get-networks
```
**Résultat** : Liste des SSID (noms des réseaux WiFi) avec leur signal.

```bash
# 4. Se connecter à un réseau
station wlan0 connect "Nom_du_WiFi"
```
**Note** : Remplacez `"Nom_du_WiFi"` par le nom exact de votre réseau (respecter majuscules/espaces).

Le système demandera le mot de passe :
```
Passphrase: [entrez le mot de passe WiFi]
```

```bash
# 5. Quitter iwctl
exit
```

**Vérification de la connexion** :
```bash
# Vérifier l'état de la connexion
station wlan0 show

# Ou après avoir quitté iwctl :
ip a  # Vérifier que wlan0 a une adresse IP
ping -c 3 archlinux.org  # Tester la connectivité
```

**Problèmes courants** :

- **"Device or resource busy"** : Votre interface est peut-être gérée par un autre service
  ```bash
  # Désactiver rfkill si nécessaire
  rfkill unblock wifi
  ```

- **Réseau caché** : Si votre WiFi n'apparaît pas
  ```bash
  iwctl station wlan0 connect-hidden "SSID_caché"
  ```

- **Oublier un réseau** :
  ```bash
  iwctl known-networks list
  iwctl known-networks "Nom_réseau" forget
  ```

### 4. Synchroniser l'horloge

```bash
timedatectl set-ntp true
```

**Vérifier** :
```bash
timedatectl status
```

## Lancer Archinstall

```bash
archinstall
```

L'interface interactive se lance. Voici le détail de chaque option :

---

## Guide des options Archinstall

### 1. Archinstall language

**Choix** : Langue de l'installateur (pas du système final)

**Options** :
- `English` (par défaut)
- `Français`
- Autres langues disponibles

**Recommandation** : `Français` pour plus de confort

---

### 2. Keyboard layout

**Choix** : Disposition du clavier pour le système installé

**Options courantes** :
- `fr` : AZERTY français
- `us` : QWERTY américain
- `be` : AZERTY belge
- `ch` : QWERTZ suisse

**Recommandation** : `fr` pour clavier français

**Pourquoi c'est important** : Détermine la correspondance des touches pour toute utilisation future du système.

---

### 3. Mirror region

**Choix** : Région des miroirs de téléchargement

**Options** :
- `France`
- `Worldwide` (tous les miroirs)
- Autres pays européens

**Recommandation** : `France` pour des téléchargements plus rapides

**Pourquoi c'est important** : Les miroirs géographiquement proches offrent de meilleures vitesses de téléchargement pour les mises à jour.

---

### 4. Locale language

**Choix** : Langue du système (messages, applications)

**Options** :
- `en_US` : Anglais américain (par défaut)
- `fr_FR.UTF-8` : Français
- Autres langues

**Recommandation** : `fr_FR.UTF-8` pour un système en français

**Pourquoi c'est important** : Définit la langue des menus, messages d'erreur et applications.

---

### 5. Locale encoding

**Choix** : Encodage des caractères

**Options** :
- `UTF-8` (par défaut et recommandé)
- Autres encodages legacy

**Recommandation** : `UTF-8` (standard moderne)

**Pourquoi c'est important** : UTF-8 supporte tous les caractères internationaux et est le standard actuel.

---

### 6. Drive(s)

**Choix** : Disque(s) sur lequel installer Arch Linux

**Options** :
- Liste des disques détectés (ex: `/dev/sda`, `/dev/nvme0n1`)
- Possibilité de sélectionner plusieurs disques

**Recommandation** : Sélectionnez le disque principal

**⚠️ ATTENTION** : Toutes les données du disque seront effacées !

**Comment identifier votre disque** :
- Taille du disque affichée
- Type (SSD, HDD, NVMe)

---

### 7. Disk layout

**Choix** : Schéma de partitionnement du disque

**Options** :

#### a) **Wipe all selected drives and use a best-effort default partition layout**
- **Description** : Efface tout et crée automatiquement les partitions
- **Recommandé pour** : Débutants, installation simple
- **Avantages** : Rapide, sans erreur
- **Partitions créées** : Boot, Swap (optionnelle), Root

#### b) **Manual Partitioning**
- **Description** : Contrôle total du partitionnement
- **Recommandé pour** : Utilisateurs avancés, configurations spécifiques
- **Avantages** : Personnalisation totale (tailles, nombre de partitions)
- **Inconvénients** : Risque d'erreur si mal configuré

#### c) **Pre-mounted configuration**
- **Description** : Utilise des partitions déjà montées
- **Recommandé pour** : Installations très avancées ou configurations existantes

**Recommandation pour débutants** : Option (a) "Wipe all selected drives"

**Pourquoi c'est important** : Un bon partitionnement optimise les performances et facilite la maintenance.

---

### 8. Disk encryption

**Choix** : Chiffrer ou non le disque

**Options** :
- `Encryption password` : Chiffrement LUKS avec mot de passe
- `No encryption` : Pas de chiffrement (par défaut)

**Avantages du chiffrement** :
- ✅ Sécurité maximale des données
- ✅ Protection en cas de vol de l'ordinateur
- ✅ Confidentialité totale

**Inconvénients du chiffrement** :
- ❌ Légère baisse de performance (5-10%)
- ❌ Mot de passe requis à chaque démarrage
- ❌ Données irrécupérables si mot de passe oublié

**Recommandation** :
- **Ordinateur portable** : `Encryption password` (risque de vol)
- **PC fixe à domicile** : `No encryption` (sauf données sensibles)

**Pourquoi c'est important** : Le chiffrement protège vos données mais ne peut être ajouté après installation sans réinstaller.

---

### 9. Bootloader

**Choix** : Chargeur de démarrage (boot loader)

**Options** :

#### a) **GRUB**
- **Description** : Bootloader le plus populaire et universel
- **Avantages** : Compatible avec tout, dual-boot facile, interface graphique
- **Inconvénients** : Plus lourd, configuration plus complexe
- **Recommandé pour** : Dual-boot Windows/Linux, débutants

#### b) **systemd-boot**
- **Description** : Bootloader minimaliste et moderne
- **Avantages** : Léger, rapide, simple, intégré à systemd
- **Inconvénients** : Nécessite UEFI, moins flexible pour dual-boot
- **Recommandé pour** : Installations UEFI modernes, Linux seul

#### c) **EFISTUB**
- **Description** : Boot direct sans bootloader intermédiaire
- **Avantages** : Très rapide, minimal
- **Inconvénients** : Pas de menu, configuration UEFI manuelle
- **Recommandé pour** : Utilisateurs avancés, systèmes UEFI

**Recommandation** :
- **Dual-boot Windows** : `GRUB`
- **Linux seul (UEFI)** : `systemd-boot`
- **Débutants** : `GRUB` (plus polyvalent)

**Pourquoi c'est important** : Le bootloader permet de démarrer votre système. GRUB est le plus universel mais systemd-boot est plus moderne et rapide sur UEFI.

---

### 10. Swap

**Choix** : Activer ou non la mémoire d'échange (swap)

**Options** :
- `True` : Activer le swap (recommandé)
- `False` : Pas de swap

**Qu'est-ce que le swap ?**
Espace disque utilisé comme extension de la RAM quand celle-ci est saturée.

**Recommandation** :
- **RAM < 8 Go** : `True` (essentiel)
- **RAM 8-16 Go** : `True` (utile)
- **RAM > 16 Go** : `True` (pour hibernation)

**Taille recommandée** :
- RAM ≤ 2 Go → Swap = 2× RAM
- RAM 2-8 Go → Swap = RAM
- RAM > 8 Go → Swap = 8 Go (ou taille RAM pour hibernation)

**Pourquoi c'est important** : Le swap évite les plantages quand la RAM est pleine et permet l'hibernation.

---

### 11. Hostname

**Choix** : Nom de votre machine sur le réseau

**Format** : Lettres, chiffres, tirets (pas d'espaces)

**Exemples** :
- `archlinux`
- `mon-pc`
- `workstation`
- `laptop-arch`

**Recommandation** : Choisissez un nom court et descriptif

**Pourquoi c'est important** : Identifie votre machine sur un réseau local.

---

### 12. Root password

**Choix** : Mot de passe du super-utilisateur (root)

**Recommandation** :
- **Mot de passe fort** : 12+ caractères, majuscules, minuscules, chiffres, symboles
- **Unique** : Ne pas réutiliser d'autres mots de passe
- **Mémorisable** : Vous en aurez besoin pour les tâches administratives

**⚠️ IMPORTANT** : Ce compte a tous les droits sur le système. Un mot de passe faible = système compromis.

**Alternative** : Certains préfèrent désactiver root et utiliser uniquement `sudo` avec un compte utilisateur.

---

### 13. User account

**Choix** : Créer un compte utilisateur standard

**Options** :
- `Add a user` : Créer un utilisateur (recommandé)
- `Skip` : Utiliser uniquement root (déconseillé)

**Configuration du compte utilisateur** :

#### a) **Username**
- Format : Lettres minuscules, chiffres, tiret bas
- Exemples : `axel`, `user`, `mon_nom`

#### b) **Password**
- Mot de passe du compte utilisateur
- Peut être moins complexe que root (mais restez raisonnable)

#### c) **Sudo privileges**
- `Yes` : L'utilisateur peut exécuter des commandes administrateur avec `sudo`
- `No` : Utilisateur standard sans privilèges

**Recommandation** : `Yes` pour un usage quotidien pratique

**Pourquoi c'est important** : Utiliser un compte utilisateur standard (avec sudo) est plus sûr qu'utiliser root en permanence. Les erreurs en tant qu'utilisateur sont moins catastrophiques.

---

### 14. Profile

**Choix** : Type d'installation (environnement de bureau ou serveur)

**Options principales** :

#### a) **Desktop**
- **Description** : Installation avec interface graphique
- **Sous-options** :
  - **KDE Plasma** : Moderne, personnalisable, Windows-like
  - **GNOME** : Épuré, moderne, macOS-like
  - **XFCE** : Léger, simple, efficace
  - **i3** : Gestionnaire de fenêtres tiling (avancé)
  - **Cinnamon** : Traditionnel, intuitif
  - **Budgie** : Moderne et élégant
  - Et bien d'autres...

**Recommandations Desktop** :
- **Débutants** : KDE Plasma ou GNOME
- **Vieux PC** : XFCE ou LXQt
- **Utilisateurs avancés** : i3, Sway, Awesome

#### b) **Minimal**
- **Description** : Installation minimale sans interface graphique
- **Recommandé pour** : Serveurs, utilisateurs avancés, installations personnalisées

#### c) **Server**
- **Description** : Profil optimisé serveur
- **Recommandé pour** : Serveurs, NAS, applications réseau

**Pourquoi c'est important** : Détermine l'interface utilisateur et les logiciels de base installés.

---

### 15. Audio server

**Choix** : Serveur audio pour la gestion du son

**Options** :

#### a) **Pipewire** (recommandé)
- **Avantages** : Moderne, faible latence, remplace PulseAudio et JACK
- **Recommandé pour** : Tous les usages (bureautique, gaming, audio pro)

#### b) **PulseAudio**
- **Avantages** : Stable, mature, bien supporté
- **Inconvénients** : Technologie plus ancienne
- **Recommandé pour** : Compatibilité maximale avec ancien matériel

#### c) **No audio server**
- **Description** : Pas de serveur audio (ALSA uniquement)
- **Recommandé pour** : Serveurs, systèmes sans son

**Recommandation** : `Pipewire` (standard moderne)

**Pourquoi c'est important** : Pipewire offre de meilleures performances et une meilleure gestion audio/vidéo que PulseAudio.

---

### 16. Kernel

**Choix** : Version du noyau Linux

**Options** :

#### a) **linux** (recommandé)
- **Description** : Noyau stable officiel
- **Avantages** : Stable, testé, bien supporté
- **Recommandé pour** : Usage général

#### b) **linux-lts**
- **Description** : Noyau Long Term Support
- **Avantages** : Support prolongé, très stable
- **Recommandé pour** : Serveurs, stabilité maximale, vieux matériel

#### c) **linux-zen**
- **Description** : Noyau optimisé pour desktop et gaming
- **Avantages** : Meilleures performances gaming et réactivité
- **Recommandé pour** : Gaming, workstations performantes

#### d) **linux-hardened**
- **Description** : Noyau renforcé pour la sécurité
- **Avantages** : Sécurité maximale
- **Recommandé pour** : Systèmes nécessitant haute sécurité

**Recommandation** :
- **Usage général** : `linux`
- **Gaming/Performance** : `linux-zen`
- **Serveur/Stabilité** : `linux-lts`

**Pourquoi c'est important** : Le noyau gère le matériel. Le choix affecte compatibilité, performances et stabilité.

---

### 17. Additional packages

**Choix** : Paquets supplémentaires à installer

**Format** : Liste séparée par espaces

**Exemples utiles** :
```
firefox vlc git neovim htop neofetch
```

**Catégories recommandées** :

**Navigateurs** :
- `firefox` : Navigateur Mozilla
- `chromium` : Version open source de Chrome

**Multimédia** :
- `vlc` : Lecteur vidéo universel
- `mpv` : Lecteur léger et performant

**Outils système** :
- `htop` : Moniteur système interactif
- `neofetch` : Affichage infos système
- `git` : Contrôle de version

**Éditeurs de texte** :
- `neovim` : Vim amélioré
- `nano` : Éditeur simple (souvent préinstallé)

**Pourquoi c'est important** : Vous pouvez installer ces paquets plus tard avec `pacman`, mais les ajouter maintenant fait gagner du temps.

---

### 18. Network configuration

**Choix** : Gestion du réseau

**Options** :

#### a) **NetworkManager** (recommandé)
- **Description** : Gestionnaire réseau moderne avec GUI
- **Avantages** : Interface graphique, WiFi facile, auto-configuration
- **Recommandé pour** : Desktops, laptops

#### b) **systemd-networkd**
- **Description** : Gestionnaire réseau minimaliste
- **Avantages** : Léger, intégré à systemd
- **Recommandé pour** : Serveurs, connexion filaire stable

#### c) **Manual configuration**
- **Description** : Configuration manuelle
- **Recommandé pour** : Utilisateurs très avancés

**Recommandation** : `NetworkManager` pour la simplicité

**Pourquoi c'est important** : NetworkManager simplifie grandement la gestion du WiFi et des connexions réseau.

---

### 19. Timezone

**Choix** : Fuseau horaire

**Format** : Région/Ville

**Exemples** :
- `Europe/Paris` : France métropolitaine
- `Europe/Brussels` : Belgique
- `America/Montreal` : Canada (Québec)
- `Europe/Zurich` : Suisse

**Recommandation** : Sélectionnez votre fuseau horaire local

**Pourquoi c'est important** : Affecte l'heure système, les logs et la synchronisation.

---

### 20. Automatic time sync (NTP)

**Choix** : Synchronisation automatique de l'heure

**Options** :
- `True` : Active la synchronisation NTP (recommandé)
- `False` : Désactive la synchronisation

**Recommandation** : `True` (essentiel pour une heure précise)

**Pourquoi c'est important** : Maintient l'horloge système précise, important pour les certificats SSL, logs et authentification.

---

## Installation finale

Après avoir configuré toutes les options :

1. **Vérifiez le récapitulatif** affiché par archinstall
2. **Confirmez l'installation** en appuyant sur Entrée
3. **Attendez la fin** (10-30 minutes selon connexion et options)
4. **Retirez la clé USB** quand demandé
5. **Redémarrez** le système

```bash
# Si archinstall ne redémarre pas automatiquement
reboot
```

## Premier démarrage

### Se connecter

1. **Login** : Entrez votre nom d'utilisateur
2. **Password** : Entrez votre mot de passe

### Premières commandes utiles

```bash
# Mettre à jour le système
sudo pacman -Syu

# Vérifier l'état du réseau
ip a
ping archlinux.org

# Installer des paquets supplémentaires
sudo pacman -S nom_du_paquet
```

## Configuration post-installation recommandée

### 1. Activer les services essentiels

```bash
# Si NetworkManager n'est pas actif
sudo systemctl enable --now NetworkManager

# Pare-feu (optionnel mais recommandé)
sudo pacman -S ufw
sudo systemctl enable --now ufw
sudo ufw enable
```

### 2. Installer un helper AUR

```bash
# Installer Yay (voir guide dans gestionnaires-paquets/yay-paru.md)
sudo pacman -S --needed git base-devel
cd /tmp
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

### 3. Optimiser les miroirs

```bash
# Installer reflector pour optimiser les miroirs
sudo pacman -S reflector
sudo reflector --country France --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```

### 4. Installer des polices supplémentaires

```bash
# Polices essentielles
sudo pacman -S ttf-dejavu ttf-liberation noto-fonts

# Polices Windows (pour compatibilité)
yay -S ttf-ms-fonts
```

## Résolution de problèmes courants

### Pas d'accès Internet après installation

```bash
# Vérifier NetworkManager
sudo systemctl status NetworkManager
sudo systemctl start NetworkManager

# Connexion WiFi manuelle
nmcli device wifi list
nmcli device wifi connect "SSID" password "mot_de_passe"
```

### Écran noir au démarrage (pilotes GPU)

```bash
# Depuis le mode recovery ou TTY (Ctrl+Alt+F2)
# Pour NVIDIA
sudo pacman -S nvidia nvidia-utils

# Pour AMD
sudo pacman -S xf86-video-amdgpu

# Pour Intel
sudo pacman -S xf86-video-intel
```

### Dual-boot Windows non détecté

```bash
# Installer os-prober pour détecter Windows
sudo pacman -S os-prober

# Activer os-prober dans GRUB
sudo nano /etc/default/grub
# Décommenter : GRUB_DISABLE_OS_PROBER=false

# Régénérer la configuration GRUB
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## Comparaison : Archinstall vs Installation manuelle

| Critère | Archinstall | Installation manuelle |
|---------|-------------|----------------------|
| **Durée** | 10-15 min | 45-90 min |
| **Complexité** | Facile | Avancée |
| **Personnalisation** | Élevée | Totale |
| **Risque d'erreur** | Faible | Moyen/Élevé |
| **Apprentissage** | Limité | Complet |
| **Recommandé pour** | Débutants, rapidité | Apprentissage, besoins spécifiques |

## Ressources utiles

- [ArchWiki - Archinstall](https://wiki.archlinux.org/title/Archinstall)
- [ArchWiki - Installation guide](https://wiki.archlinux.org/title/Installation_guide)
- [ArchWiki - General recommendations](https://wiki.archlinux.org/title/General_recommendations)
- [Arch Linux Forums](https://bbs.archlinux.org/)

---

💡 **Conseil final** : Archinstall est un excellent moyen de découvrir Arch Linux. Une fois à l'aise, vous pourrez explorer l'installation manuelle pour comprendre en profondeur le fonctionnement du système.