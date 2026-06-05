---
title: Symfony – Validation des données
author: Gérard LE REST
date: 2026-06-02 20:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, validation, formulaire]
---

# Cours 23 — Validation des données

## Introduction

Symfony permet de vérifier automatiquement les données saisies par l'utilisateur.

Les règles de validation sont généralement placées dans les entités.

---

## Importer les contraintes

```php
use Symfony\Component\Validator\Constraints as Assert;
```

---

## Champ obligatoire

```php
#[Assert\NotBlank]
private ?string $nom = null;
```

Résultat :

```text
Le champ nom ne peut pas être vide.
```

---

## Longueur minimale et maximale

```php
#[Assert\Length(
    min: 2,
    max: 50
)]
private ?string $nom = null;
```

Résultat :

```text
Le nom doit contenir entre 2 et 50 caractères.
```

---

## Vérifier une adresse email

```php
#[Assert\Email]
private ?string $email = null;
```

Résultat :

```text
L'adresse email doit être valide.
```

---

## Combiner plusieurs contraintes

```php
#[Assert\NotBlank]
#[Assert\Length(min: 2, max: 50)]
private ?string $nom = null;
```

---

## Déclencher la validation

```php
$form->handleRequest($request);

if (
    $form->isSubmitted() &&
    $form->isValid()
) {

}
```

La méthode `isValid()` vérifie automatiquement les contraintes.

---

## Afficher les erreurs

```twig
{% raw %}
{{ form_errors(form.nom) }}
{% endraw %}
```

---

## Comprendre le processus

```text
Saisie utilisateur
↓
Validation
↓
isValid()
↓
Erreurs éventuelles
↓
Enregistrement
```

---

## Conclusion

La validation permet de sécuriser les données.

Contraintes à retenir :

```php
NotBlank
Length
Email
```

Méthode à retenir :

```php
isValid()
```
