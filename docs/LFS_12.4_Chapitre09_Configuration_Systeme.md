
# Linux From Scratch 12.4 - Chapitre 9 : Configuration du Système

Ce chapitre explique comment configurer le nouveau système Linux après l’installation des paquets de base.

---

## Table des Matières

1. Introduction
2. Configuration générale du réseau
3. Manipulation des périphériques et modules
4. Gestion des périphériques
5. Configuration de l'horloge système
6. Configuration de la Console Linux
7. Paramètres régionaux du système
8. Création des fichiers de configuration essentiels
9. Utilisation et configuration de Systemd

---

## 1. Introduction

Après avoir installé le système de base, il faut le **configurer correctement** pour qu’il soit prêt à l’emploi.  
Cela inclut :  
- Le réseau  
- Les périphériques  
- L’horloge système  
- La configuration régionale (locales)  
- Le gestionnaire d’initialisation Systemd

---

## 2. Configuration générale du réseau

On définit le **nom d’hôte** :  
```bash
echo "LFS" > /etc/hostname
```

On configure le fichier **/etc/hosts** :  
```bash
cat > /etc/hosts << "EOF"
127.0.0.1   localhost
127.0.1.1   LFS
::1         localhost ip6-localhost ip6-loopback
EOF
```

---

## 3. Manipulation des périphériques et modules

Les périphériques sont gérés par **udev** qui crée dynamiquement les fichiers dans **/dev**.  
Les modules du noyau peuvent être chargés avec :  
```bash
modprobe <nom_module>
```

---

## 4. Gestion des périphériques

On configure **udev** pour gérer les périphériques automatiquement au démarrage.  
Les règles udev sont placées dans **/etc/udev/rules.d/**.

---

## 5. Configuration de l'horloge système

Pour définir la zone horaire :  
```bash
ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime
```

Puis synchroniser l’horloge matérielle avec l’horloge système :  
```bash
hwclock --systohc
```

---

## 6. Configuration de la Console Linux

On définit la disposition du clavier :  
```bash
cat > /etc/vconsole.conf << "EOF"
KEYMAP=fr
FONT=Lat2-Terminus16
EOF
```

---

## 7. Paramètres régionaux du système

On active les locales :  
```bash
cat > /etc/locale.gen << "EOF"
en_US.UTF-8 UTF-8
fr_FR.UTF-8 UTF-8
EOF
locale-gen
```

Puis on définit la locale par défaut :  
```bash
echo "LANG=fr_FR.UTF-8" > /etc/locale.conf
```

---

## 8. Création des fichiers de configuration essentiels

### /etc/inputrc  
Personnalisation des raccourcis clavier dans le terminal :  
```bash
cat > /etc/inputrc << "EOF"
set editing-mode vi
set completion-ignore-case on
EOF
```

### /etc/shells  
Liste des shells disponibles :  
```bash
cat > /etc/shells << "EOF"
/bin/sh
/bin/bash
EOF
```

---

## 9. Utilisation et configuration de Systemd

Systemd est le gestionnaire d’initialisation par défaut.  
Pour activer un service au démarrage :  
```bash
systemctl enable <service>
```

Exemple :  
```bash
systemctl enable sshd
```

---

Fin du Chapitre 9.
