---
title: Symfony – Organisation d’un projet Symfony
author: Gérard LE REST
date: 2026-06-03 14:00:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Architecture, Organisation]
---

# Cours 40 — Organisation d’un projet Symfony

## Introduction

Symfony impose une organisation claire des fichiers et des dossiers.

Cette structure facilite la maintenance et la compréhension du projet.

---

## Dossier principal

```text
mon_projet/
```

Contient l'ensemble de l'application.

---

## Dossier src

```text
src/
```

Contient le code PHP de l'application.

---

## Contrôleurs

```text
src/Controller/
```

Exemple :

```text
PatientController.php
SejourController.php
```

---

## Entités

```text
src/Entity/
```

Exemple :

```text
Patient.php
Sejour.php
User.php
```

---

## Repositories

```text
src/Repository/
```

Exemple :

```text
PatientRepository.php
```

---

## Formulaires

```text
src/Form/
```

Exemple :

```text
PatientFormType.php
```

---

## Services

```text
src/Service/
```

Exemple :

```text
CalculAgeService.php
```

---

## Templates Twig

```text
templates/
```

Exemple :

```text
templates/patient/
templates/sejour/
```

---

## Fichiers publics

```text
public/
```

Contient :

```text
images
css
javascript
index.php
```

---

## Configuration

```text
config/
```

Contient :

```text
services.yaml
routes.yaml
packages/
```

---

## Migrations

```text
migrations/
```

Contient les fichiers de migration Doctrine.

---

## Comprendre le projet

```text
Route
↓
Contrôleur
↓
Entity
↓
Repository
↓
Twig
```

---

## Schéma simplifié

```text
src/
├── Controller
├── Entity
├── Repository
├── Form
└── Service

templates/

config/

public/
```

---

## Conclusion

Symfony organise automatiquement les fichiers selon leur rôle.

Dossiers à retenir :

```text
Controller
Entity
Repository
Form
Service
templates
config
public
```
