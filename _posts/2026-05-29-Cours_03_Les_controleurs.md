---
title: Symfony – Les contrôleurs
author: Gérard LE REST
date: 2026-05-29 17:30:00 +0800
categories: [Symfony, Cours]
tags: [Symfony, Contrôleur, Backend]
---

# Cours 3 — Les contrôleurs

## Présentation

Un contrôleur est une méthode PHP appelée par Symfony lorsqu'une route correspond à l'URL demandée.

La route répond à la question :

```text
Quelle URL est demandée ?
```

Le contrôleur répond à la question :

```text
Que faut-il faire quand cette URL est demandée ?
```

---

## Schéma général

```text
Navigateur
    ↓
URL
    ↓
Route
    ↓
Contrôleur
    ↓
Réponse
```

---

## 1. Contrôleur très simple

```php
#[Route('/bonjour', name: 'app_bonjour')]
public function bonjour(): Response
{
    return new Response('Bonjour');
}
```

URL :

```text
/bonjour
```

Résultat :

```text
Bonjour
```

---

## Comment lire ce code ?

```php
public function bonjour(): Response
```

Signifie :

```text
La méthode s'appelle bonjour.
Elle renvoie obligatoirement une réponse HTTP.
```

La réponse est ici :

```php
return new Response('Bonjour');
```

Symfony renvoie donc le texte `Bonjour` au navigateur.

---

## 2. Contrôleur avec paramètre

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

## Ce que fait Symfony

Symfony transforme l'URL :

```text
/patient/12
```

en appel de méthode :

```php
show(12)
```

Le contrôleur reçoit donc directement la valeur.

---

## 3. Contrôleur qui affiche une vue Twig

Dans un vrai projet Symfony, le contrôleur ne renvoie pas toujours du texte brut.

Il renvoie souvent une page HTML grâce à Twig.

```php
#[Route('/accueil', name: 'app_accueil')]
public function accueil(): Response
{
    return $this->render('accueil/index.html.twig');
}
```

Résultat :

```text
Symfony affiche le fichier Twig accueil/index.html.twig
```

---

## 4. Contrôleur qui transmet des données à Twig

```php
#[Route('/patient/{id}', name: 'patient_show')]
public function show(int $id): Response
{
    return $this->render('patient/show.html.twig', [
        'id' => $id,
    ]);
}
```

Dans Twig, on pourra écrire :

```twig
{{ id }}
```

URL :

```text
/patient/12
```

Résultat affiché dans la page :

```text
12
```

---

## Comment lire ce tableau ?

```php
[
    'id' => $id,
]
```

Signifie :

```text
Je donne à Twig une variable appelée id.
Sa valeur est celle de la variable PHP $id.
```

---

## 5. Contrôleur avec Repository

Dans un projet comme SoigneMoi, le contrôleur doit souvent récupérer des données dans la base.

Exemple :

```php
#[Route('/patient/{id}', name: 'patient_show')]
public function show(int $id, PatientRepository $patientRepository): Response
{
    $patient = $patientRepository->find($id);

    return $this->render('patient/show.html.twig', [
        'patient' => $patient,
    ]);
}
```

---

## Comment lire ce code ?

```php
PatientRepository $patientRepository
```

Signifie :

```text
Symfony fournit automatiquement un objet PatientRepository au contrôleur.
```

Puis :

```php
$patient = $patientRepository->find($id);
```

Signifie :

```text
Je cherche dans la base de données le patient dont l'identifiant vaut $id.
```

Enfin :

```php
'patient' => $patient
```

Signifie :

```text
Je transmets l'objet Patient à Twig.
```

---

## Exemple inspiré de SoigneMoi

Imaginons l'URL :

```text
/patient/25
```

Symfony suit ce chemin :

```text
/patient/25
    ↓
Route /patient/{id}
    ↓
id = 25
    ↓
PatientController::show(25)
    ↓
PatientRepository->find(25)
    ↓
patient/show.html.twig
```

Le contrôleur sert donc de pont entre :

```text
URL
 ↓
Données
 ↓
Vue Twig
```

---

## Ce que Symfony fait automatiquement

Symfony :

- trouve la route ;
- appelle la bonne méthode ;
- transmet les paramètres de route ;
- fournit certains objets comme les repositories ;
- transforme la réponse PHP en réponse HTTP.

---

## Ce que le développeur écrit

Le développeur écrit :

- la méthode du contrôleur ;
- les paramètres nécessaires ;
- les appels aux repositories ;
- le choix du template Twig ;
- les variables transmises à Twig.

---

## À retenir

Un contrôleur :

- est appelé par une route ;
- contient le code à exécuter ;
- prépare les données ;
- renvoie une réponse ;
- sert souvent de lien entre Doctrine et Twig.

Schéma mental :

```text
Route
 ↓
Contrôleur
 ↓
Données
 ↓
Twig
 ↓
Réponse HTML
```

---

## Erreurs fréquentes

### Oublier le type Response

Incorrect :

```php
public function accueil()
```

Correct :

```php
public function accueil(): Response
```

---

### Oublier le return

Incorrect :

```php
public function accueil(): Response
{
    $this->render('accueil/index.html.twig');
}
```

Correct :

```php
public function accueil(): Response
{
    return $this->render('accueil/index.html.twig');
}
```

---

### Confondre variable PHP et variable Twig

PHP :

```php
'patient' => $patient
```

Twig :

```twig
{{ patient.nom }}
```

La variable Twig s'appelle `patient`, pas `$patient`.

---

## Conclusion

Le contrôleur est le cœur du passage entre l'URL et la réponse.

Quand tu lis un projet Symfony comme SoigneMoi, le contrôleur permet de comprendre :

- quelle page est appelée ;
- quelles données sont récupérées ;
- quel template Twig est utilisé ;
- quelles variables sont envoyées à la vue.

C'est donc l'un des premiers fichiers à lire pour comprendre le fonctionnement réel d'une application Symfony.
