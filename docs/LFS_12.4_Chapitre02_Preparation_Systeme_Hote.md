
# Linux From Scratch 12.4 - Chapitre 2 : Préparation du Système Hôte

Ce chapitre explique comment préparer correctement le système hôte avant de commencer la construction de Linux From Scratch.

---

## Table des Matières

1. Introduction
2. Prérequis du système hôte
3. Les étapes de la construction de LFS
4. Création d'une nouvelle partition
5. Création d'un système de fichiers sur la partition
6. Définition de la variable $LFS et du Umask
7. Montage de la nouvelle partition

---

## 1. Introduction

Avant de construire Linux From Scratch, il est essentiel de préparer correctement le **système hôte** qui servira à compiler tous les composants du futur système.

L'objectif est de créer un environnement propre et isolé pour éviter toute interférence avec le système déjà en place.

---

## 2. Prérequis du système hôte

Le système hôte doit disposer :
- D’un compilateur C valide (GCC).  
- D’outils de construction comme `make`, `binutils`, `tar`, `xz`, etc.  
- D’un noyau Linux moderne (4.19 ou supérieur).  

Commandes pour vérifier les versions :
```bash
bash --version
gcc --version
ld --version
```

---

## 3. Les étapes de la construction de LFS

Résumé des étapes à venir :
1. Préparer l’environnement.  
2. Construire les outils temporaires.  
3. Compiler le système de base.  
4. Configurer et démarrer sur le nouveau système.  

---

## 4. Création d'une nouvelle partition

On crée une **partition dédiée** pour LFS afin d’isoler complètement le système :

```bash
fdisk /dev/sdX
```

- `/dev/sdX` : disque cible.  
- Taille recommandée : au moins **20 Go**.

---

## 5. Création d'un système de fichiers sur la partition

On formate la partition pour qu’elle soit utilisable par Linux :  
```bash
mkfs.ext4 /dev/sdXn
```

- `ext4` est le système de fichiers recommandé pour LFS.

---

## 6. Définition de la variable $LFS et du Umask

La variable `$LFS` désigne le point de montage principal du futur système :  
```bash
export LFS=/mnt/lfs
```

Le `umask` définit les permissions par défaut des fichiers nouvellement créés :  
```bash
umask 022
```

---

## 7. Montage de la nouvelle partition

On monte la partition à l’emplacement choisi :  
```bash
mkdir -pv $LFS
mount /dev/sdXn $LFS
```

On crée aussi le dossier pour les sources et outils :
```bash
mkdir -v $LFS/sources
chmod -v a+wt $LFS/sources
mkdir -pv $LFS/tools
ln -sv $LFS/tools /
```

---

Fin du Chapitre 2.
