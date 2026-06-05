---
title: CSV et Python
author: Gérard LE REST
date: 2026-04-20 16:00:00 +0800
categories: [CSV, Python, Cours]
tags: [csv, python]
---

# 📄 CSV et Python – L’essentiel

## 🔹 Qu’est-ce qu’un CSV ?

Un fichier CSV est un **fichier texte** contenant des données sous forme de tableau.

➡️ Une ligne = un enregistrement  
➡️ Valeurs séparées par `;` (souvent en France)

Exemple :

```csv
prenom;nom;age
Jean;Dupont;18
```

---

## 🔹 Lire un fichier CSV

```python
import csv

with open("eleves.csv", newline='', encoding="utf-8") as f:
    lecteur = csv.reader(f, delimiter=';')

    for ligne in lecteur:
        print(ligne)
```

➡️ Chaque ligne = une **liste**

---

## 🔹 Ignorer l’en-tête

```python
next(lecteur)
```

---

## 🔹 Récupérer les valeurs

```python
for ligne in lecteur:
    prenom, nom, age = ligne
```

---

## 🔹 Conversion des types

```python
age = int(age)
```

➡️ Important : tout est lu en **texte**

---

## 🔹 Lire avec des noms de colonnes

```python
lecteur = csv.DictReader(f, delimiter=';')

for ligne in lecteur:
    print(ligne["prenom"])
```

➡️ Chaque ligne = **dictionnaire**

---

## 🔹 Écrire dans un CSV

```python
import csv

with open("eleves.csv", "w", newline='', encoding="utf-8") as f:
    writer = csv.writer(f, delimiter=';')

    writer.writerow(["prenom", "nom", "age"])
    writer.writerow(["Jean", "Dupont", 18])
```

---

## 🔹 Ajouter une ligne

```python
with open("eleves.csv", "a", newline='', encoding="utf-8") as f:
    writer = csv.writer(f, delimiter=';')
    writer.writerow(["Paul", "Durand", 16])
```

---

## 🔹 Points importants ⭐

- Toujours :
  - `encoding="utf-8"`
  - `newline=''`
  - `delimiter=';'`
- Utiliser `next()` pour ignorer l’en-tête
- Convertir les nombres (`int`, `float`)
- `reader` → listes  
- `DictReader` → dictionnaires (plus lisible)

---

## 🔹 À retenir

- CSV = **simple et universel**
- Python → module `csv` intégré
- Sert souvent à :
  - importer dans SQLite
  - alimenter une application
  - échanger des données
