
# Linux From Scratch 12.4 - Chapitre 7 : Entrée dans le chroot et Outils Temporaires Supplémentaires

Ce chapitre explique comment entrer dans l'environnement **chroot** pour isoler complètement le futur système et y construire des outils supplémentaires nécessaires avant la construction du système final.

---

## Table des Matières

1. Introduction
2. Changement du propriétaire
3. Préparer les systèmes de fichiers virtuels du noyau
4. Entrer dans l'environnement chroot
5. Création des répertoires
6. Création des fichiers et des liens symboliques essentiels
7. Installation des outils supplémentaires :
   - Gettext
   - Bison
   - Perl
   - Python
   - Texinfo
   - Util-linux
8. Nettoyage et Sauvegarde du système temporaire

---

## 1. Introduction

L'étape **chroot** (change root) permet de basculer dans le futur système comme si c'était le système principal.  
Ainsi, toute action faite à partir de maintenant affectera uniquement le nouveau système LFS.

---

## 2. Changement du propriétaire

On s'assure que tout appartient à l'utilisateur **root** avant de chrooter :  
```bash
chown -R root:root $LFS/{usr,lib,var,etc,bin,sbin,tools}
```

---

## 3. Préparer les systèmes de fichiers virtuels du noyau

On monte les systèmes nécessaires :  
```bash
mount -v --bind /dev $LFS/dev
mount -vt devpts devpts $LFS/dev/pts -o gid=5,mode=620
mount -vt proc proc $LFS/proc
mount -vt sysfs sysfs $LFS/sys
mount -vt tmpfs tmpfs $LFS/run
```

---

## 4. Entrer dans l'environnement chroot

On entre dans le futur système avec :  
```bash
chroot "$LFS" /usr/bin/env -i \
    HOME=/root TERM="$TERM" PS1='(lfs chroot) \u:\w\$ ' \
    PATH=/usr/bin:/usr/sbin /bin/bash --login
```

---

## 5. Création des répertoires

On crée l'arborescence standard de Linux :  
```bash
mkdir -pv /{boot,home,mnt,opt,srv}
mkdir -pv /etc/{opt,sysconfig}
mkdir -pv /lib/firmware
mkdir -pv /media/{floppy,cdrom}
```

---

## 6. Création des fichiers et des liens symboliques essentiels

On ajoute les fichiers critiques :  
```bash
ln -sv /proc/self/mounts /etc/mtab
touch /etc/passwd /etc/group
```

---

## 7. Installation des outils supplémentaires

### Gettext

**Rôle :** internationalisation des messages système.  
```bash
tar -xf gettext-0.26.tar.xz
cd gettext-0.26
./configure --prefix=/usr
make
make install
```

### Bison

**Rôle :** générateur d'analyseurs syntaxiques.  
```bash
tar -xf bison-3.8.2.tar.xz
cd bison-3.8.2
./configure --prefix=/usr
make
make install
```

### Perl

**Rôle :** langage de script polyvalent, utilisé par de nombreux outils.  
```bash
tar -xf perl-5.42.0.tar.xz
cd perl-5.42.0
./Configure -des -Dprefix=/usr
make
make install
```

### Python

**Rôle :** langage de script moderne utilisé par beaucoup d'applications.  
```bash
tar -xf Python-3.13.7.tar.xz
cd Python-3.13.7
./configure --prefix=/usr --enable-shared
make
make install
```

### Texinfo

**Rôle :** génération de documentation en format info.  
```bash
tar -xf texinfo-7.2.tar.xz
cd texinfo-7.2
./configure --prefix=/usr
make
make install
```

### Util-linux

**Rôle :** outils essentiels pour la gestion du système (mount, fdisk...).  
```bash
tar -xf util-linux-2.41.1.tar.xz
cd util-linux-2.41.1
./configure --prefix=/usr --without-systemd
make
make install
```

---

## 8. Nettoyage et Sauvegarde du système temporaire

Après ces installations, il est conseillé de faire une **sauvegarde** du système temporaire pour éviter de tout recommencer en cas de problème.

---

Fin du Chapitre 7.
