---
title: Symfony – Les vues Twig
author: Gérard LE REST
date: 2026-06-01 12:02:00 +0800
categories: [Symfony, Cours]
tags: [symfony, twig, vue]
---

# Cours 6 — Les vues Twig

## Introduction

Une vue Twig permet d'afficher des pages HTML dans Symfony.

Le contrôleur prépare les données puis les transmet à Twig qui se charge de l'affichage.

Twig évite de mélanger le code PHP et le code HTML.

> **Note Jekyll**
> 
> Dans un site Jekyll, le moteur Liquid utilise aussi les accolades de Twig.
> Pour afficher du code Twig dans un article, il faut entourer les blocs Twig avec les balises `raw` et `endraw` de Liquid.
> Dans le texte du cours, on évite d'écrire directement les symboles Twig complets afin que Jekyll ne les interprète pas.

---

## Créer une vue Twig

Créer un fichier dans le dossier :

```text
templates/
```

Exemple :

```text
templates/accueil/index.html.twig
```

Contenu :

```twig
<h1>Bienvenue sur SoigneMoi</h1>
```

---

## Afficher une vue depuis un contrôleur

```php
#[Route('/accueil', name: 'app_accueil')]
public function index(): Response
{
    return $this->render('accueil/index.html.twig');
}
```

Lorsque l'utilisateur appelle l'URL :

```text
/accueil
```

Symfony affiche :

```text
templates/accueil/index.html.twig
```

---

## Afficher une variable

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
<h1>Bonjour {{ prenom }}</h1>
```

{% endraw %}

Résultat :

```html
Bonjour Gérard
```

---

## Afficher plusieurs variables

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
<p>{{ prenom }} {{ nom }}</p>
```

{% endraw %}

---

## Afficher une condition

{% raw %}

```twig
{% if age >= 18 %}
    <p>Adulte</p>
{% else %}
    <p>Mineur</p>
{% endif %}
```

{% endraw %}

---

## Afficher une boucle

{% raw %}

```twig
{% for patient in patients %}
    <p>{{ patient.nom }}</p>
{% endfor %}
```

{% endraw %}

---

## Conclusion

Twig est le moteur d'affichage de Symfony.

À retenir :

- les vues se trouvent dans le dossier `templates` ;
- un contrôleur utilise `render()` pour afficher une vue ;
- les variables sont affichées avec les doubles accolades Twig ;
- les structures de contrôle utilisent les balises Twig avec pourcentage ;
- Twig permet de séparer clairement l'affichage et le traitement.
