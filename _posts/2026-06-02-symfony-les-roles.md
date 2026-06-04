---
title: Symfony – Les rôles
author: Gérard LE REST
date: 2026-06-02 22:00:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Sécurité, Rôles]
---

# Cours 27 — Les rôles

## Introduction

Les rôles permettent de contrôler l'accès aux différentes parties d'une application.

Chaque utilisateur possède un ou plusieurs rôles.

---

## Exemple de rôle

```php
['ROLE_USER']
```

Ce rôle correspond à un utilisateur connecté.

---

## Définir un rôle

```php
$user->setRoles([
    'ROLE_USER'
]);
```

---

## Plusieurs rôles

```php
$user->setRoles([
    'ROLE_USER',
    'ROLE_ADMIN'
]);
```

---

## Vérifier un rôle

```php
#[IsGranted('ROLE_USER')]
```

Seuls les utilisateurs possédant ce rôle peuvent accéder à la page.

---

## Exemple dans un contrôleur

```php
#[Route('/sejour')]
#[IsGranted('ROLE_USER')]
public function index(): Response
{
    return new Response('Accès autorisé');
}
```

---

## Vérification dans le code

```php
if (
    $this->isGranted('ROLE_ADMIN')
) {
    // Action réservée à l'administrateur
}
```

---

## Lire les rôles

```php
$user = $this->getUser();

$roles = $user->getRoles();
```

---

## Rôles fréquents

```text
ROLE_USER
ROLE_ADMIN
ROLE_SUPER_ADMIN
```

---

## Comprendre le processus

```text
Connexion
↓
Utilisateur
↓
Rôles
↓
Contrôle d'accès
```

---

## Conclusion

Les rôles permettent de sécuriser l'application.

À retenir :

```php
setRoles()

getRoles()

#[IsGranted('ROLE_USER')]

isGranted()
```
