---
title: Symfony – Rechercher plusieurs enregistrements
author: Gérard LE REST
date: 2026-06-02 15:00:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Doctrine, Repository]
---

# Cours 13 — Rechercher plusieurs enregistrements

## Introduction

Les méthodes `findAll()` et `findBy()` permettent de récupérer plusieurs enregistrements.

Elles sont fournies par le repository de l'entité.

---

## Rechercher tous les enregistrements

```php
$patients = $patientRepository->findAll();
```

Résultat :

```text
Retourne tous les patients.
```

---

## Utiliser findAll() dans un contrôleur

```php
#[Route('/patients', name: 'patient_liste')]
public function index(
    PatientRepository $patientRepository
): Response
{
    $patients = $patientRepository->findAll();

    return $this->render('patient/index.html.twig', [
        'patients' => $patients
    ]);
}
```

---

## Afficher les résultats dans Twig

{% raw %}
```twig
{% for patient in patients %}
    {{ patient.nom }}
{% endfor %}
```
{% endraw %}

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

## Plusieurs critères

```php
$patients = $patientRepository->findBy([
    'nom' => 'Durand',
    'prenom' => 'Paul'
]);
```

Résultat :

```text
Retourne les patients correspondant aux deux critères.
```

---

## Comprendre le résultat

```php
$patients = $patientRepository->findAll();
```

Retourne :

```text
Une collection d'objets Patient.
```

Contrairement à :

```php
$patient = $patientRepository->find($id);
```

qui retourne :

```text
Un seul objet Patient.
```

---

## Conclusion

Pour rechercher plusieurs enregistrements :

```php
findAll()
findBy()
```

À retenir :

- `findAll()` retourne tous les enregistrements ;
- `findBy()` applique un ou plusieurs critères ;
- le résultat est une collection d'objets ;
- Twig utilise généralement une boucle `for` pour afficher les résultats.
