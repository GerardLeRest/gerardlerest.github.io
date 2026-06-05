---
title: Symfony – Paramètres de configuration
author: Gérard LE REST
date: 2026-06-03 10:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, configuration, parametres]
---

# Cours 32 — Paramètres de configuration

## Introduction

Les paramètres de configuration permettent de stocker des valeurs utilisées par l'application.

Ils évitent d'écrire des valeurs directement dans le code.

---

## Fichier .env

Exemple :

```text
APP_ENV=dev
APP_SECRET=123456
```

Ces valeurs sont accessibles dans Symfony.

---

## Exemple de paramètre

```text
SITE_NAME=MonSite
```

---

## Récupérer un paramètre

```php
$siteName = $_ENV['SITE_NAME'];
```

---

## Paramètres Symfony

Fichier :

```text
config/services.yaml
```

Exemple :

```yaml
parameters:
    app.version: '1.0'
```

---

## Utiliser un paramètre

```php
$version = $this->getParameter(
    'app.version'
);
```

---

## Exemple

```php
return new Response(
    $this->getParameter('app.version')
);
```

---

## Pourquoi utiliser des paramètres ?

Permet de :

- centraliser les valeurs ;
- simplifier la maintenance ;
- éviter les valeurs en dur ;
- adapter facilement l'application.

---

## Exemples fréquents

```text
Version
Nom du site
Adresse email
Clé API
```

---

## Comprendre le processus

```text
Paramètre
↓
Configuration
↓
Application
↓
Utilisation
```

---

## Conclusion

Les paramètres permettent de centraliser la configuration.

À retenir :

```text
.env

services.yaml
```

Méthode :

```php
getParameter()
```
