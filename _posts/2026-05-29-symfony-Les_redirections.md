---
title: Symfony – Les redirections
author: Gérard LE REST
date: 2026-05-29 18:30:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Redirection, Route]
---

# Cours 5 — Les redirections

## Présentation

Une redirection permet d'envoyer automatiquement l'utilisateur vers une autre URL.

Au lieu d'afficher immédiatement une page, Symfony demande au navigateur d'aller consulter une nouvelle adresse.

Les redirections sont très utilisées après :

- une connexion ;
- une déconnexion ;
- un ajout en base de données ;
- une modification ;
- une suppression.

---

## Schéma général

```text
Contrôleur
    ↓
Redirection
    ↓
Nouvelle URL
    ↓
Nouvelle Route
    ↓
Nouveau Contrôleur
```

---

## 1. Redirection simple

```php
return $this->redirect('/accueil');
```

Ce code signifie :

```text
Va sur l'URL /accueil
```

---

## Ce qui se passe

```text
Utilisateur
    ↓
/connexion
    ↓
Contrôleur
    ↓
redirect('/accueil')
    ↓
/accueil
```

Le navigateur effectue une nouvelle requête.

---

## 2. Redirection vers une route

C'est la méthode recommandée.

```php
return $this->redirectToRoute('app_accueil');
```

---

## Pourquoi ?

Supposons :

```php
#[Route('/accueil', name: 'app_accueil')]
```

Si l'URL change plus tard :

```php
#[Route('/home', name: 'app_accueil')]
```

La redirection continue de fonctionner.

---

## Comment lire ce code ?

```php
redirectToRoute('app_accueil')
```

Signifie :

```text
Cherche la route app_accueil
et redirige vers son URL.
```

---

## 3. Redirection avec paramètre

Route :

```php
#[Route('/patient/{id}', name: 'patient_show')]
```

Redirection :

```php
return $this->redirectToRoute(
    'patient_show',
    [
        'id' => 25
    ]
);
```

Symfony génère :

```text
/patient/25
```

---

## Ce qui se passe

```text
Route patient_show
    ↓
id = 25
    ↓
/patient/25
```

---

## Exemple concret

Ajout d'un patient :

```php
public function ajouter()
{
    ...
    return $this->redirectToRoute(
        'patient_show',
        [
            'id' => $patient->getId()
        ]
    );
}
```

Après l'enregistrement :

```text
Création du patient
    ↓
Redirection
    ↓
Fiche du patient
```

---

## Pourquoi utiliser une redirection ?

Sans redirection :

```text
Utilisateur
    ↓
Actualise la page
    ↓
Le formulaire est envoyé une seconde fois
```

Avec redirection :

```text
Formulaire
    ↓
Sauvegarde
    ↓
Redirection
    ↓
Nouvelle page
```

Le risque de double enregistrement est réduit.

---

## À retenir

Une redirection :

- n'affiche pas directement une page ;
- demande au navigateur d'aller ailleurs ;
- est souvent utilisée après une modification de données.

Schéma mental :

```text
Action
 ↓
Redirection
 ↓
Nouvelle URL
 ↓
Nouvelle page
```

---

## Conclusion

Les redirections sont omniprésentes dans les applications Symfony.

Quand tu lis un contrôleur et que tu vois :

```php
return $this->redirectToRoute(...);
```

comprends immédiatement :

```text
Ce contrôleur n'affiche pas une page.
Il envoie l'utilisateur vers une autre route.
```
