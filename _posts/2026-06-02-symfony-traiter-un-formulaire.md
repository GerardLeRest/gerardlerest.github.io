---
title: Symfony – Traiter un formulaire
author: Gérard LE REST
date: 2026-06-02 19:30:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Formulaire, Contrôleur]
---

# Cours 22 — Traiter un formulaire

## Introduction

Après l'affichage du formulaire, le contrôleur doit traiter les données saisies par l'utilisateur.

Symfony fournit plusieurs méthodes pour effectuer ce traitement.

---

## Récupérer les données

```php
$form->handleRequest($request);
```

Cette méthode récupère les données envoyées par le formulaire.

---

## Vérifier la soumission

```php
if ($form->isSubmitted()) {

}
```

Résultat :

```text
Le formulaire a été envoyé.
```

---

## Vérifier la validité

```php
if (
    $form->isSubmitted() &&
    $form->isValid()
) {

}
```

Résultat :

```text
Le formulaire est envoyé et valide.
```

---

## Exemple complet

```php
$form->handleRequest($request);

if (
    $form->isSubmitted() &&
    $form->isValid()
) {

    // Traitement

}
```

---

## Enregistrer les données

```php
$entityManager->persist($patient);
$entityManager->flush();
```

---

## Rediriger l'utilisateur

```php
return $this->redirectToRoute(
    'app_home'
);
```

---

## Exemple complet dans un contrôleur

```php
$form = $this->createForm(
    PatientFormType::class,
    $patient
);

$form->handleRequest($request);

if (
    $form->isSubmitted() &&
    $form->isValid()
) {

    $entityManager->persist($patient);
    $entityManager->flush();

    return $this->redirectToRoute(
        'app_home'
    );
}
```

---

## Comprendre le processus

```text
Affichage
↓
Saisie utilisateur
↓
handleRequest()
↓
isSubmitted()
↓
isValid()
↓
persist()
↓
flush()
↓
Redirection
```

---

## Conclusion

Pour traiter un formulaire :

- récupérer les données ;
- vérifier la soumission ;
- vérifier la validité ;
- enregistrer les données ;
- rediriger l'utilisateur.

Méthodes à retenir :

```php
handleRequest()
isSubmitted()
isValid()
persist()
flush()
redirectToRoute()
```
