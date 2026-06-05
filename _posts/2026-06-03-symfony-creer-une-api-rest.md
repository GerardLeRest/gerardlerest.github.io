---
---
title: "Symfony - Créer une API REST"
author: "Gérard LE REST"
date: 2026-06-03 12:00:00 +0200
categories: [Symfony, Cours]
tags: [symfony, api, rest, json]
---
---

# Cours 36 — Créer une API REST

## Introduction

Une API REST permet à une application externe de communiquer avec Symfony.

Les échanges se font généralement au format JSON.

---

## Créer une route API

```php
#[Route('/api/patient')]
```

Cette URL sera utilisée par un programme externe.

---

## Exemple simple

```php
#[Route('/api/test')]
public function test(): Response
{
    return $this->json([
        'message' => 'API opérationnelle'
    ]);
}
```

---

## Résultat

```json
{
    "message": "API opérationnelle"
}
```

---

## Recevoir des données JSON

```php
$donnees = json_decode(
    $request->getContent(),
    true
);
```

---

## Exemple

JSON reçu :

```json
{
    "nom": "Durand",
    "prenom": "Paul"
}
```

---

## Lire les données

```php
$nom = $donnees['nom'];

$prenom = $donnees['prenom'];
```

---

## Retourner une réponse

```php
return $this->json([
    'message' => 'Patient enregistré'
]);
```

---

## Exemple complet

```php
#[Route('/api/patient')]
public function patient(
    Request $request
): Response
{
    $donnees = json_decode(
        $request->getContent(),
        true
    );

    return $this->json([
        'nom' => $donnees['nom']
    ]);
}
```

---

## Utilisation fréquente

```text
Application Android
Application Python
Application JavaScript
```

---

## Comprendre le processus

```text
Application
↓
JSON
↓
Symfony
↓
Traitement
↓
JSON
↓
Réponse
```

---

## Conclusion

Une API REST permet d'échanger des données avec Symfony.

Éléments à retenir :

```php
json_decode()

$request->getContent()

$this->json()
```
