---
title: Symfony – Les relations ManyToMany
author: Gérard LE REST
date: 2026-06-02 17:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, doctrine, relation]
---

# Cours 18 — Les relations ManyToMany

## Introduction

Une relation ManyToMany permet de relier plusieurs objets entre eux.

Exemple :

```text
Médecin
↕
Spécialité
```

Un médecin peut avoir plusieurs spécialités.

Une spécialité peut concerner plusieurs médecins.

---

## Créer la relation

Commande :

```bash
php bin/console make:entity
```

Puis :

```text
New property name:
```

Exemple :

```text
specialites
```

Type :

```text
relation
```

Puis :

```text
ManyToMany
```

---

## Exemple

```php
#[ORM\ManyToMany(targetEntity: Specialite::class)]
private Collection $specialites;
```

---

## Ajouter un objet

```php
$medecin->addSpecialite($specialite);
```

---

## Supprimer un objet

```php
$medecin->removeSpecialite($specialite);
```

---

## Lire la relation

```php
$specialites = $medecin->getSpecialites();
```

Résultat :

```text
Collection de spécialités.
```

---

## Parcourir les résultats

```php
foreach ($specialites as $specialite) {
    echo $specialite->getLibelle();
}
```

---

## Comprendre le schéma

```text
Médecin 1
    ↕
Cardiologie

Médecin 1
    ↕
Médecine générale

Médecin 2
    ↕
Cardiologie
```

---

## Conclusion

Une relation ManyToMany permet :

- plusieurs objets vers plusieurs objets ;
- l'ajout avec `add...()` ;
- la suppression avec `remove...()` ;
- la lecture avec `get...()`.

Doctrine crée automatiquement la table de liaison nécessaire.
