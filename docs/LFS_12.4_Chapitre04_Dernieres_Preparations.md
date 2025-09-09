
# Linux From Scratch 12.4 - Chapitre 4 : Dernières préparations

Ce chapitre couvre les étapes finales avant de commencer la construction des outils et du système LFS.

---

## Table des Matières

1. Introduction
2. Créer une structure des répertoires limitée dans le système LFS
3. Ajouter l'utilisateur LFS
4. Configurer l'environnement
5. À propos des SBU
6. À propos des suites de tests

---

## 1. Introduction

Avant de compiler les outils nécessaires à LFS, il faut :
- Préparer l'environnement de travail.  
- Créer un utilisateur dédié pour éviter toute modification accidentelle du système hôte.  

---

## 2. Créer une structure des répertoires limitée dans le système LFS

On crée les répertoires de base pour l'installation :  
```bash
mkdir -pv $LFS/{bin,etc,lib,sbin,usr,var}
```

Cette structure initiale servira de squelette pour le futur système.

---

## 3. Ajouter l'utilisateur LFS

On crée un utilisateur **lfs** pour construire le système en toute sécurité :  
```bash
groupadd lfs
useradd -s /bin/bash -g lfs -m -k /dev/null lfs
passwd lfs
```

Ensuite, on donne à cet utilisateur les droits nécessaires :  
```bash
chown -v lfs $LFS/{usr,lib,var,etc,bin,sbin,tools}
chmod -v a+wt $LFS/sources
```

---

## 4. Configurer l'environnement

On passe sur l'utilisateur LFS :  
```bash
su - lfs
```

On définit les variables d'environnement :  
```bash
cat > ~/.bash_profile << "EOF"
exec env -i HOME=$HOME TERM=$TERM PS1='\\u:\\w\\$ ' /bin/bash
EOF

cat > ~/.bashrc << "EOF"
set +h
umask 022
LFS=/mnt/lfs
LC_ALL=POSIX
LFS_TGT=$(uname -m)-lfs-linux-gnu
PATH=/usr/bin
export LFS LC_ALL LFS_TGT PATH
EOF
```

---

## 5. À propos des SBU

Le **Standard Build Unit (SBU)** est une mesure du temps de compilation basé sur le temps nécessaire pour compiler Binutils.  
Cela permet d’estimer la durée des compilations suivantes.

---

## 6. À propos des suites de tests

Certaines étapes permettent d’exécuter des **tests automatiques** pour vérifier la validité des paquets compilés.  
Elles ne sont pas toujours obligatoires mais fortement recommandées.

---

Fin du Chapitre 4.
