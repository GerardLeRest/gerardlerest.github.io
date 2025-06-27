---
title: "10 - Récupérer un champs avec un bouton"
date: 2025-06-17 17:46:00 +0800
categories: [cours]
tags: [python, pyside6]
---

## 1. Récupérer le texte d’un champ

✅ Chaque QLineEdit a une méthode simple :

```python
texte = mon_champ.text()
```

text() permet de lire ce que l’utilisateur a écrit.

## 2. Connecter un bouton pour lire le texte

✅ Quand tu crées ton bouton, tu connectes son clic à une méthode :

```python
mon_bouton.clicked.connect(self.ma_methode)
```

Dans la méthode, tu utilises .text() pour récupérer le texte.

## 3. Exemple minimal complet

```python
from PySide6.QtWidgets import QApplication, QWidget, QPushButton, QLineEdit, QVBoxLayout
import sys

class Fenetre(QWidget):
    def __init__(self):
        super().__init__()
        self.initialiser_fenetre()

    def initialiser_fenetre(self):
        self.setWindowTitle("Récupérer un champ texte")
        self.resize(400, 200)

        layout = QVBoxLayout()

        # Créer un champ texte
        self.champ = QLineEdit()
        self.champ.setPlaceholderText("Tapez quelque chose...")

        # Créer un bouton
        bouton = QPushButton("Valider")
        bouton.clicked.connect(self.afficher_texte)

        layout.addWidget(self.champ)
        layout.addWidget(bouton)

        self.setLayout(layout)
        self.show()

    def afficher_texte(self):
        # Récupérer le texte du champ
        texte = self.champ.text()
        print("Texte saisi :", texte)

if __name__ == "__main__":
    app = QApplication(sys.argv)
    fenetre = Fenetre()
    app.exec()
```

✅ Ce que ce programme fait :

- Tu écris du texte dans le champ.
- Tu cliques sur "Valider".
- Le texte tapé est affiché dans la console.
