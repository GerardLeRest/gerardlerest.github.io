---
title: Symfony – Passer des variables à Twig
author: Gérard LE REST
date: 2026-06-02 12:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, twig, variables]
---

# Cours 7 — Passer des variables à Twig

## Introduction

Un contrôleur peut transmettre des données à une vue Twig.

Ces données sont généralement affichées dans une page HTML.

> **Note Jekyll**
> 
> Les exemples Twig de ce cours sont entourés par les balises Liquid `raw` et `endraw`
> afin d'éviter que Jekyll interprète les expressions Twig.

---

## Principe général

Le contrôleur prépare les données :

```php
return $this->render('accueil/index.html.twig', [
    'prenom' => 'Gérard'
]);
```

Twig les affiche :

{% raw %}

```twig
{{ prenom }}
```

{% endraw %}

---

## Passer une variable

Contrôleur :

```php
#[Route('/bonjour', name: 'app_bonjour')]
public function bonjour(): Response
{
    return $this->render('bonjour/index.html.twig', [
        'prenom' => 'Gérard'
    ]);
}
```

Vue Twig :

{% raw %}

```twig
{{ prenom }}
```

{% endraw %}

Résultat :

```html
Gérard
```

---

## Passer plusieurs variables

Contrôleur :

```php
return $this->render('patient/index.html.twig', [
    'nom' => 'Durand',
    'prenom' => 'Paul'
]);
```

Vue Twig :

{% raw %}

```twig
{{ prenom }} {{ nom }}
```

{% endraw %}

Résultat :

```html
Paul Durand
```

---

## Passer un objet

Contrôleur :

```php
return $this->render('patient/show.html.twig', [
    'patient' => $patient
]);
```

Vue Twig :

{% raw %}

```twig
{{ patient.nom }}
```

{% endraw %}

Résultat :

```html
Durand
```

---

## Conclusion

Pour transmettre des données à Twig :

- utiliser le deuxième paramètre de `render()` ;
- fournir un tableau associatif ;
- utiliser le nom de la clé dans Twig ;
- accéder aux propriétés d'un objet avec la notation point.

Exemple :

```php
'patient' => $patient
```

{% raw %}

```twig
{{ patient.nom }}
```

{% endraw %}
