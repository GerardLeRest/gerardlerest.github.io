---
title: Les dictionnaires - Python
author: Gérard LE REST
date: 2025-12-28 18:49:00 +0800
categories: [Python, Cours]
tags: [dictionnaire, Json]
---

# 📘 PySide6 — Les menus avec QMenu (cours clair et structuré)

Ce cours explique **simplement** comment fonctionnent les menus en PySide6,
en utilisant **explicitement `QMenu`**, sans raccourcis peu lisibles.

---

# 📘 Dictionnaire Python (dict)

Ce document explique simplement ce qu’est un dictionnaire en Python,
comment l’utiliser, et dans quels cas il est pertinent.

---

## 1. Définition

Un **dictionnaire** (`dict`) est une structure de données qui associe :

clé → valeur

Chaque clé permet de retrouver rapidement une valeur.

---

## 2. Création d’un dictionnaire

### Dictionnaire vide

```python
d = {}
```

### Dictionnaire avec une valeur

```python
config_langue = {
    "langueSelectionnee": "fr"
}
```

---

## 3. Accéder à une valeur

### Accès direct (à éviter si la clé peut manquer)

```python
langue = config_langue["langueSelectionnee"]
```

### Accès sécurisé (recommandé)

```python
langue = config_langue.get("langueSelectionnee", "fr")
```

---

## 4. Modifier ou ajouter une valeur

```python
config_langue["langueSelectionnee"] = "en"
```

---

## 5. Supprimer une clé

```python
config_langue.pop("langueSelectionnee", None)
```

---

## 6. Tester si une clé existe

```python
if "langueSelectionnee" in config_langue:
    print("clé présente")
```

---

## 7. Parcourir un dictionnaire

```python
for cle, valeur in config_langue.items():
    print(cle, valeur)
```

---

## 8. Dictionnaire et JSON

JSON :

```json
{
  "langueSelectionnee": "fr"
}
```

Python :

```python
import json

with open("configurationLangue.json", "r", encoding="utf-8") as f:
    config_langue = json.load(f)
```

---

## 9. Cas d’usage : table de correspondance

```python
UI_VALUES = {
    "parlement": "Parlement",
    "entreprise": "Entreprise",
    "lycee": "Lycée"
}
```

---

## 10. À retenir

- `{}` crée un dictionnaire
- clé → valeur
- `.get()` évite les erreurs
- JSON `{}` → dict Python
