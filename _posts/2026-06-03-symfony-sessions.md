---
title: Symfony – Les sessions
author: Gérard LE REST
date: 2026-06-03 10:30:00 +0800
categories: [Symfony, Cours]
tags: [symfony, session, securite]
---

# Cours 33 — Les sessions

## Introduction

Une session permet de conserver des informations entre plusieurs pages.

Symfony utilise automatiquement les sessions pour gérer les utilisateurs connectés.

---

## Exemple

```text
Connexion utilisateur
↓
Session créée
↓
Navigation sur le site
```

L'utilisateur reste connecté.

---

## Récupérer la session

```php
$session = $request->getSession();
```

---

## Enregistrer une valeur

```php
$session->set(
    'prenom',
    'Gérard'
);
```

---

## Lire une valeur

```php
$prenom = $session->get(
    'prenom'
);
```

---

## Supprimer une valeur

```php
$session->remove(
    'prenom'
);
```

---

## Détruire la session

```php
$session->invalidate();
```

Résultat :

```text
Toutes les données de session sont supprimées.
```

---

## Exemple complet

```php
$session = $request->getSession();

$session->set(
    'prenom',
    'Gérard'
);

$prenom = $session->get(
    'prenom'
);
```

---

## Utilisation fréquente

```text
Utilisateur connecté
Panier
Préférences
Messages temporaires
```

---

## Comprendre le processus

```text
Navigateur
↓
Session
↓
Données conservées
↓
Nouvelle page
```

---

## Conclusion

Les sessions permettent de conserver des informations entre plusieurs requêtes.

Méthodes à retenir :

```php
set()

get()

remove()

invalidate()
```
