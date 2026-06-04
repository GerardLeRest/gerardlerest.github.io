---
title: Symfony – Les Voters
author: Gérard LE REST
date: 2026-06-02 23:00:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Sécurité, Voter]
---

# Cours 29 — Les Voters

## Introduction

Un Voter permet de définir des règles d'autorisation personnalisées.

Il complète le système de rôles de Symfony.

---

## Pourquoi utiliser un Voter ?

Les rôles permettent de répondre à la question :

```text
L'utilisateur possède-t-il le rôle demandé ?
```

Un Voter permet de répondre à la question :

```text
L'utilisateur a-t-il le droit d'accéder à cet objet ?
```

---

## Exemple

```text
Patient connecté
↓
Peut consulter son séjour
```

mais :

```text
Patient connecté
↓
Ne peut pas consulter le séjour d'un autre patient
```

---

## Créer un Voter

Commande :

```bash
php bin/console make:voter
```

Symfony crée :

```text
src/Security/SejourVoter.php
```

---

## Vérifier une autorisation

```php
$this->denyAccessUnlessGranted(
    'VIEW',
    $sejour
);
```

---

## Exemple dans un contrôleur

```php
$sejour = $repository->find($id);

$this->denyAccessUnlessGranted(
    'VIEW',
    $sejour
);
```

---

## Résultat

```text
Autorisé
↓
Le contrôleur continue
```

ou :

```text
Refusé
↓
Erreur 403
```

---

## Principe du Voter

```text
Utilisateur
↓
Objet
↓
Voter
↓
Autorisation ou refus
```

---

## Différence avec les rôles

```php
#[IsGranted('ROLE_USER')]
```

Vérifie :

```text
Le rôle.
```

Un Voter vérifie :

```text
Les droits sur un objet précis.
```

---

## Conclusion

Les Voters permettent de gérer des règles de sécurité avancées.

À retenir :

```php
denyAccessUnlessGranted()
```

Commande :

```bash
php bin/console make:voter
```

Utilisation :

```text
Utilisateur
+
Objet
↓
Autorisation
```
