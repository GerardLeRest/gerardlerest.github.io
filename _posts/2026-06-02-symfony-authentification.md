---
title: Symfony – Authentification
author: Gérard LE REST
date: 2026-06-02 20:30:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Sécurité, Authentification]
---

# Cours 24 — Authentification

## Introduction

L'authentification permet à un utilisateur de se connecter à l'application.

Symfony fournit un système de sécurité intégré.

---

## Créer l'authentification

Commande :

```bash
php bin/console make:auth
```

Symfony crée les fichiers nécessaires.

---

## L'entité User

L'utilisateur est généralement représenté par une entité :

```php
class User
{
}
```

Cette entité contient notamment :

```php
$email
$password
```

---

## Connexion

Lors de la connexion :

```text
Email
+
Mot de passe
```

sont vérifiés par Symfony.

---

## Utilisateur connecté

Dans un contrôleur :

```php
$user = $this->getUser();
```

Résultat :

```text
Retourne l'utilisateur connecté.
```

---

## Vérifier le rôle

```php
#[IsGranted('ROLE_USER')]
```

Seuls les utilisateurs connectés peuvent accéder à la page.

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

## Déconnexion

Dans le fichier :

```text
config/packages/security.yaml
```

Symfony gère automatiquement la déconnexion.

---

## Comprendre le processus

```text
Connexion
↓
Authentification
↓
Utilisateur connecté
↓
getUser()
↓
Contrôle des rôles
```

---

## Conclusion

L'authentification permet :

- de connecter un utilisateur ;
- de récupérer l'utilisateur connecté ;
- de protéger certaines pages.

Éléments à retenir :

```php
getUser()

#[IsGranted('ROLE_USER')]
```
