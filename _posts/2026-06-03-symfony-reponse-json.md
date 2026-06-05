---
title: Symfony – Réponse JSON
author: Gérard LE REST
date: 2026-06-03 11:30:00 +0800
categories: [Symfony, Cours]
tags: [symfony, json, api]
---

# Cours 35 — Réponse JSON

## Introduction

Une réponse JSON permet à Symfony d'envoyer des données à une application ou à un autre programme.

Les API utilisent très souvent ce format.

---

## Exemple simple

```php
return $this->json([
    'message' => 'Bonjour'
]);
```

Résultat :

```json
{
    "message": "Bonjour"
}
```

---

## Plusieurs données

```php
return $this->json([
    'nom' => 'Durand',
    'prenom' => 'Paul'
]);
```

Résultat :

```json
{
    "nom": "Durand",
    "prenom": "Paul"
}
```

---

## Réponse avec un code HTTP

```php
return $this->json(
    ['error' => 'Erreur de saisie'],
    400
);
```

---

## Exemple de succès

```php
return $this->json(
    ['message' => 'Enregistrement effectué'],
    200
);
```

---

## Exemple dans un contrôleur

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

## Utilisation fréquente

```text
Application Android
Application Python
Application JavaScript
API REST
```

---

## Comprendre le processus

```text
Client
↓
Requête
↓
Contrôleur Symfony
↓
JSON
↓
Réponse
```

---

## Exemple réel

```php
return $this->json([
    'id' => 12,
    'nom' => 'Durand'
]);
```

---

## Conclusion

Le format JSON permet d'échanger facilement des données.

Méthode à retenir :

```php
$this->json()
```

Codes fréquents :

```text
200 OK
400 Erreur de saisie
404 Introuvable
```
