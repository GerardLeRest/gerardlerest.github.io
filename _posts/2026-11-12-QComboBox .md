---
title: Les QComboBox
author: Gérard LE REST
date: 2026-11-12 15:00:00 +0100
categories: [Pyside6, Python, Cours]
tags: [qcombobox]
---

# QComboBox --- L'essentiel (PySide6)

👉 Liste **déroulante** permettant de choisir un élément parmi plusieurs propositions.  
👉 Permet à l'utilisateur de sélectionner une valeur sans avoir à la saisir.

------------------------------------------------------------------------

## ✅ Création

```python
from PySide6.QtWidgets import QComboBox

combo = QComboBox()
```

➡️ Crée une liste déroulante initialement vide.

------------------------------------------------------------------------

## ➕ Ajouter des éléments

### Ajouter un seul élément

```python
combo.addItem("Classe TSTI1")
```

➡️ Ajoute un élément à la liste.

### Ajouter plusieurs éléments

```python
combo.addItems(["TSTI1", "TSTI2", "TSTI3"])
```

➡️ Ajoute plusieurs éléments en une seule instruction.

------------------------------------------------------------------------

## ✔️ Récupérer l'élément sélectionné

```python
combo.currentText()
```

➡️ Retourne le texte de l'élément actuellement sélectionné.

Exemple :

```python
classe = combo.currentText()
print(classe)
```

➡️ Affiche le nom de la classe sélectionnée.

------------------------------------------------------------------------

## 🔢 Récupérer l'indice de l'élément sélectionné

```python
combo.currentIndex()
```

➡️ Retourne la position de l'élément sélectionné.

Les indices commencent à **0**.

Exemple :

```python
combo.addItems(["TSTI1", "TSTI2", "TSTI3"])

print(combo.currentIndex())
```

➡️ Retourne `0` si le premier élément est sélectionné.

👉 Si aucun élément n'est sélectionné, retourne `-1`.

------------------------------------------------------------------------

## ✏️ Sélectionner un élément par code

### Par son indice

```python
combo.setCurrentIndex(1)
```

➡️ Sélectionne le deuxième élément.

### Par son texte

```python
combo.setCurrentText("TSTI2")
```

➡️ Sélectionne l'élément dont le texte correspond à `"TSTI2"`, s'il existe.

------------------------------------------------------------------------

## 🎯 Détecter un changement de sélection

```python
combo.currentTextChanged.connect(ma_fonction)
```

➡️ Déclenche une fonction lorsque le texte sélectionné change.

Exemple :

```python
def ma_fonction(classe):
    print("Classe sélectionnée :", classe)

combo.currentTextChanged.connect(ma_fonction)
```

👉 Le signal `currentTextChanged` transmet automatiquement le texte sélectionné à la fonction.

### Autre signal

```python
combo.currentIndexChanged.connect(ma_fonction)
```

➡️ Transmet l'indice de l'élément sélectionné.

👉 `currentTextChanged` : transmet le texte.  
👉 `currentIndexChanged` : transmet l'indice.

**Attention :** ces signaux peuvent également être émis lorsque la sélection est modifiée par le programme.

------------------------------------------------------------------------

## 🗑️ Supprimer des éléments

### Supprimer un élément

```python
combo.removeItem(0)
```

➡️ Supprime le premier élément.

### Vider complètement la liste

```python
combo.clear()
```

➡️ Supprime tous les éléments.

------------------------------------------------------------------------

## 🔍 Rechercher un élément

```python
indice = combo.findText("TSTI2")
```

➡️ Retourne l'indice de l'élément recherché.

👉 Retourne `-1` si l'élément n'existe pas.

------------------------------------------------------------------------

## 🔢 Connaître le nombre d'éléments

```python
nombre = combo.count()
```

➡️ Retourne le nombre d'éléments présents dans la liste.

------------------------------------------------------------------------

## 📏 Définir la hauteur

```python
combo.setMinimumHeight(32)
```

➡️ Définit une hauteur minimale de **32 pixels** pour le widget.

👉 Cette instruction concerne la partie visible de la ComboBox, et non la hauteur de la liste déroulante.

------------------------------------------------------------------------

## 🔁 Exemple simple

```python
combo = QComboBox()

combo.addItems(["TSTI1", "TSTI2", "TSTI3"])

def choisir_classe(classe):
    print("Classe choisie :", classe)

combo.currentTextChanged.connect(choisir_classe)
```

➡️ Lorsque l'utilisateur sélectionne une autre classe, la fonction `choisir_classe()` est appelée.

👉 Le nom de la classe est transmis automatiquement à la fonction.

------------------------------------------------------------------------

## 📦 Dans un layout

```python
layout.addWidget(combo)
```

➡️ Ajoute la liste déroulante dans l'interface.

------------------------------------------------------------------------

## 📌 Résumé ultra-court

👉 `QComboBox` = liste déroulante

👉 `addItem()` = ajouter un élément  
👉 `addItems()` = ajouter plusieurs éléments

👉 `currentText()` = récupérer le texte sélectionné

👉 `currentIndex()` = récupérer l'indice sélectionné

👉 `setCurrentIndex()` = sélectionner par indice

👉 `setCurrentText()` = sélectionner par texte

👉 `currentTextChanged` = signal  
👉 Détecte un changement du texte sélectionné

👉 `currentIndexChanged` = signal  
👉 Détecte un changement d'indice

👉 `clear()` = vider la liste

👉 `count()` = compter les éléments

👉 `setMinimumHeight()` = définir une hauteur minimale

👉 Widget très utilisé pour **choisir une classe, une catégorie, un mode ou une option**.