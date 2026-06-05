---
title: Symfony – Afficher un formulaire Twig
author: Gérard LE REST
date: 2026-06-02 19:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, twig, formulaire]
---

# Cours 21 — Afficher un formulaire Twig

## Introduction

Une fois le formulaire créé dans le contrôleur, il doit être affiché dans une vue Twig.

Symfony fournit plusieurs fonctions pour afficher facilement les champs.

---

## Contrôleur

```php
return $this->render('patient/index.html.twig', [
    'form' => $form->createView()
]);
```

---

## Afficher tout le formulaire

```twig
{% raw %}
{{ form(form) }}
{% endraw %}
```

Symfony affiche automatiquement tous les champs.

---

## Afficher le début et la fin du formulaire

```twig
{% raw %}
{{ form_start(form) }}

{{ form_end(form) }}
{% endraw %}
```

---

## Afficher un champ

```twig
{% raw %}
{{ form_row(form.nom) }}
{% endraw %}
```

Résultat :

```text
Label + Champ + Erreurs
```

---

## Afficher séparément

```twig
{% raw %}
{{ form_label(form.nom) }}

{{ form_widget(form.nom) }}

{{ form_errors(form.nom) }}
{% endraw %}
```

---

## Exemple complet

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

## Ajouter une classe Bootstrap

```twig
{% raw %}
{{ form_widget(
    form.nom,
    {
        'attr': {
            'class': 'form-control'
        }
    }
) }}
{% endraw %}
```

---

## Comprendre le processus

```text
FormType
↓
Contrôleur
↓
createView()
↓
Twig
↓
Affichage HTML
```

---

## Conclusion

Pour afficher un formulaire :

- transmettre le formulaire à Twig ;
- utiliser `form_start()` ;
- afficher les champs ;
- utiliser `form_end()`.

Fonctions à retenir :

```twig
form_start()
form_end()
form_row()
form_label()
form_widget()
form_errors()
```
