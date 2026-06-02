---
title: Symfony – Ajouter un enregistrement
author: Gérard LE REST
date: 2026-06-02 15:30:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Doctrine, EntityManager]
---

# Cours 14 — Ajouter un enregistrement

## Introduction

Pour enregistrer un objet dans la base de données, Doctrine utilise l'EntityManager.

Deux méthodes sont essentielles :

```php
persist()
flush()
```

---

## Principe général

```php
$entityManager->persist($patient);
$entityManager->flush();
```

Résultat :

```text
Le patient est enregistré dans la base de données.
```

---

## Créer un objet

```php
$patient = new Patient();

$patient->setNom('Durand');
$patient->setPrenom('Paul');
```

À ce stade, l'objet existe uniquement en mémoire.

---

## Préparer l'enregistrement

```php
$entityManager->persist($patient);
```

Signifie :

```text
Doctrine prépare l'enregistrement de l'objet.
```

---

## Enregistrer dans la base

```php
$entityManager->flush();
```

Signifie :

```text
Doctrine exécute les requêtes SQL nécessaires.
```

---

## Exemple complet

```php
$patient = new Patient();

$patient->setNom('Durand');
$patient->setPrenom('Paul');

$entityManager->persist($patient);
$entityManager->flush();
```

---

## Utiliser dans un contrôleur

```php
#[Route('/patient/ajouter', name: 'patient_add')]
public function add(
    EntityManagerInterface $entityManager
): Response
{
    $patient = new Patient();

    $patient->setNom('Durand');
    $patient->setPrenom('Paul');

    $entityManager->persist($patient);
    $entityManager->flush();

    return new Response('Patient ajouté');
}
```

---

## Comprendre le processus

```text
Objet Patient
↓
persist()
↓
flush()
↓
Base de données
```

---

## Conclusion

Pour ajouter un enregistrement :

```php
$entityManager->persist($objet);
$entityManager->flush();
```

À retenir :

- `persist()` prépare l'enregistrement ;
- `flush()` exécute l'enregistrement ;
- les deux méthodes sont généralement utilisées ensemble.
