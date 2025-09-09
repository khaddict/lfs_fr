
# Linux From Scratch 12.4 - Chapitre 8 : Installation des Logiciels du Système de Base

Ce chapitre installe tous les composants nécessaires pour obtenir un **système Linux fonctionnel**.  
Chaque package est expliqué avec son **rôle** dans le système.

---

## Table des Matières

1. Introduction  
2. Gestion des paquets  
3. Tableau des packages avec explications  
4. Nettoyage des fichiers temporaires  
5. Préparation à la configuration finale  

---

## 1. Introduction

Après avoir préparé l'environnement chroot, nous installons les **logiciels du système de base** :  
- Bibliothèques essentielles  
- Outils systèmes  
- Utilitaires pour le développement et l'administration  

---

## 2. Gestion des paquets

Les paquets sont installés **manuellement** avec :  
- `configure` pour personnaliser l'installation  
- `make` pour compiler  
- `make install` pour installer  

---

## 3. Tableau des packages avec explications

| Package | Rôle / Fonction principale |
|---------|-----------------------------|
| Man-pages-6.15 | Pages de manuel pour la documentation système. |
| Iana-Etc-20250807 | Fichiers de configuration pour les protocoles réseau et services. |
| Glibc-2.42 | Bibliothèque C standard, cœur du système Linux. |
| Zlib-1.3.1 | Bibliothèque de compression utilisée par de nombreux programmes. |
| Bzip2-1.0.8 | Compression/décompression de fichiers `.bz2`. |
| Xz-5.8.1 | Compression haute performance pour `.xz`. |
| Lz4-1.10.0 | Compression ultra-rapide avec LZ4. |
| Zstd-1.5.7 | Compression moderne rapide avec Zstandard. |
| File-5.46 | Détection du type des fichiers. |
| Readline-8.3 | Historique et édition des commandes dans Bash. |
| M4-1.4.20 | Préprocesseur de macros pour scripts de configuration. |
| Bc-7.0.3 | Calculatrice en ligne de commande avec précision arbitraire. |
| Flex-2.6.4 | Générateur d’analyseurs lexicaux. |
| Tcl-8.6.16 | Langage de script utilisé par Expect et d'autres outils. |
| Expect-5.45.4 | Automatisation d’interactions avec des programmes interactifs. |
| DejaGNU-1.6.3 | Framework de tests pour outils comme GCC. |
| Pkgconf-2.5.1 | Gestion des dépendances pour les bibliothèques. |
| Binutils-2.45 | Assembleur et Linker pour la construction d’exécutables. |
| GMP-6.3.0 | Calcul arithmétique haute précision. |
| MPFR-4.2.2 | Précision flottante pour calculs avancés. |
| MPC-1.3.1 | Calculs arithmétiques complexes. |
| Attr-2.5.2 | Gestion des attributs étendus sur les fichiers. |
| Acl-2.3.2 | Contrôle d’accès avancé pour fichiers. |
| Libcap-2.76 | Gestion des capacités POSIX pour la sécurité. |
| Libxcrypt-4.4.38 | Fonctions cryptographiques pour les mots de passe. |
| Shadow-4.18.0 | Gestion des utilisateurs et mots de passe. |
| GCC-15.2.0 | Compilateur C/C++ essentiel pour tout Linux. |
| Ncurses-6.5-20250809 | Interfaces texte pour le terminal. |
| Sed-4.9 | Éditeur de flux pour traitement de texte automatique. |
| Psmisc-23.7 | Outils pour gérer les processus (`killall`, `fuser`, etc.). |
| Gettext-0.26 | Internationalisation (traduction des messages). |
| Bison-3.8.2 | Générateur d’analyseurs syntaxiques. |
| Grep-3.12 | Recherche de texte dans les fichiers. |
| Bash-5.3 | Shell principal de Linux. |
| Libtool-2.5.4 | Gestion des bibliothèques partagées. |
| GDBM-1.26 | Base de données simple en fichiers plats. |
| Gperf-3.3 | Génération de tables de hachage parfaites. |
| Expat-2.7.1 | Bibliothèque pour le traitement XML. |
| Inetutils-2.6 | Outils réseau de base (ping, telnet...). |
| Less-679 | Visualisation de fichiers texte en console. |
| Perl-5.42.0 | Langage de script polyvalent. |
| XML::Parser-2.47 | Analyseur XML pour Perl. |
| Intltool-0.51.0 | Outils pour l’internationalisation. |
| Autoconf-2.72 | Génération automatique de scripts de configuration. |
| Automake-1.18.1 | Génération automatique de Makefiles. |
| OpenSSL-3.5.2 | Chiffrement et SSL/TLS. |
| Libelf-3.12 | Gestion des fichiers ELF (binaires Linux). |
| Libffi-3.5.2 | Appels dynamiques à des fonctions C. |
| Python-3.13.7 | Langage de script moderne. |
| Flit-Core-3.12.0 | Gestion de paquets Python. |
| Packaging-25.0 | Outils pour la distribution Python. |
| Wheel-0.46.1 | Format standard pour paquets Python. |
| Setuptools-80.9.0 | Installation de paquets Python. |
| Ninja-1.13.1 | Système de build rapide. |
| Meson-1.8.3 | Système de build moderne. |
| Kmod-34.2 | Gestion des modules du noyau. |
| Coreutils-9.7 | Commandes Unix de base (`ls`, `cp`, `mv`, etc.). |
| Diffutils-3.12 | Comparaison de fichiers et création de patchs. |
| Gawk-5.3.2 | Traitement de texte avec AWK. |
| Findutils-4.10.0 | Recherche de fichiers dans l’arborescence. |
| Groff-1.23.0 | Génération de documents texte. |
| GRUB-2.12 | Chargeur d’amorçage pour Linux. |
| Gzip-1.14 | Compression/décompression `.gz`. |
| IPRoute2-6.16.0 | Configuration réseau avancée. |
| Kbd-2.8.0 | Gestion des claviers et consoles. |
| Libpipeline-1.5.8 | Gestion des pipelines de processus. |
| Make-4.4.1 | Automatisation des compilations. |
| Patch-2.8 | Application de correctifs aux fichiers source. |
| Tar-1.35 | Archivage et compression de fichiers. |
| Texinfo-7.2 | Documentation au format info. |
| Vim-9.1.1629 | Éditeur de texte avancé pour Linux. |
| MarkupSafe-3.0.2 | Sécurité pour modèles HTML. |
| Jinja2-3.1.6 | Moteur de templates Python. |
| Systemd-257.8 | Système d’initialisation et gestion des services. |
| D-Bus-1.16.2 | Communication inter-processus. |
| Man-DB-2.13.1 | Système de pages de manuel. |
| Procps-ng-4.0.5 | Surveillance des processus et ressources. |
| Util-linux-2.41.1 | Outils système divers (fdisk, mount...). |
| E2fsprogs-1.47.3 | Gestion des systèmes de fichiers ext2/3/4. |

---

## 4. Nettoyage des fichiers temporaires

Après installation, on supprime les sources pour économiser de l’espace :  
```bash
rm -rf /sources/*
```

---

## 5. Préparation à la configuration finale

Une fois tous les paquets installés, on passe à la **configuration du système** :  
- Réseau  
- Locales  
- Noyau  
- Bootloader (GRUB)

---

Fin du Chapitre 8 détaillé.
