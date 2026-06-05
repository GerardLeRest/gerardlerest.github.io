---
title: Symfony – Les routes Symfony
author: Gérard LE REST
date: 2026-05-29 16:30:00 +0800
categories: [Symfony, Cours]
tags: [symfony, route, controleur]
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

## Conclusion

Les routes sont la porte d'entrée de Symfony.

Lorsque tu ouvriras un contrôleur dans SoigneMoi, la première chose à regarder sera généralement l'attribut :

```php
#[Route(...)]
```

Il indique comment l'utilisateur arrive dans le code.
