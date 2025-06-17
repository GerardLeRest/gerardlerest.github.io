---
title: "C - Ajouter un bouton"
date: 2025-06-17 14:00:00 +0000
categories: [cours]
tags: [python, pyside6]

---

## 1. Objectif

- Ajouter un bouton (QPushButton) dans ta fenêtre.
- Comprendre comment créer un bouton et comment le positionner.

## 2. Étapes

- Importer QPushButton en plus de QApplication et QWidget.
- Créer le bouton dans ta fenêtre.
- Donner un texte au bouton (exemple : "Cliquez-moi !").
- Positionner le bouton dans la fenêtre avec move(x, y).
- Afficher la fenêtre comme avant.

## 3. Code complet (exemple simple)

```python
from PySide6.QtWidgets import QApplication, QWidget, QPushButton
import sys

class Fenetre(QWidget):
    def __init__(self):
        super().__init__()
        self.initialiser_fenetre()

    def initialiser_fenetre(self):
        self.setWindowTitle("Fenêtre avec un bouton")
        self.resize(400, 300)

        # Création du bouton
        bouton = QPushButton("Cliquez-moi !", self)
        bouton.move(150, 130)  # Position du bouton (x=150, y=130)

        self.show()

if __name__ == "__main__":
    app = QApplication(sys.argv)
    fenetre = Fenetre()
    app.exec()
```

### ✅ Ce que fait ce code :

- Crée une fenêtre 400x300.
- Ajoute un bouton "Cliquez-moi !" centré approximativement dans la fenêtre.
- Le bouton n’a pas encore d’action → il est juste affiché.
