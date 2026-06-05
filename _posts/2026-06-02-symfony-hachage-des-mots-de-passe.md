---
title: Symfony – Hachage des mots de passe
author: Gérard LE REST
date: 2026-06-02 21:30:00 +0800
categories: [Symfony, Cours]
tags: [symfony, securite, Mot de passe]
---

# Cours 26 — Hachage des mots de passe

## Introduction

Un mot de passe ne doit jamais être enregistré en clair dans la base de données.

Symfony utilise un système de hachage sécurisé.

---

## Mot de passe en clair

À éviter :

```text
azerty123
```

Si la base est compromise, le mot de passe est visible.

---

## Mot de passe haché

Exemple :

```text
$2y$13$4M...
```

Le mot de passe devient illisible.

---

## Hachage avec Symfony

```php
$hashedPassword =
    $passwordHasher->hashPassword(
        $user,
        $password
    );
```

---

## Enregistrer le mot de passe

```php
$user->setPassword(
    $hashedPassword
);
```

---

## Exemple complet

```php
$hashedPassword =
    $passwordHasher->hashPassword(
        $user,
        $password
    );

$user->setPassword(
    $hashedPassword
);
```

---

## Vérification lors de la connexion

L'utilisateur saisit :

```text
Email
Mot de passe
```

Symfony compare automatiquement le mot de passe saisi avec le mot de passe haché enregistré.

---

## Comprendre le processus

```text
Mot de passe
↓
hashPassword()
↓
Valeur hachée
↓
Base de données
```

---

## Pourquoi hacher ?

Le mot de passe réel n'est jamais stocké.

Même l'administrateur de la base ne peut pas le lire.

---

## Conclusion

Pour sécuriser un mot de passe :

```php
$passwordHasher->hashPassword()
```

À retenir :

- ne jamais stocker un mot de passe en clair ;
- utiliser `hashPassword()` ;
- enregistrer uniquement la valeur hachée ;
- Symfony vérifie automatiquement le mot de passe lors de la connexion.
