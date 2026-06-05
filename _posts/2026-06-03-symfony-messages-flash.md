---
title: Symfony – Les messages Flash
author: Gérard LE REST
date: 2026-06-03 11:00:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Flash, Session]
---

# Cours 34 — Les messages Flash

## Introduction

Les messages Flash permettent d'afficher un message temporaire à l'utilisateur.

Ils sont souvent utilisés après une action réussie ou en cas d'erreur.

---

## Ajouter un message

```php
$this->addFlash(
    'success',
    'Inscription réussie !'
);
```

---

## Exemple d'erreur

```php
$this->addFlash(
    'error',
    'Cet email est déjà utilisé.'
);
```

---

## Redirection

Les messages Flash sont souvent utilisés avant une redirection.

```php
$this->addFlash(
    'success',
    'Enregistrement effectué.'
);

return $this->redirectToRoute(
    'app_home'
);
```

---

## Afficher les messages dans Twig

```twig
{% raw %}
{% for message in app.flashes('success') %}
    <div class="alert alert-success">
        {{ message }}
    </div>
{% endfor %}
{% endraw %}
```

---

## Afficher les erreurs

```twig
{% raw %}
{% for message in app.flashes('error') %}
    <div class="alert alert-danger">
        {{ message }}
    </div>
{% endfor %}
{% endraw %}
```

---

## Types fréquents

```text
success
error
warning
info
```

---

## Comprendre le processus

```text
Action
↓
addFlash()
↓
Redirection
↓
Affichage du message
```

---

## Utilisation fréquente

```text
Inscription réussie
Modification effectuée
Suppression effectuée
Erreur de saisie
```

---

## Conclusion

Les messages Flash permettent d'informer l'utilisateur.

Méthode à retenir :

```php
addFlash()
```

Accès dans Twig :

```twig
app.flashes()
```
