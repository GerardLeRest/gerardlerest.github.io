---
title: Symfony – Rechercher un enregistrement
author: Gérard LE REST
date: 2026-06-02 14:30:00 +0800
categories: [Symfony, Cours]
tags: [symfony, doctrine, repository]
---

# Cours 12 — Rechercher un enregistrement

## Introduction

La méthode `find()` permet de rechercher un enregistrement à partir de son identifiant.

Elle est fournie par le repository de l'entité.

---

## Principe général

```php
$patient = $patientRepository->find(12);
```

Résultat :

```text
Recherche le patient dont l'identifiant vaut 12.
```

---

## Utiliser find() dans un contrôleur

```php
#[Route('/patient/{id}', name: 'patient_show')]
public function show(
    int $id,
    PatientRepository $patientRepository
): Response
{
    $patient = $patientRepository->find($id);

    return $this->render('patient/show.html.twig', [
        'patient' => $patient
    ]);
}
```

---

## Comprendre le code

```php
$patientRepository->find($id);
```

Signifie :

```text
Chercher l'enregistrement dont l'identifiant vaut $id.
```

---

## Résultat trouvé

Si l'identifiant existe :

```php
$patient = $patientRepository->find(12);
```

alors :

```php
$patient
```

contient un objet Patient.

---

## Résultat non trouvé

Si l'identifiant n'existe pas :

```php
$patient = $patientRepository->find(999);
```

alors :

```php
$patient === null
```

---

## Vérifier le résultat

```php
$patient = $patientRepository->find($id);

if (!$patient) {
    throw $this->createNotFoundException();
}
```

---

## Affichage dans Twig

Contrôleur :

```php
return $this->render('patient/show.html.twig', [
    'patient' => $patient
]);
```

Vue Twig :

```twig
{{ patient.nom }}
```

---

## Conclusion

Pour rechercher un enregistrement :

```php
$patient = $patientRepository->find($id);
```

À retenir :

- `find()` recherche par identifiant ;
- la méthode retourne un objet ;
- si aucun enregistrement n'est trouvé, elle retourne `null` ;
- le résultat peut être transmis à Twig.
