---
title: Symfony – Consommer une API
author: Gérard LE REST
date: 2026-06-03 12:30:00 +0800
categories: [Symfony, Cours]
tags: [symfony, api, http-client]
---

# Cours 37 — Consommer une API

## Introduction

Consommer une API consiste à interroger un service externe afin de récupérer des données.

Symfony fournit un composant HTTP Client pour effectuer ces requêtes.

---

## Installer le composant

```bash
composer require symfony/http-client
```

---

## Injection du client HTTP

```php
use Symfony\Contracts\HttpClient\HttpClientInterface;
```

---

## Exemple simple

```php
public function index(
    HttpClientInterface $httpClient
): Response
{
}
```

Symfony fournit automatiquement le client HTTP.

---

## Envoyer une requête GET

```php
$response = $httpClient->request(
    'GET',
    'https://api.exemple.com/patients'
);
```

---

## Lire la réponse

```php
$donnees = $response->toArray();
```

---

## Exemple complet

```php
$response = $httpClient->request(
    'GET',
    'https://api.exemple.com/patients'
);

$donnees = $response->toArray();
```

---

## Accéder aux données

```php
$nom = $donnees['nom'];
```

---

## Envoyer des données

```php
$response = $httpClient->request(
    'POST',
    'https://api.exemple.com/patients',
    [
        'json' => [
            'nom' => 'Durand'
        ]
    ]
);
```

---

## Comprendre le processus

```text
Symfony
↓
Requête HTTP
↓
API distante
↓
Réponse JSON
↓
Traitement
```

---

## Utilisation fréquente

```text
Météo
Paiement
Cartographie
Services externes
```

---

## Conclusion

Consommer une API permet d'utiliser des services externes.

Éléments à retenir :

```php
HttpClientInterface

request()

toArray()
```
