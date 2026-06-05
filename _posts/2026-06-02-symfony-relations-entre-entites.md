---
title: Symfony – Les relations entre entités
author: Gérard LE REST
date: 2026-06-02 16:30:00 +0800
categories: [Symfony, Cours]
tags: [symfony, doctrine, relation]
---

# Cours 17 — Les relations entre entités

## Introduction

Une relation permet de relier deux entités.

Exemple :

```text
Patient
↓
Séjour
```

Un patient peut posséder plusieurs séjours.

---

## Créer une relation

Commande :

```bash
php bin/console make:entity
```

Puis :

```text
New property name:
```

Exemple :

```text
patient
```

Type :

```text
relation
```

---

## Exemple ManyToOne

Un séjour appartient à un seul patient.

```php
#[ORM\ManyToOne]
private ?Patient $patient = null;
```

---

## Exemple OneToMany

Un patient possède plusieurs séjours.

```php
#[ORM\OneToMany(
    targetEntity: Sejour::class,
    mappedBy: 'patient'
)]
private Collection $sejours;
```

---

## Utiliser la relation

```php
$sejour->setPatient($patient);
```

---

## Lire la relation

```php
$patient = $sejour->getPatient();
```

---

## Accéder à plusieurs objets

```php
$sejours = $patient->getSejours();
```

Résultat :

```text
Collection de séjours du patient.
```

---

## Comprendre le schéma

```text
Patient
    ↓
  Séjour 1

Patient
    ↓
  Séjour 2

Patient
    ↓
  Séjour 3
```

---

## Conclusion

Les relations permettent de relier plusieurs entités.

À retenir :

- `ManyToOne` : plusieurs objets vers un seul ;
- `OneToMany` : un objet vers plusieurs ;
- Doctrine génère automatiquement le code nécessaire ;
- les relations facilitent la navigation entre les objets.
