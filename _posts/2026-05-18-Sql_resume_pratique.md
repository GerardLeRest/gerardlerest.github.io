---
title: SQL
author: Gérard LE REST
date: 2026-05-18 11:00:00 +0200
categories: [Base de données, Cours]
tags: [sql, sqlite, mysql]
---

# SQL – Résumé pratique (usage courant)

## Qu’est-ce que SQL ?

**SQL (Structured Query Language)** est le langage utilisé pour :

- créer des bases de données

- créer des tables

- ajouter des données

- modifier des données

- supprimer des données

- effectuer des recherches

➡️ Utilisé avec SQLite, MySQL, PostgreSQL, MariaDB...

---

## Une table SQL

Exemple d'une table élèves :

| id  | nom    | prenom | age |
| --- | ------ | ------ | --- |
| 1   | Dupont | Paul   | 18  |
| 2   | Martin | Sophie | 17  |

---

## Création d'une table

```sql
CREATE TABLE eleves (
    id INTEGER PRIMARY KEY,
    nom TEXT,
    prenom TEXT,
    age INTEGER
);
```

---

## Insertion d'une ligne

```sql
INSERT INTO eleves (nom, prenom, age)
VALUES ('Dupont', 'Paul', 18);
```

---

## Afficher toutes les données

```sql
SELECT * FROM eleves;
```

Résultat :

```text
1 | Dupont | Paul | 18
```

---

## Afficher certaines colonnes

```sql
SELECT nom, prenom
FROM eleves;
```

---

## Rechercher une ligne

```sql
SELECT *
FROM eleves
WHERE nom = 'Dupont';
```

---

## Utilisation des opérateurs

```sql
SELECT *
FROM eleves
WHERE age > 18;
```

Opérateurs courants :

| Opérateur | Signification     |
| --------- | ----------------- |
| =         | égal              |
| <>        | différent         |
| >         | supérieur         |
| <         | inférieur         |
| >=        | supérieur ou égal |
| <=        | inférieur ou égal |

---

## Trier les résultats

Par ordre croissant :

```sql
SELECT *
FROM eleves
ORDER BY nom;
```

Par ordre décroissant :

```sql
SELECT *
FROM eleves
ORDER BY nom DESC;
```

---

## Modifier une donnée

```sql
UPDATE eleves
SET age = 19
WHERE id = 1;
```

⚠️ Toujours utiliser un `WHERE` lorsque c'est nécessaire.

---

## Supprimer une ligne

```sql
DELETE FROM eleves
WHERE id = 1;
```

---

## Supprimer toutes les lignes

```sql
DELETE FROM eleves;
```

⚠️ La structure de la table reste présente.

---

## Supprimer une table

```sql
DROP TABLE eleves;
```

⚠️ La table et toutes ses données sont supprimées.

---

## Compter des lignes

```sql
SELECT COUNT(*)
FROM eleves;
```

---

## Rechercher avec LIKE

Commence par "Du" :

```sql
SELECT *
FROM eleves
WHERE nom LIKE 'Du%';
```

Contient "ont" :

```sql
SELECT *
FROM eleves
WHERE nom LIKE '%ont%';
```

---

## Limiter le nombre de résultats

```sql
SELECT *
FROM eleves
LIMIT 10;
```

---

## Valeurs NULL

Rechercher les lignes sans âge :

```sql
SELECT *
FROM eleves
WHERE age IS NULL;
```

---

## SQL depuis Python (SQLite)

```python
import sqlite3

connexion = sqlite3.connect("eleves.db")
curseur = connexion.cursor()

curseur.execute("""
    SELECT nom, prenom
    FROM eleves
""")

resultats = curseur.fetchall()

for eleve in resultats:
    print(eleve)

connexion.close()
```

---

## Bonnes pratiques

- Toujours sauvegarder avant des suppressions importantes.

- Utiliser des clés primaires (`PRIMARY KEY`).

- Éviter `SELECT *` dans les gros projets.

- Utiliser des requêtes paramétrées en Python.

- Toujours fermer la connexion à la base de données.

---

## Requêtes paramétrées (recommandé)

```python
nom = "Dupont"

curseur.execute(
    "SELECT * FROM eleves WHERE nom = ?",
    (nom,)
)
```

➡️ Évite les injections SQL.

---

## À retenir

> SQL permet de créer, rechercher, modifier et supprimer des données dans une base de données relationnelle.

Les quatre commandes fondamentales sont :

```sql
SELECT
INSERT
UPDATE
DELETE
```

Elles constituent la base de la majorité des applications utilisant une base de données.
