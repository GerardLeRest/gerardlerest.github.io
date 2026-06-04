---
title: Symfony – Créer un formulaire
author: Gérard LE REST
date: 2026-06-02 18:30:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Formulaire, FormType]
---

# Cours 20 — Créer un formulaire

## Introduction

Symfony utilise des classes FormType pour créer et gérer les formulaires.

Un formulaire permet de saisir et de valider des données.

---

## Créer un formulaire

Commande :

```bash
php bin/console make:form
```

Symfony demande :

```text
The name of the form class:
```

Exemple :

```text
PatientFormType
```

---

## Résultat

Symfony crée le fichier :

```text
src/Form/PatientFormType.php
```

---

## Exemple simple

```php
class PatientFormType extends AbstractType
{
    public function buildForm(
        FormBuilderInterface $builder,
        array $options
    ): void
    {
        $builder
            ->add('nom')
            ->add('prenom');
    }
}
```

---

## Créer le formulaire dans le contrôleur

```php
$patient = new Patient();

$form = $this->createForm(
    PatientFormType::class,
    $patient
);
```

---

## Traiter la saisie

```php
$form->handleRequest($request);

if ($form->isSubmitted() && $form->isValid()) {

}
```

---

## Afficher le formulaire dans Twig

```twig
{% raw %}
{{ form_start(form) }}

{{ form_row(form.nom) }}
{{ form_row(form.prenom) }}

<button type="submit">
    Valider
</button>

{{ form_end(form) }}
{% endraw %}
```

---

## Comprendre le processus

```text
FormType
↓
Contrôleur
↓
handleRequest()
↓
isValid()
↓
Base de données
```

---

## Conclusion

Pour créer un formulaire :

- créer un FormType ;
- créer le formulaire dans le contrôleur ;
- traiter la requête ;
- afficher le formulaire dans Twig.

Méthodes à retenir :

```php
createForm()
handleRequest()
isSubmitted()
isValid()
```
