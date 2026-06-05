---
title: Symfony – Les Services
author: Gérard LE REST
date: 2026-06-03 09:00:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Service, Injection]
---

# Cours 30 — Les Services

## Introduction

Un service est une classe qui contient une logique réutilisable.

Il permet d'éviter de placer trop de code dans les contrôleurs.

---

## Exemple

Au lieu d'écrire :

```php
class PatientController
{
    // Beaucoup de code
}
```

on déplace certaines fonctionnalités dans un service.

---

## Créer un service

Créer un fichier :

```text
src/Service/CalculAgeService.php
```

---

## Exemple de service

```php
namespace App\Service;

class CalculAgeService
{
    public function calculer(
        int $anneeNaissance
    ): int
    {
        return date('Y') - $anneeNaissance;
    }
}
```

---

## Utiliser un service

```php
public function index(
    CalculAgeService $calculAgeService
): Response
{
    $age = $calculAgeService->calculer(1980);

    return new Response(
        (string) $age
    );
}
```

---

## Injection de dépendance

Symfony fournit automatiquement le service :

```php
CalculAgeService $calculAgeService
```

dans la méthode du contrôleur.

---

## Pourquoi utiliser un service ?

Permet de :

- réutiliser du code ;
- alléger les contrôleurs ;
- faciliter les tests ;
- améliorer l'organisation du projet.

---

## Comprendre le processus

```text
Contrôleur
↓
Service
↓
Traitement
↓
Résultat
```

---

## Conclusion

Un service contient une logique réutilisable.

À retenir :

- dossier `src/Service` ;
- classe spécialisée ;
- injection automatique ;
- réutilisation du code.
