---
title: Symfony – Les routes Symfony
author: Gérard LE REST
date: 2026-05-29 16:30:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Route, Contrôleur]
---

# Cours 1 — Les routes Symfony

## Présentation

Une route est le point d'entrée d'une application Symfony.

Lorsqu'un utilisateur saisit une URL dans son navigateur, Symfony recherche une route correspondant à cette URL puis appelle le contrôleur associé.

Sans route, Symfony ne sait pas quel code exécuter.

---

## Schéma général

```text
Navigateur
    ↓
URL
    ↓
Route Symfony
    ↓
Contrôleur
    ↓
Réponse HTTP
    ↓
Navigateur
```

---

## 1. Route simple

```php
#[Route('/bonjour', name: 'app_bonjour')]
public function bonjour(): Response
{
    return new Response('Bonjour');
}
```

URL :

```text
http://localhost:8000/bonjour
```

Résultat :

```text
Bonjour
```

---

## Comment lire cette route ?

```php
#[Route('/bonjour', name: 'app_bonjour')]
```

Signifie :

```text
Si l'utilisateur demande /bonjour,
alors Symfony exécute cette méthode.
```

Le nom :

```php
name: 'app_bonjour'
```

permet de générer des liens ailleurs dans l'application.

---

## 2. Route avec paramètre

```php
#[Route('/patient/{id}', name: 'patient_show')]
public function show(int $id): Response
{
    return new Response("Patient : $id");
}
```

URL :

```text
http://localhost:8000/patient/12
```

Résultat :

```text
Patient : 12
```

---

## Comment lire cette route ?

Symfony détecte automatiquement :

```text
/patient/12
```

et extrait :

```text
id = 12
```

Puis il appelle :

```php
show(12)
```

---

## 3. Plusieurs paramètres

```php
#[Route('/sejour/{id}/{annee}', name: 'sejour_show')]
public function show(int $id, int $annee): Response
{
    return new Response("$id - $annee");
}
```

URL :

```text
/sejour/15/2026
```

Résultat :

```text
15 - 2026
```

---

## Ce que Symfony fait automatiquement

Symfony :

- analyse l'URL ;
- compare toutes les routes ;
- trouve la bonne route ;
- extrait les paramètres ;
- appelle le contrôleur ;
- transmet les paramètres à la méthode.

---

## Ce que le développeur écrit

Le développeur écrit :

```php
#[Route('/patient/{id}', name: 'patient_show')]
```

et :

```php
public function show(int $id)
```

Symfony s'occupe du reste.

---

## Exemple inspiré de SoigneMoi

Imaginons :

```php
#[Route('/patient/{id}', name: 'patient_show')]
public function show(int $id)
```

L'utilisateur demande :

```text
/patient/25
```

Symfony exécute :

```php
show(25)
```

Le contrôleur peut alors récupérer le patient n°25 dans la base de données.

---

## À retenir

Une route :

- associe une URL à un contrôleur ;
- peut contenir des paramètres ;
- est le point d'entrée de Symfony ;
- permet de transmettre des informations au contrôleur.

Schéma mental à retenir :

```text
URL
 ↓
Route
 ↓
Contrôleur
 ↓
Réponse
```

---

## Erreurs fréquentes

### Oublier le caractère #

Incorrect :

```php
[Route('/bonjour')]
```

Correct :

```php
#[Route('/bonjour')]
```

### Nom de paramètre différent

Incorrect :

```php
#[Route('/patient/{id}')]

public function show(int $numero)
```

Symfony ne trouve pas la correspondance.

Correct :

```php
#[Route('/patient/{id}')]

public function show(int $id)
```

---

## Conclusion

Les routes sont la porte d'entrée de Symfony.

Lorsque tu ouvriras un contrôleur dans SoigneMoi, la première chose à regarder sera généralement l'attribut :

```php
#[Route(...)]
```

Il indique comment l'utilisateur arrive dans le code.
