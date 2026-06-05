---
title: Symfony – Déploiement
author: Gérard LE REST
date: 2026-06-03 13:30:00 +0800
categories: [Symfony, Cours]
tags: [symfony, deploiement, production]
---

# Cours 39 — Déploiement

## Introduction

Le déploiement consiste à installer une application Symfony sur un serveur afin qu'elle soit accessible sur Internet.

---

## Préparer l'application

Vérifier que le projet fonctionne correctement en local.

---

## Installer les dépendances

```bash
composer install
```

Cette commande installe les bibliothèques nécessaires.

---

## Configurer l'environnement

Fichier :

```text
.env
```

En production :

```text
APP_ENV=prod
APP_DEBUG=0
```

---

## Créer la base de données

```bash
php bin/console doctrine:database:create
```

---

## Exécuter les migrations

```bash
php bin/console doctrine:migrations:migrate
```

---

## Vider le cache

```bash
php bin/console cache:clear
```

---

## Générer le cache de production

```bash
php bin/console cache:warmup
```

---

## Vérifier les droits

Les dossiers doivent être accessibles :

```text
var/
public/
```

---

## Serveur Web

Les plus utilisés sont :

```text
Apache
Nginx
```

Le point d'entrée est :

```text
public/index.php
```

---

## Comprendre le processus

```text
Projet Symfony
↓
Serveur
↓
Base de données
↓
Migrations
↓
Cache
↓
Site en ligne
```

---

## Vérifications finales

```text
Site accessible
Base de données opérationnelle
Connexion utilisateur
Formulaires fonctionnels
```

---

## Conclusion

Le déploiement permet de rendre une application accessible sur Internet.

Commandes à retenir :

```bash
composer install

php bin/console doctrine:migrations:migrate

php bin/console cache:clear

php bin/console cache:warmup
```
