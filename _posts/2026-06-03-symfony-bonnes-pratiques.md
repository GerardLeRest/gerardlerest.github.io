---
title: Symfony – Bonnes pratiques
author: Gérard LE REST
date: 2026-06-03 14:30:00 +0800
categories: [Symfony, Cours]
tags: [symfony, bonnes_pratiques, qualite]
---

# Cours 41 — Bonnes pratiques

## Introduction

Symfony facilite le développement, mais certaines habitudes permettent d'obtenir un code plus clair et plus facile à maintenir.

---

## Un contrôleur léger

Éviter :

```php
class PatientController
{
    // 500 lignes de code
}
```

Préférer :

```text
Contrôleur
↓
Service
↓
Traitement
```

---

## Utiliser les services

Déplacer la logique métier dans :

```text
src/Service/
```

---

## Une classe = une responsabilité

Exemple :

```text
PatientController
```

gère les patients.

```text
SejourController
```

gère les séjours.

---

## Utiliser les repositories

Éviter :

```php
SELECT * FROM patient
```

dans les contrôleurs.

Préférer :

```php
$patientRepository->find($id);
```

---

## Utiliser les formulaires

Éviter :

```php
$_POST
```

Préférer :

```php
FormType
```

et :

```php
handleRequest()
```

---

## Sécuriser les accès

Utiliser :

```php
#[IsGranted('ROLE_USER')]
```

pour protéger les pages.

---

## Nommer clairement

Exemple :

```php
$patient
```

plutôt que :

```php
$p
```

---

## Éviter les doublons

Si du code est utilisé plusieurs fois :

```text
Créer un service.
```

---

## Utiliser Doctrine

Préférer :

```php
persist()

flush()
```

aux requêtes SQL écrites à la main.

---

## Relire régulièrement le projet

Permet :

- d'améliorer le code ;
- de simplifier certaines parties ;
- de détecter les incohérences.

---

## Comprendre le processus

```text
Code simple
↓
Code lisible
↓
Maintenance facile
```

---

## Conclusion

Les bonnes pratiques rendent les projets plus robustes.

À retenir :

- contrôleurs légers ;
- services réutilisables ;
- noms explicites ;
- sécurité ;
- limitation des doublons ;
- relecture régulière du code.
