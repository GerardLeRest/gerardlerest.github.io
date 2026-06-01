---
title: Symfony – Les réponses HTTP
author: Gérard LE REST
date: 2026-05-29 18:00:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Response, HTTP]
---

# Cours 4 — Les réponses HTTP

## Présentation

Après avoir exécuté un contrôleur, Symfony doit renvoyer une réponse au navigateur.

Cette réponse est appelée une **réponse HTTP**.

Sans réponse HTTP, le navigateur ne reçoit rien.

---

## Schéma général

```text
Navigateur
    ↓
Route
    ↓
Contrôleur
    ↓
Response
    ↓
Navigateur
```

---

## 1. Réponse texte simple

```php
use Symfony\Component\HttpFoundation\Response;

#[Route('/bonjour', name: 'app_bonjour')]
public function bonjour(): Response
{
    return new Response('Bonjour');
}
```

Résultat :

```text
Bonjour
```

---

## Comment lire ce code ?

```php
return new Response('Bonjour');
```

Signifie :

```text
Créer une réponse HTTP
contenant le texte Bonjour.
```

---

## 2. Réponse HTML

```php
return new Response('<h1>Bonjour</h1>');
```

Résultat :

```html
<h1>Bonjour</h1>
```

Le navigateur interprète alors le HTML.

---

## 3. Réponse générée par Twig

Le cas le plus fréquent dans Symfony.

```php
return $this->render(
    'accueil/index.html.twig'
);
```

---

## Ce qui se passe

```text
Twig
    ↓
HTML
    ↓
Response
    ↓
Navigateur
```

Même si tu ne vois pas explicitement l'objet Response, Symfony le crée automatiquement.

---

## 4. Réponse avec variables Twig

```php
return $this->render(
    'patient/show.html.twig',
    [
        'nom' => 'Dupont'
    ]
);
```

Twig :

```twig
<h1>{{ nom }}</h1>
```

Résultat :

```html
<h1>Dupont</h1>
```

---

## 5. Réponse JSON

Très utilisée pour les API.

```php
return $this->json([
    'nom' => 'Dupont',
    'age' => 42
]);
```

Résultat :

```json
{
    "nom": "Dupont",
    "age": 42
}
```

---

## Pourquoi est-ce utile ?

Une application Android, Flutter ou JavaScript peut lire directement ces données.

C'est exactement le principe utilisé par de nombreuses API.

---

## 6. Réponse vide

```php
return new Response();
```

Symfony renvoie simplement une réponse vide.

---

## À retenir

Une réponse HTTP est le résultat final envoyé au navigateur.

Dans Symfony, elle peut contenir :

- du texte ;
- du HTML ;
- une page Twig ;
- du JSON.

Schéma mental :

```text
Contrôleur
 ↓
Response
 ↓
Navigateur
```

---

## Conclusion

La réponse HTTP est l'étape finale du traitement d'une requête.

Quand tu lis un contrôleur Symfony, la première chose à regarder est souvent :

```php
return ...
```

C'est cette instruction qui détermine ce que recevra réellement l'utilisateur.
