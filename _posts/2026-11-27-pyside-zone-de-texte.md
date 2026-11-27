---
title: Zone de texte
author: Gérard LE REST
date: 2026-11-27 15:35:00 +0100
categories: [Pyside6, Python, Cours]
tags: [qlineedit, qtextedit, qplaintextedit, fenetre]

---

# Comment insérer une zone de texte

## 1 Les différents types de zones de texte

PySide6 propose trois principaux widgets :

| Widget           | Utilisation                                   |
| ---------------- | --------------------------------------------- |
| `QLineEdit`      | Saisie de texte sur une seule ligne           |
| `QTextEdit`      | Saisie de texte multiligne avec mise en forme |
| `QPlainTextEdit` | Saisie de texte multiligne sans mise en forme |

## 2 Étapes simples

- Importer le widget souhaité.
- Créer un objet.
- Lui donner un parent (la fenêtre).
- Définir sa position et ses dimensions.
- Éventuellement, lui donner un texte initial.

## 3 Voici un modèle de code

```python
from PySide6.QtWidgets import (
    QApplication, QWidget, QLineEdit,
    QTextEdit, QPlainTextEdit
)
import sys


class Fenetre(QWidget):

    def __init__(self):
        super().__init__()
        self.initialisation()

    def initialisation(self):
        self.setWindowTitle("Zones de texte")
        self.resize(500, 400)

        # Zone de texte sur une seule ligne
        self.nom = QLineEdit(self)
        self.nom.setGeometry(50, 20, 400, 30)
        self.nom.setPlaceholderText("Saisir un nom")

        # Zone de texte multiligne
        self.description = QTextEdit(self)
        self.description.setGeometry(50, 70, 400, 130)

        # Zone de texte multiligne sans mise en forme
        self.appreciation = QPlainTextEdit(self)
        self.appreciation.setGeometry(50, 220, 400, 130)

        self.show()


if __name__ == "__main__":
    app = QApplication(sys.argv)
    fenetre = Fenetre()
    app.exec()
```

## 4 Écrire dans une zone de texte

**QLineEdit :**

```python
self.nom.setText("Dupont")
```

**QTextEdit et QPlainTextEdit :**

```python
self.description.setPlainText("Un élève sérieux.")
self.appreciation.setPlainText("Très bon trimestre.")
```

## 5 Récupérer le contenu d'une zone de texte

**QLineEdit :**

```python
nom = self.nom.text()
```

**QTextEdit et QPlainTextEdit :**

```python
description = self.description.toPlainText()
appreciation = self.appreciation.toPlainText()
```

## 6 Quelques méthodes utiles

| Méthode                       | Fonction                       |
| ----------------------------- | ------------------------------ |
| `clear()`                     | Effacer le contenu             |
| `setReadOnly(True)`           | Interdire la modification      |
| `setReadOnly(False)`          | Autoriser la modification      |
| `setPlaceholderText("Texte")` | Afficher un texte indicatif    |
| `setFocus()`                  | Placer le curseur dans la zone |
| `setEnabled(False)`           | Désactiver la zone             |
| `setEnabled(True)`            | Activer la zone                |

## 7 Détecter une modification du texte

Les trois widgets disposent du signal `textChanged`.

```python
self.appreciation.textChanged.connect(self.modification)
```

La méthode appelée :

```python
def modification(self):
    texte = self.appreciation.toPlainText()
    print(texte)
```

Remarque : pour `QLineEdit`, le signal `textChanged`
transmet également le nouveau texte.

```python
self.nom.textChanged.connect(self.modification_nom)
```

```python
def modification_nom(self, texte):
    print(texte)
```

## 8 Ajouter du texte sans effacer le contenu précédent

**QLineEdit :**

```python
self.nom.insert(" Dupont")
```

Le texte est inséré à la position du curseur.

**QTextEdit :**

```python
self.description.append("Nouvelle ligne")
```

**QPlainTextEdit :**

```python
self.appreciation.appendPlainText("Nouvelle ligne")
```

## 9 Afficher du texte avec une mise en forme

Cette possibilité est offerte par `QTextEdit`.

```python
self.description.setHtml("<b>Très bon trimestre.</b>")
```

Pour récupérer le contenu au format HTML :

```python
texte = self.description.toHtml()
```

## 10 Quel widget choisir ?

- `QLineEdit` : nom, prénom, adresse électronique...
- `QPlainTextEdit` : commentaire, appréciation, bilan...
- `QTextEdit` : texte nécessitant une mise en forme.
