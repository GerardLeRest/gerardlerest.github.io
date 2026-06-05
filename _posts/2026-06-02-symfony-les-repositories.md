---
title: Symfony – Les repositories
author: Gérard LE REST
date: 2026-06-02 14:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, doctrine, repository]
---

# Cours 11 — Les repositories

## Introduction

Un repository permet de rechercher des données dans la base de données.

Chaque entité possède généralement son propre repository.

Exemple :

```text
Patient
↓
PatientRepository
```

---

## Création automatique

Lors de la création d'une entité :

```bash
php bin/console make:entity
```

Symfony crée automatiquement un repository.

Exemple :

```text
src/Repository/PatientRepository.php
```

---

## Utiliser un repository

Dans un contrôleur :

```php
public function show(PatientRepository $patientRepository): Response
{
}
```

Symfony fournit automatiquement le repository.

---

## Rechercher par identifiant

```php
$patient = $patientRepository->find(12);
```

Résultat :

```text
Recherche du patient dont l'identifiant vaut 12.
```

---

## Rechercher plusieurs enregistrements

```php
$patients = $patientRepository->findAll();
```

Résultat :

```text
Retourne tous les patients.
```

---

## Rechercher avec une condition

```php
$patients = $patientRepository->findBy([
    'nom' => 'Durand'
]);
```

Résultat :

```text
Retourne tous les patients dont le nom est Durand.
```

---

## Rechercher un seul enregistrement

```php
$patient = $patientRepository->findOneBy([
    'nom' => 'Durand'
]);
```

Résultat :

```text
Retourne le premier patient trouvé.
```

---

## Conclusion

Le repository permet de rechercher des données dans la base.

Méthodes à retenir :

```php
find()
findAll()
findBy()
findOneBy()
```

Schéma mental :

```text
Entité
↓
Repository
↓
Base de données
```
