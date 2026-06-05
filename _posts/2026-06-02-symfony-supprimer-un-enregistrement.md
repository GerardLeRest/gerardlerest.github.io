---
title: Symfony – Supprimer un enregistrement
author: Gérard LE REST
date: 2026-06-02 16:15:00 +0800
categories: [Symfony, Cours]
tags: [symfony, doctrine, entitymanager]
---

# Cours 16 — Supprimer un enregistrement

## Introduction

Pour supprimer un enregistrement, il faut :

1. rechercher l'objet ;
2. demander sa suppression ;
3. enregistrer la modification dans la base.

---

## Principe général

```php
$patient = $patientRepository->find($id);

$entityManager->remove($patient);
$entityManager->flush();
```

Résultat :

```text
Le patient est supprimé de la base de données.
```

---

## Rechercher l'objet

```php
$patient = $patientRepository->find($id);
```

Doctrine récupère l'objet à supprimer.

---

## Vérifier que l'objet existe

```php
if (!$patient) {
    throw $this->createNotFoundException();
}
```

Si l'objet n'existe pas, Symfony affiche une erreur 404.

---

## Demander la suppression

```php
$entityManager->remove($patient);
```

Signifie :

```text
Doctrine prépare la suppression de l'objet.
```

---

## Exécuter la suppression

```php
$entityManager->flush();
```

Signifie :

```text
Doctrine exécute la requête SQL de suppression.
```

---

## Exemple complet

```php
$patient = $patientRepository->find($id);

if (!$patient) {
    throw $this->createNotFoundException();
}

$entityManager->remove($patient);
$entityManager->flush();
```

---

## Utiliser dans un contrôleur

```php
#[Route('/patient/supprimer/{id}', name: 'patient_delete')]
public function delete(
    int $id,
    PatientRepository $patientRepository,
    EntityManagerInterface $entityManager
): Response
{
    $patient = $patientRepository->find($id);

    if (!$patient) {
        throw $this->createNotFoundException();
    }

    $entityManager->remove($patient);
    $entityManager->flush();

    return new Response('Patient supprimé');
}
```

---

## Comprendre le processus

```text
find()
↓
remove()
↓
flush()
↓
Base de données
```

---

## Conclusion

Pour supprimer un enregistrement :

```php
$entityManager->remove($objet);
$entityManager->flush();
```

À retenir :

- rechercher l'objet ;
- vérifier qu'il existe ;
- utiliser `remove()` ;
- utiliser `flush()` pour appliquer la suppression.
