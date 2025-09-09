
# Linux From Scratch 12.4 - Chapitre 10 : Rendre le Système LFS Amorçable

Ce chapitre explique comment rendre le système Linux From Scratch **démarrable** en installant et configurant le chargeur d’amorçage ainsi que le noyau.

---

## Table des Matières

1. Introduction
2. Création du fichier /etc/fstab
3. Compilation et installation du noyau Linux
4. Installation et configuration de GRUB

---

## 1. Introduction

Après avoir installé le système de base et configuré les paramètres essentiels, il est temps de :  
- Compiler le **noyau Linux**, cœur du système.  
- Installer **GRUB**, le chargeur d’amorçage.  

Cela permettra à la machine de démarrer directement sur notre système LFS.

---

## 2. Création du fichier /etc/fstab

Le fichier **/etc/fstab** définit les partitions à monter au démarrage. Exemple :

```
# device        mount-point      type    options         dump    fsck
/dev/sda1       /                ext4    defaults        1       1
/dev/sda2       swap             swap    pri=1           0       0
proc            /proc            proc    nosuid,noexec   0       0
sysfs           /sys             sysfs   nosuid,noexec   0       0
devpts          /dev/pts         devpts  gid=5,mode=620  0       0
tmpfs           /run             tmpfs   defaults        0       0
```

On adapte les partitions selon son installation.

---

## 3. Compilation et installation du noyau Linux

### Extraction et préparation
```bash
tar -xf linux-6.16.1.tar.xz
cd linux-6.16.1
make mrproper
```

### Configuration du noyau  
On configure le noyau avec une interface semi-graphique :  
```bash
make menuconfig
```

Points importants :
- Activer le support pour le système de fichiers racine (ex: ext4).  
- Inclure les pilotes nécessaires pour le matériel utilisé.  
- Activer le support de l’init system (Systemd).  

### Compilation et installation  
```bash
make
make modules_install
cp -iv arch/x86/boot/bzImage /boot/vmlinuz-6.16.1-lfs-12.4
cp -iv System.map /boot/System.map-6.16.1
cp -iv .config /boot/config-6.16.1
```

---

## 4. Installation et configuration de GRUB

### Installation de GRUB  
```bash
grub-install /dev/sda
```

### Création de la configuration  
```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

Un fichier d’exemple pour **/boot/grub/grub.cfg** :

```
set default=0
set timeout=5

menuentry "Linux From Scratch 12.4" {
    set root=(hd0,1)
    linux /boot/vmlinuz-6.16.1-lfs-12.4 root=/dev/sda1 ro
}
```

GRUB est maintenant prêt à démarrer le système.

---

Fin du Chapitre 10.
