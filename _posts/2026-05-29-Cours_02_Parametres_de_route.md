---
title: Symfony – Les paramètres de route
author: Gérard LE REST
date: 2026-05-29 17:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, route, parametre]
---

# Cours 2 — Les paramètres de route

## Présentation

Les paramètres de route permettent de transmettre des informations depuis l'URL vers le contrôleur.

Grâce à eux, une même route peut servir à afficher des patients différents, des séjours différents ou des avis différents.

---

## Schéma général

```text
URL
    ↓
Route
    ↓
Extraction des paramètres
    ↓
Contrôleur
```

---

## 1. Paramètre simple

```php
#[Route('/patient/{id}', name: 'patient_show')]
public function show(int $id): Response
{
    return new Response("Patient : $id");
}
```

URL :

```text
/patient/12
```

Résultat :

```text
Patient : 12
```

---

## Comment lire cette route ?

```php
/ patient / {id}
```

Signifie :

```text
La partie fixe est : patient
La partie variable est : id
```

Symfony récupère automatiquement la valeur.

---

## 2. Plusieurs paramètres

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

## Ce que Symfony fait

Symfony transforme :

```text
/sejour/15/2026
```

en :

```php
show(15, 2026)
```

---

## 3. Paramètre texte

```php
#[Route('/ville/{nom}', name: 'ville_show')]
public function show(string $nom): Response
{
    return new Response($nom);
}
```

URL :

```text
/ville/Anvers
```

Résultat :

```text
Anvers
```

---

## 4. Contraindre un paramètre

Par défaut Symfony accepte tout.

On peut limiter aux nombres :

```php
#[Route(
    '/patient/{id<\d+>}',
    name: 'patient_show'
)]
```

Valide :

```text
/patient/12
```

Invalide :

```text
/patient/toto
```

---

## Pourquoi utiliser une contrainte ?

Pour éviter qu'une URL incorrecte arrive dans le contrôleur.

Symfony bloque l'accès avant même l'exécution du code.

---

## 5. Valeur par défaut

```php
#[Route(
    '/annee/{annee}',
    name: 'annee_show',
    defaults: ['annee' => 2026]
)]
```

URL :

```text
/annee
```

Résultat :

```text
2026
```

---

## Exemple inspiré de SoigneMoi

```php
#[Route('/patient/{id}', name: 'patient_show')]
public function show(int $id)
```

URL :

```text
/patient/25
```

Symfony appelle :

```php
show(25)
```

Puis le contrôleur pourra demander :

```php
$patientRepository->find(25);
```

pour récupérer le patient.

---

## Ce que Symfony fait automatiquement

Symfony :

- lit l'URL ;
- détecte les paramètres ;
- vérifie les contraintes ;
- transmet les valeurs au contrôleur.

---

## Ce que le développeur écrit

Le développeur choisit :

- le nom du paramètre ;
- son type ;
- les contraintes éventuelles ;
- la logique métier.

---

## À retenir

Les paramètres de route permettent :

- d'identifier un enregistrement ;
- de transmettre une information au contrôleur ;
- de réutiliser une même route avec plusieurs valeurs.

Schéma mental :

```text
URL
 ↓
Paramètre
 ↓
Contrôleur
```

---

## Erreurs fréquentes

### Nom différent

Incorrect :

```php
#[Route('/patient/{id}')]

public function show(int $numero)
```

Correct :

```php
#[Route('/patient/{id}')]

public function show(int $id)
```

---

### Oublier les accolades

Incorrect :

```php
'/patient/id'
```

Correct :

```php
'/patient/{id}'
```

---

## Conclusion

Les paramètres de route permettent à Symfony de transmettre des informations depuis l'URL vers le contrôleur.

Ils sont utilisés partout dans les applications Symfony, notamment pour afficher, modifier ou supprimer un enregistrement précis.
