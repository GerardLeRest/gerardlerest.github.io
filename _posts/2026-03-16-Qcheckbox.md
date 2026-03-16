---
title: Les QCheckBox
author: Gérard LE REST
date: 2026-03-16 14:00:00 +0800
categories: [Pyside6, Python, Cours]
tags: [QCheckBox]
---

# QCheckBox --- L'essentiel (PySide6)

👉 Case **à cocher / décocher**\
👉 Permet à l'utilisateur d'activer ou désactiver une option

------------------------------------------------------------------------

## ✅ Création

```python
case = QCheckBox("Option")
```

➡️ Crée une case à cocher avec un texte.

------------------------------------------------------------------------

## ✔️ Vérifier si la case est cochée

```python
case.isChecked()
```

➡️ Retourne :

- `True` si la case est cochée\
- `False` sinon

Exemple :

```python
if case.isChecked():
    print("option activée")
```

------------------------------------------------------------------------

## ✏️ Cocher / décocher par code

```python
case.setChecked(True)   # cocher
case.setChecked(False)  # décocher
```

➡️ Permet de modifier l'état de la case depuis le programme.

------------------------------------------------------------------------

## 🎯 Détecter un changement

```python
case.stateChanged.connect(ma_fonction)
```

➡️ Lance une action quand l'utilisateur coche ou décoche.

Exemple :

```python
def ma_fonction():
    print("changement")
```

------------------------------------------------------------------------

## 🔁 Exemple simple

```python
case = QCheckBox("Afficher photo")

def verifier():
    if case.isChecked():
        print("photo visible")
    else:
        print("photo cachée")

case.stateChanged.connect(verifier)
```

➡️ Le programme réagit lorsque l'utilisateur change l'état.

------------------------------------------------------------------------

## 📦 Dans un layout

```python
layout.addWidget(case)
```

➡️ Ajoute la case à cocher dans l'interface.

------------------------------------------------------------------------

## 📌 Résumé ultra-court

👉 `QCheckBox` = activer/désactiver une option

👉 `isChecked()` = lire l'état\
👉 Retourne `True` ou `False`

👉 `setChecked()` = modifier l'état\
👉 Permet de cocher ou décocher

👉 `stateChanged` = signal\
👉 Détecte un changement utilisateur

👉 Widget très utilisé pour **options, filtres et paramètres**.
