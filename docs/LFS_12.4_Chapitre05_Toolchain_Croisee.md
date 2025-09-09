
# Linux From Scratch 12.4 - Chapitre 5 : Compilation d'une Chaîne d'Outils Croisée

Ce chapitre détaille la construction de la **toolchain croisée**, un ensemble minimal d'outils permettant de compiler le futur système LFS indépendamment du système hôte.

---

## Table des Matières

1. Introduction
2. Binutils - Passe 1
3. GCC - Passe 1
4. Linux API Headers
5. Glibc
6. Libstdc++ (GCC)

---

## 1. Introduction

La **toolchain croisée** est nécessaire pour construire LFS dans un environnement isolé.  
Elle comprend :  
- Un **assembleur** et un **linker** (Binutils).  
- Un **compilateur C/C++** (GCC).  
- La **bibliothèque C** (Glibc).  
- Les **en-têtes du noyau** pour la compatibilité système.

Cette étape est essentielle pour éviter toute dépendance avec le système hôte.

---

## 2. Binutils - Passe 1

**Rôle :**  
- `as` : Assembleur, transforme le code source en code machine.  
- `ld` : Linker, assemble les fichiers objets en exécutables.

**Commandes principales :**
```bash
tar -xf binutils-2.45.tar.xz
cd binutils-2.45
mkdir -v build && cd build
../configure --prefix=$LFS/tools --with-sysroot=$LFS --target=$LFS_TGT --disable-nls --disable-werror
make
make install
```

---

## 3. GCC - Passe 1

**Rôle :**  
- Compilateur C et C++, essentiel pour construire tous les logiciels suivants.  

**Commandes principales :**
```bash
tar -xf gcc-15.2.0.tar.xz
cd gcc-15.2.0
./contrib/download_prerequisites
mkdir -v build && cd build
../configure --target=$LFS_TGT --prefix=$LFS/tools --with-glibc-version=2.42 --with-sysroot=$LFS --disable-nls --disable-multilib --disable-decimal-float --disable-threads --disable-libatomic --disable-libgomp --disable-libquadmath --disable-libssp --disable-libvtv --disable-libstdcxx --enable-languages=c,c++
make
make install
```

---

## 4. Linux API Headers

**Rôle :** Fournir les en-têtes du noyau pour que Glibc puisse interagir avec le noyau Linux.  

**Commandes principales :**
```bash
tar -xf linux-6.16.1.tar.xz
cd linux-6.16.1
make mrproper
make headers
find usr/include -name '.*' -delete
cp -rv usr/include $LFS/usr
```

---

## 5. Glibc

**Rôle :** La bibliothèque standard C, cœur de tout système Linux.  
Elle fournit les appels systèmes et fonctions de base utilisées par presque tous les programmes.

**Commandes principales :**
```bash
tar -xf glibc-2.42.tar.xz
cd glibc-2.42
mkdir -v build && cd build
../configure --prefix=/usr --host=$LFS_TGT --build=$(../scripts/config.guess) --enable-kernel=4.19 --with-headers=$LFS/usr/include --disable-nls
make
make install
```

---

## 6. Libstdc++ (GCC)

**Rôle :** Bibliothèque standard C++ utilisée par de nombreux programmes modernes.

**Commandes principales :**
```bash
cd gcc-15.2.0/build
make -C libstdc++-v3
make -C libstdc++-v3 install
```

---

Fin du Chapitre 5.
