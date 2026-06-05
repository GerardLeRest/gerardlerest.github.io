---
title: Symfony – Injection de dépendances
author: Gérard LE REST
date: 2026-06-03 09:30:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Injection, Service]
---

# Cours 31 — Injection de dépendances

## Introduction

L'injection de dépendances permet à Symfony de fournir automatiquement les objets nécessaires à une classe ou à une méthode.

Cette technique est utilisée partout dans Symfony.

---

## Exemple simple

```php
public function index(
    EntityManagerInterface $entityManager
): Response
{
}
```

Symfony fournit automatiquement :

```php
$entityManager
```

---

## Exemple avec un service

```php
public function index(
    CalculAgeService $calculAgeService
): Response
{
}
```

Symfony crée et fournit le service.

---

## Exemple avec Request

```php
public function index(
    Request $request
): Response
{
}
```

Symfony fournit automatiquement l'objet Request.

---

## Plusieurs dépendances

```php
public function index(
    Request $request,
    EntityManagerInterface $entityManager,
    CalculAgeService $calculAgeService
): Response
{
}
```

---

## Pourquoi utiliser l'injection ?

Permet de :

- éviter les créations manuelles ;
- réduire le code ;
- faciliter les tests ;
- améliorer la maintenance.

---

## Sans injection

```php
$service = new CalculAgeService();
```

---

## Avec injection

```php
CalculAgeService $calculAgeService
```

Symfony s'occupe de tout.

---

## Comprendre le processus

```text
Contrôleur
↓
Symfony
↓
Injection
↓
Objet disponible
```

---

## Exemples fréquents

```php
Request

EntityManagerInterface

Repository

Service
```

---

## Conclusion

L'injection de dépendances est un mécanisme fondamental de Symfony.

À retenir :

- Symfony fournit automatiquement les objets ;
- aucun `new` n'est nécessaire ;
- utilisée avec les services, repositories et Request ;
- simplifie fortement le développement.
