---
title: "4 - Faire agir un bouton"
date: 2025-06-17 12:50:00 +0000
categories: [cours]
tags: [python, pyside6]
---

## 1. Objectif

- Ajouter un bouton dans ta fenêtre.
- Faire en sorte que quand on clique sur le bouton, la fenêtre se ferme.

## 2. Introduction rapide aux signaux et slots

En PySide (et Qt en général) :

- Quand tu cliques sur un bouton, il émet un "signal".
- Ce "signal" peut être connecté à une fonction qui fait quelque chose (= le "slot").

Par exemple :

- Le bouton émet le signal clicked.
- On connecte ce signal à la méthode close() de la fenêtre.
- Résultat : quand tu cliques, la fenêtre se ferme.

## 3. Code complet (exemple simple)

```python
from PySide6.QtWidgets import QApplication, QWidget, QPushButton
import sys

class Fenetre(QWidget):
    def __init__(self):
        super().__init__()
        self.initialiser_fenetre()

    def initialiser_fenetre(self):
        self.setWindowTitle("Fenêtre avec bouton actif")
        self.resize(400, 300)

        # Création du bouton
        bouton = QPushButton("Fermer la fenêtre", self)
        bouton.move(130, 130)

        # Connexion du signal "clic" du bouton à la méthode "close"
        bouton.clicked.connect(self.close)

        self.show()

if __name__ == "__main__":
    app = QApplication(sys.argv)
    fenetre = Fenetre()
    app.exec()
```
