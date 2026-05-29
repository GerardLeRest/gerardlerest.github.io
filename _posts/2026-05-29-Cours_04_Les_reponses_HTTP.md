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

## Exemple inspiré de SoigneMoi

Imaginons :

```php
#[Route('/patient/{id}')]
public function show(
    int $id,
    PatientRepository $patientRepository
): Response
{
    $patient = $patientRepository->find($id);

    return $this->render(
        'patient/show.html.twig',
        [
            'patient' => $patient
        ]
    );
}
```

Cheminement :

```text
URL
    ↓
Contrôleur
    ↓
Repository
    ↓
Patient
    ↓
Twig
    ↓
Response
    ↓
Navigateur
```

---

## Ce que Symfony fait automatiquement

Symfony :

- crée l'objet Response ;
- ajoute les en-têtes HTTP ;
- envoie la réponse au navigateur ;
- transforme Twig en HTML ;
- transforme un tableau PHP en JSON.

---

## Ce que le développeur écrit

Le développeur décide :

- du contenu à envoyer ;
- du template Twig à utiliser ;
- des données à transmettre ;
- du format (HTML, JSON, texte...).

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

## Erreurs fréquentes

### Oublier le return

Incorrect :

```php
$this->render('accueil/index.html.twig');
```

Correct :

```php
return $this->render(
    'accueil/index.html.twig'
);
```

---

### Retourner autre chose qu'une Response

Incorrect :

```php
return "Bonjour";
```

Correct :

```php
return new Response("Bonjour");
```

ou

```php
return $this->render(...);
```

---

## Conclusion

La réponse HTTP est l'étape finale du traitement d'une requête.

Quand tu lis un contrôleur Symfony, la première chose à regarder est souvent :

```php
return ...
```

C'est cette instruction qui détermine ce que recevra réellement l'utilisateur.
