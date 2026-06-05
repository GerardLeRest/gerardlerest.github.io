---
title: Symfony – Cascade persist et remove
author: Gérard LE REST
date: 2026-06-02 18:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, doctrine, cascade]
---

# Cours 19 — Cascade persist et remove

## Introduction

Les options `cascade` permettent à Doctrine d'effectuer automatiquement certaines opérations sur les entités liées.

Les plus utilisées sont :

```php
persist
remove
```

---

## Cascade persist

Sans cascade :

```php
$patient->addSejour($sejour);

$entityManager->persist($patient);
$entityManager->persist($sejour);
$entityManager->flush();
```

---

## Avec cascade persist

```php
#[ORM\OneToMany(
    targetEntity: Sejour::class,
    mappedBy: 'patient',
    cascade: ['persist']
)]
private Collection $sejours;
```

Puis :

```php
$patient->addSejour($sejour);

$entityManager->persist($patient);
$entityManager->flush();
```

Doctrine enregistre automatiquement le séjour.

---

## Cascade remove

Sans cascade :

```php
$entityManager->remove($sejour);
$entityManager->remove($patient);
$entityManager->flush();
```

---

## Avec cascade remove

```php
#[ORM\OneToMany(
    targetEntity: Sejour::class,
    mappedBy: 'patient',
    cascade: ['remove']
)]
private Collection $sejours;
```

Puis :

```php
$entityManager->remove($patient);
$entityManager->flush();
```

Doctrine supprime automatiquement les séjours liés.

---

## Utiliser plusieurs cascades

```php
#[ORM\OneToMany(
    targetEntity: Sejour::class,
    mappedBy: 'patient',
    cascade: ['persist', 'remove']
)]
private Collection $sejours;
```

---

## Comprendre le fonctionnement

```text
Patient
↓
Séjours
```

Avec :

```text
cascade persist
```

l'enregistrement du patient entraîne l'enregistrement des séjours.

Avec :

```text
cascade remove
```

la suppression du patient entraîne la suppression des séjours.

---

## Attention

Une cascade remove peut supprimer un grand nombre d'enregistrements.

Il faut l'utiliser avec prudence.

---

## Conclusion

Les cascades automatisent certaines opérations Doctrine.

À retenir :

- `persist` : enregistrement automatique ;
- `remove` : suppression automatique ;
- plusieurs cascades peuvent être combinées ;
- attention aux suppressions en cascade.
