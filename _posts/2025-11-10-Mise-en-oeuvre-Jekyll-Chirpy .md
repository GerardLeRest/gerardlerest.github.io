---
title: Mise en oeuvre de Jekyll-Chirpy
author: Gérard LE REST
date: 2025-11-20 17:34:00 +0800
categories: [Jekyll-theme-chirpy, Tutorial]
tags: [favicon]
---

## Les dossiers et les fichiers importants

Une fois installé, on peut utiliser les dossiers pour y déposer des page de blog, tutoriels. Voici les principaux fichiers/dossiers:

## Download & Replace

Download the generated package, unzip and delete the following file(s) from the extracted files:

* config.yml: fichier de configuration
* .git: ficxhier githu pour la synchronisation
* _tabs: contient toutes les pages webs
* _post: contient les pages de blog (billets
* /assets/img/favicons : favicons du site
* /assets/img

## Site en local

ouvrir un terminal à la racine de dossier du site.

```bash
bundle exec jekyll clean
```

puis:

```bash
bundle exec jekyll server
```

sur le naviateur: 
[http://localhost:4000](http://localhost:4000)
