---
title: Symfony – Créer une entité
author: Gérard LE REST
date: 2026-06-02 12:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, doctrine, entite]
---

# Cours 9 — Créer une entité

## Introduction

Une entité représente un objet métier de l'application.

Exemples :

- un patient ;
- un utilisateur ;
- un produit ;
- un article.

Une entité est généralement associée à une table de la base de données.

---

## Créer une entité

Commande :

```bash
php bin/console make:entity
```

Symfony demande ensuite :

```text
Class name of the entity to create:
```

Exemple :

```text
Patient
```

---

## Ajouter des propriétés

Symfony propose ensuite d'ajouter des propriétés.

Exemple :

```text
New property name:
```

```text
nom
```

Type :

```text
string
```

Puis :

```text
prenom
```

Type :

```text
string
```

---

## Résultat

Symfony crée le fichier :

```text
src/Entity/Patient.php
```

Exemple :

```php
#[ORM\Entity]
class Patient
{
    #[ORM\Id]
    #[ORM\GeneratedValue]
    #[ORM\Column]
    private ?int $id = null;

    #[ORM\Column(length: 255)]
    private ?string $nom = null;

    #[ORM\Column(length: 255)]
    private ?string $prenom = null;
}
```

---

## Les propriétés

Dans cette entité :

```php
private ?int $id = null;
private ?string $nom = null;
private ?string $prenom = null;
```

Chaque propriété correspond à une future colonne de la table.

---

## La clé primaire

```php
#[ORM\Id]
#[ORM\GeneratedValue]
#[ORM\Column]
private ?int $id = null;
```

Cette propriété représente l'identifiant unique de chaque enregistrement.

Symfony génère automatiquement sa valeur.

---

## Les méthodes Getter et Setter

Symfony génère automatiquement des méthodes.

Exemple :

```php
public function getNom(): ?string
{
    return $this->nom;
}

public function setNom(string $nom): static
{
    $this->nom = $nom;

    return $this;
}
```

Le getter permet de lire une valeur.

Le setter permet de modifier une valeur.

---

## Conclusion

Pour créer une entité :

- utiliser la commande `make:entity` ;
- choisir un nom de classe ;
- ajouter les propriétés ;
- laisser Symfony générer le fichier.

Une entité représente un objet métier et servira à stocker les données dans la base de données.
