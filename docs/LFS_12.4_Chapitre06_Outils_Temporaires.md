
# Linux From Scratch 12.4 - Chapitre 6 : Compilation Croisée des Outils Temporaires

Ce chapitre couvre la construction des outils temporaires qui serviront plus tard à construire le système final dans un environnement chrooté.

---

## Table des Matières

1. Introduction
2. M4
3. Ncurses
4. Bash
5. Coreutils
6. Diffutils
7. File
8. Findutils
9. Gawk
10. Grep
11. Gzip
12. Make
13. Patch
14. Sed
15. Tar
16. Xz
17. Binutils - Passe 2
18. GCC - Passe 2

---

## 1. Introduction

Les outils temporaires construits ici sont utilisés uniquement dans le processus de construction et ne font pas partie du système final.

But :
- Créer un environnement autonome dans **$LFS/tools**.
- Éviter les dépendances avec le système hôte.

---

## 2. M4

**Rôle :** Préprocesseur de macros utilisé par Autoconf.  
```bash
tar -xf m4-1.4.20.tar.xz
cd m4-1.4.20
./configure --prefix=/usr
make
make install
```

---

## 3. Ncurses

**Rôle :** Fournit des bibliothèques pour gérer les interfaces texte.  
```bash
tar -xf ncurses-6.5-20250809.tar.gz
cd ncurses-6.5-20250809
./configure --prefix=/usr --with-shared --without-debug
make
make install
```

---

## 4. Bash

**Rôle :** Shell principal pour exécuter tous les scripts.  
```bash
tar -xf bash-5.3.tar.gz
cd bash-5.3
./configure --prefix=/usr --without-bash-malloc
make
make install
```

---

## 5. Coreutils

**Rôle :** Commandes Unix de base (`ls`, `cp`, `mv`, `rm`, etc.).  
```bash
tar -xf coreutils-9.7.tar.xz
cd coreutils-9.7
./configure --prefix=/usr --enable-install-program=hostname
make
make install
```

---

## 6. Diffutils

**Rôle :** Comparaison de fichiers et génération de patchs.  
```bash
tar -xf diffutils-3.12.tar.xz
cd diffutils-3.12
./configure --prefix=/usr
make
make install
```

---

## 7. File

**Rôle :** Détection du type de fichiers.  
```bash
tar -xf file-5.46.tar.gz
cd file-5.46
./configure --prefix=/usr
make
make install
```

---

## 8. Findutils

**Rôle :** Recherche et manipulation des fichiers.  
```bash
tar -xf findutils-4.10.0.tar.xz
cd findutils-4.10.0
./configure --prefix=/usr
make
make install
```

---

## 9. Gawk

**Rôle :** Traitement avancé du texte avec le langage AWK.  
```bash
tar -xf gawk-5.3.2.tar.xz
cd gawk-5.3.2
./configure --prefix=/usr
make
make install
```

---

## 10. Grep

**Rôle :** Recherche de chaînes de texte dans des fichiers.  
```bash
tar -xf grep-3.12.tar.xz
cd grep-3.12
./configure --prefix=/usr
make
make install
```

---

## 11. Gzip

**Rôle :** Compression et décompression de fichiers.  
```bash
tar -xf gzip-1.14.tar.xz
cd gzip-1.14
./configure --prefix=/usr
make
make install
```

---

## 12. Make

**Rôle :** Automatisation des compilations avec Makefiles.  
```bash
tar -xf make-4.4.1.tar.gz
cd make-4.4.1
./configure --prefix=/usr
make
make install
```

---

## 13. Patch

**Rôle :** Application de correctifs aux fichiers source.  
```bash
tar -xf patch-2.8.tar.gz
cd patch-2.8
./configure --prefix=/usr
make
make install
```

---

## 14. Sed

**Rôle :** Éditeur de texte en ligne de commande pour modifications automatiques.  
```bash
tar -xf sed-4.9.tar.xz
cd sed-4.9
./configure --prefix=/usr
make
make install
```

---

## 15. Tar

**Rôle :** Création et extraction d’archives.  
```bash
tar -xf tar-1.35.tar.xz
cd tar-1.35
./configure --prefix=/usr
make
make install
```

---

## 16. Xz

**Rôle :** Compression avec algorithme LZMA haute performance.  
```bash
tar -xf xz-5.8.1.tar.xz
cd xz-5.8.1
./configure --prefix=/usr
make
make install
```

---

## 17. Binutils - Passe 2

**Rôle :** Version finale de Binutils pour le futur système.  
```bash
tar -xf binutils-2.45.tar.xz
cd binutils-2.45
mkdir -v build && cd build
../configure --prefix=/usr --disable-nls --enable-gold --enable-ld=default --enable-plugins --enable-shared --with-system-zlib
make
make install
```

---

## 18. GCC - Passe 2

**Rôle :** Version finale du compilateur GCC pour le système complet.  
```bash
tar -xf gcc-15.2.0.tar.xz
cd gcc-15.2.0
mkdir -v build && cd build
../configure --prefix=/usr --disable-multilib --disable-bootstrap --enable-languages=c,c++
make
make install
```

---

Fin du Chapitre 6.
