---
title: Symfony – L'entité User
author: Gérard LE REST
date: 2026-06-02 21:00:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, User, Sécurité]
---

# Cours 25 — L'entité User

## Introduction

L'entité User représente un utilisateur de l'application.

Elle est utilisée par le système d'authentification de Symfony.

---

## Création

Commande :

```bash
php bin/console make:user
```

Symfony crée l'entité :

```text
src/Entity/User.php
```

---

## Exemple simplifié

```php
class User
{
    private ?int $id = null;

    private ?string $email = null;

    private ?string $password = null;
}
```

---

## Identifiant de connexion

```php
private ?string $email = null;
```

L'email permet d'identifier l'utilisateur.

---

## Mot de passe

```php
private ?string $password = null;
```

Le mot de passe est stocké sous forme hachée.

---

## Les rôles

```php
private array $roles = [];
```

Exemple :

```php
['ROLE_USER']
```

---

## Lire l'utilisateur connecté

```php
$user = $this->getUser();
```

Résultat :

```text
Retourne l'utilisateur connecté.
```

---

## Accéder à l'email

```php
$user->getEmail();
```

---

## Accéder aux rôles

```php
$user->getRoles();
```

---

## Exemple

```php
$user = $this->getUser();

$email = $user->getEmail();
```

---

## Comprendre le processus

```text
Connexion
↓
User
↓
getUser()
↓
Email
Rôles
Identité
```

---

## Conclusion

L'entité User représente l'utilisateur connecté.

À retenir :

- email ;
- mot de passe ;
- rôles ;
- `getUser()` ;
- `getEmail()` ;
- `getRoles()`.
