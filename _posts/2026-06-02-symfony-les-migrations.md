---
title: Symfony – Les migrations
author: Gérard LE REST
date: 2026-06-02 13:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, doctrine, migration]
---

# Cours 10 — Les migrations

## Introduction

Une migration permet de mettre à jour la structure de la base de données.

Après avoir créé ou modifié une entité, Symfony peut générer automatiquement les requêtes SQL nécessaires.

---

## Générer une migration

Commande :

```bash
php bin/console make:migration
```

Symfony compare les entités avec la base de données.

Il crée alors un fichier de migration.

---

## Résultat

Exemple :

```text
src/Migrations/Version20260602130000.php
```

Ce fichier contient les requêtes SQL permettant de mettre à jour la base de données.

---

## Exécuter une migration

Commande :

```bash
php bin/console doctrine:migrations:migrate
```

Symfony affiche alors un message de confirmation.

Répondre :

```text
yes
```

La base de données est mise à jour.

---

## Exemple

Entité :

```php
#[ORM\Column(length: 255)]
private ?string $nom = null;
```

Puis ajout d'une propriété :

```php
#[ORM\Column(length: 255)]
private ?string $prenom = null;
```

Génération de la migration :

```bash
php bin/console make:migration
```

Exécution :

```bash
php bin/console doctrine:migrations:migrate
```

La colonne `prenom` est ajoutée à la table.

---

## Modifier une entité

Après chaque modification d'une entité :

```php
private ?string $email = null;
```

il faut généralement exécuter :

```bash
php bin/console make:migration
```

puis :

```bash
php bin/console doctrine:migrations:migrate
```

---

## Conclusion

Pour mettre à jour la base de données :

1. modifier une entité ;
2. générer une migration ;
3. exécuter la migration.

Commandes à retenir :

```bash
php bin/console make:migration
```

```bash
php bin/console doctrine:migrations:migrate
```
