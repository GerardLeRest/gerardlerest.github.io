---
title: Symfony – Modifier un enregistrement
author: Gérard LE REST
date: 2026-06-02 16:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, doctrine, entitymanager]
---

# Cours 15 — Modifier un enregistrement

## Introduction

Pour modifier un enregistrement, il faut :

1. rechercher l'objet ;
2. modifier ses propriétés ;
3. enregistrer les changements.

---

## Principe général

```php
$patient = $patientRepository->find($id);

$patient->setNom('Martin');

$entityManager->flush();
```

Résultat :

```text
Le nom du patient est modifié dans la base de données.
```

---

## Rechercher l'objet

```php
$patient = $patientRepository->find($id);
```

Doctrine récupère l'objet depuis la base.

---

## Modifier une propriété

```php
$patient->setNom('Martin');
```

L'objet est modifié en mémoire.

---

## Enregistrer les modifications

```php
$entityManager->flush();
```

Doctrine met à jour la base de données.

---

## Exemple complet

```php
$patient = $patientRepository->find($id);

if (!$patient) {
    throw $this->createNotFoundException();
}

$patient->setNom('Martin');

$entityManager->flush();
```

---

## Utiliser dans un contrôleur

```php
#[Route('/patient/modifier/{id}', name: 'patient_edit')]
public function edit(
    int $id,
    PatientRepository $patientRepository,
    EntityManagerInterface $entityManager
): Response
{
    $patient = $patientRepository->find($id);

    if (!$patient) {
        throw $this->createNotFoundException();
    }

    $patient->setNom('Martin');

    $entityManager->flush();

    return new Response('Patient modifié');
}
```

---

## Pourquoi pas persist() ?

L'objet existe déjà dans la base.

Doctrine le surveille automatiquement.

Il suffit donc d'utiliser :

```php
$entityManager->flush();
```

---

## Comprendre le processus

```text
find()
↓
Modification
↓
flush()
↓
Base de données
```

---

## Conclusion

Pour modifier un enregistrement :

```php
$objet = $repository->find($id);

$objet->setPropriete(...);

$entityManager->flush();
```

À retenir :

- rechercher l'objet ;
- modifier ses propriétés ;
- utiliser `flush()` ;
- `persist()` n'est généralement pas nécessaire.
