---
title: SQL - Les jointures
author: Gérard LE REST
date: 2026-06-22 11:00:00 +0200
categories: [Base de données, Cours]
tags: [sql, sqlite, mysql, jointure]
---

# SQL – Les jointures

## Pourquoi utiliser une jointure ?

Dans une base de données relationnelle, les informations sont souvent réparties dans plusieurs tables.

Exemple :

Table `eleves`

| id | nom |
|----|------|
| 1 | Dupont |
| 2 | Martin |

Table `notes`

| id | id_eleve | note |
|----|----------|------|
| 1 | 1 | 15 |
| 2 | 1 | 18 |
| 3 | 2 | 12 |

L'objectif est souvent d'afficher :

```text
Dupont | 15
Dupont | 18
Martin | 12
```

Pour cela, on utilise une jointure.

---

## Structure des tables

```sql
CREATE TABLE eleves (
    id INTEGER PRIMARY KEY,
    nom TEXT
);
```

```sql
CREATE TABLE notes (
    id INTEGER PRIMARY KEY,
    id_eleve INTEGER,
    note INTEGER
);
```

La colonne :

```sql
id_eleve
```

fait référence à :

```sql
eleves.id
```

---

## INNER JOIN

C'est la jointure la plus utilisée.

Elle affiche uniquement les lignes présentes dans les deux tables.

```sql
SELECT eleves.nom,
       notes.note
FROM eleves
INNER JOIN notes
ON eleves.id = notes.id_eleve;
```

Résultat :

```text
Dupont | 15
Dupont | 18
Martin | 12
```

---

## Utilisation d'alias

Pour simplifier l'écriture :

```sql
SELECT e.nom,
       n.note
FROM eleves e
INNER JOIN notes n
ON e.id = n.id_eleve;
```

Le résultat est identique.

---

## INNER JOIN avec condition

Afficher uniquement les notes supérieures ou égales à 15 :

```sql
SELECT e.nom,
       n.note
FROM eleves e
INNER JOIN notes n
ON e.id = n.id_eleve
WHERE n.note >= 15;
```

Résultat :

```text
Dupont | 15
Dupont | 18
```

---

## LEFT JOIN

Affiche toutes les lignes de la table de gauche.

Même si aucune correspondance n'existe dans la table de droite.

Table `eleves`

| id | nom |
|----|------|
| 1 | Dupont |
| 2 | Martin |
| 3 | Bernard |

Table `notes`

| id | id_eleve | note |
|----|----------|------|
| 1 | 1 | 15 |
| 2 | 2 | 12 |

Requête :

```sql
SELECT e.nom,
       n.note
FROM eleves e
LEFT JOIN notes n
ON e.id = n.id_eleve;
```

Résultat :

```text
Dupont  | 15
Martin  | 12
Bernard | NULL
```

Bernard apparaît même sans note.

---

## RIGHT JOIN

Affiche toutes les lignes de la table de droite.

```sql
SELECT e.nom,
       n.note
FROM eleves e
RIGHT JOIN notes n
ON e.id = n.id_eleve;
```

⚠️ SQLite ne supporte pas directement `RIGHT JOIN`.

Avec SQLite, on inverse généralement les tables et on utilise un `LEFT JOIN`.

---

## Jointure sur plusieurs colonnes

On peut utiliser plusieurs critères.

```sql
SELECT *
FROM table1 t1
INNER JOIN table2 t2
ON t1.id = t2.id
AND t1.code = t2.code;
```

---

## Jointure entre trois tables

Exemple :

Table `eleves`

Table `notes`

Table `matieres`

```sql
SELECT e.nom,
       m.nom_matiere,
       n.note
FROM notes n
INNER JOIN eleves e
ON e.id = n.id_eleve
INNER JOIN matieres m
ON m.id = n.id_matiere;
```

Résultat :

```text
Dupont | Maths   | 15
Dupont | Physique| 18
Martin | Maths   | 12
```

---

## Rechercher les élèves sans note

Grâce au LEFT JOIN :

```sql
SELECT e.nom
FROM eleves e
LEFT JOIN notes n
ON e.id = n.id_eleve
WHERE n.id IS NULL;
```

Résultat :

```text
Bernard
```

---

## Jointure et tri

```sql
SELECT e.nom,
       n.note
FROM eleves e
INNER JOIN notes n
ON e.id = n.id_eleve
ORDER BY e.nom;
```

---

## Jointure et agrégation

Calculer la moyenne des notes :

```sql
SELECT e.nom,
       AVG(n.note) AS moyenne
FROM eleves e
INNER JOIN notes n
ON e.id = n.id_eleve
GROUP BY e.nom;
```

Résultat :

```text
Dupont | 16.5
Martin | 12
```

---

## Schéma mental d'une jointure

```text
Table eleves

id | nom
-----------
1  | Dupont
2  | Martin

        ||
        ||
        \/

Table notes

id_eleve | note
----------------
1        | 15
1        | 18
2        | 12
```

La jointure relie :

```text
eleves.id
=
notes.id_eleve
```

---

## SQL depuis Python

```python
import sqlite3

connexion = sqlite3.connect("ecole.db")
curseur = connexion.cursor()

curseur.execute("""
    SELECT e.nom, n.note
    FROM eleves e
    INNER JOIN notes n
    ON e.id = n.id_eleve
""")

resultats = curseur.fetchall()

for ligne in resultats:
    print(ligne)

connexion.close()
```

---

## Bonnes pratiques

- Utiliser des clés primaires (`PRIMARY KEY`).
- Utiliser des clés étrangères (`FOREIGN KEY`).
- Toujours préciser la condition du `ON`.
- Utiliser des alias (`e`, `n`, `m`) pour simplifier les requêtes.
- Éviter les jointures inutiles sur de très grosses tables.

---

## À retenir

La jointure la plus utilisée est :

```sql
INNER JOIN
```

Syntaxe générale :

```sql
SELECT colonnes
FROM table1
INNER JOIN table2
ON table1.cle = table2.cle;
```

Les jointures permettent de relier les données réparties dans plusieurs tables et constituent l'un des mécanismes les plus importants des bases de données relationnelles.