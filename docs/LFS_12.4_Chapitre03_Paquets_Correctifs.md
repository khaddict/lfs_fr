
# Linux From Scratch 12.4 - Chapitre 3 : Paquets et Correctifs

Ce chapitre explique quels paquets sont nécessaires pour construire LFS et comment les organiser avant la compilation.

---

## Table des Matières

1. Introduction
2. Tous les paquets nécessaires
3. Correctifs requis

---

## 1. Introduction

Avant de commencer la construction du système, il est essentiel de télécharger tous les **paquets sources** et **correctifs** nécessaires.  
Ces fichiers doivent être stockés dans le répertoire **$LFS/sources** pour faciliter la compilation.

---

## 2. Tous les paquets nécessaires

Les paquets contiennent :
- **Compilateurs** : GCC, Binutils…
- **Bibliothèques** : Glibc, Zlib…
- **Outils système** : Coreutils, Bash, Sed, etc.
- **Utilitaires réseau** : Inetutils, IPRoute2…

Exemple pour télécharger un paquet :
```bash
wget https://ftp.gnu.org/gnu/binutils/binutils-2.45.tar.xz -P $LFS/sources
```

Chaque version est choisie pour sa **stabilité** et sa **compatibilité** avec les autres paquets.

---

## 3. Correctifs requis

Certains paquets nécessitent des **patchs** pour :  
- Corriger des bugs connus.  
- Améliorer la compatibilité avec les nouvelles versions du noyau.  
- Éviter des failles de sécurité.  

Exemple pour appliquer un patch :
```bash
patch -Np1 -i ../nom-du-correctif.patch
```

Les correctifs sont généralement fournis sur le site officiel de LFS :  
[https://www.linuxfromscratch.org/lfs/patches](https://www.linuxfromscratch.org/lfs/patches)

---

Fin du Chapitre 3.
