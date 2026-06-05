---
title: Symfony – Restriction d'accès
author: Gérard LE REST
date: 2026-06-02 22:30:00 +0800
categories: [Symfony, Cours]
tags: [symfony, securite, acces]
---

# Cours 28 — Restriction d'accès

## Introduction

Symfony permet de limiter l'accès à certaines pages.

La restriction peut être basée sur les rôles de l'utilisateur.

---

## Restriction avec IsGranted

```php
#[IsGranted('ROLE_USER')]
```

Seuls les utilisateurs possédant ce rôle peuvent accéder à la page.

---

## Exemple

```php
#[Route('/sejour')]
#[IsGranted('ROLE_USER')]
public function index(): Response
{
    return new Response('Accès autorisé');
}
```

---

## Restriction pour un administrateur

```php
#[IsGranted('ROLE_ADMIN')]
```

Seuls les administrateurs peuvent accéder à la page.

---

## Vérification dans le contrôleur

```php
if (!$this->isGranted('ROLE_ADMIN')) {
    throw $this->createAccessDeniedException();
}
```

---

## Erreur d'accès

```php
throw $this->createAccessDeniedException();
```

Résultat :

```text
Erreur 403 - Accès interdit
```

---

## Utiliser getUser()

```php
$user = $this->getUser();
```

Permet de récupérer l'utilisateur connecté.

---

## Exemple réel

```php
#[Route('/profil')]
#[IsGranted('ROLE_USER')]
public function profil(): Response
{
    $user = $this->getUser();

    return new Response(
        $user->getEmail()
    );
}
```

---

## Comprendre le processus

```text
Utilisateur
↓
Connexion
↓
Rôle
↓
Contrôle d'accès
↓
Page autorisée ou refusée
```

---

## Conclusion

La restriction d'accès permet de protéger les pages sensibles.

À retenir :

```php
#[IsGranted(...)]

isGranted()

createAccessDeniedException()
```
