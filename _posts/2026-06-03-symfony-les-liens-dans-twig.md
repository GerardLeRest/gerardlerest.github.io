---
title: Symfony – Les liens dans Twig
author: Gérard LE REST
date: 2026-06-02 12:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, twig, liens]
---

# Cours 8 — Les liens dans Twig

## Introduction

Twig permet de créer des liens vers les routes Symfony.

Cela évite d'écrire directement les URL dans les pages.

Si une URL change, il suffit de modifier la route.

---

## Principe général

Route :

```php
#[Route('/accueil', name: 'app_accueil')]
```

Vue Twig :

{% raw %}

```twig
<a href="{{ path('app_accueil') }}">Accueil</a>
```

{% endraw %}

Résultat :

```html
<a href="/accueil">Accueil</a>
```

---

## Créer un lien simple

Route :

```php
#[Route('/contact', name: 'app_contact')]
```

Vue Twig :

{% raw %}

```twig
<a href="{{ path('app_contact') }}">Contact</a>
```

{% endraw %}

---

## Créer un lien avec un paramètre

Route :

```php
#[Route('/patient/{id}', name: 'patient_show')]
```

Vue Twig :

{% raw %}

```twig
<a href="{{ path('patient_show', {'id': 12}) }}">
    Voir le patient
</a>
```

{% endraw %}

Résultat :

```text
/patient/12
```

---

## Utiliser une variable comme paramètre

{% raw %}

```twig
<a href="{{ path('patient_show', {'id': patient.id}) }}">
    Voir le patient
</a>
```

{% endraw %}

---

## Créer plusieurs liens dans une boucle

{% raw %}

```twig
{% for patient in patients %}

    <a href="{{ path('patient_show', {'id': patient.id}) }}">
        {{ patient.nom }}
    </a>

{% endfor %}
```

{% endraw %}

---

## Conclusion

Pour créer un lien dans Twig :

- utiliser la fonction `path()` ;
- fournir le nom de la route ;
- transmettre les paramètres si nécessaire ;
- éviter d'écrire directement les URL.

Exemple :

{% raw %}

```twig
<a href="{{ path('app_accueil') }}">Accueil</a>
```

{% endraw %}
