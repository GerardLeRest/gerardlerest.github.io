---
title: "B - Comment ajouter un label"
date: 2025-06-17 17:46:00 +0800
categories: [cours]
tags: [python, pyside6]
---

## 1 Étapes simples :

Importer QLabel  
Créer un objet QLabel  
Lui donner un texte  
Lui donner un parent (ta fenêtre)

## 2 Voici un modèle de code :

```python
from PySide6.QtWidgets import QApplication, QWidget, QLabel
import sys

class Fenetre(QWidget):

    def __init__(self):
        super().__init__()
        self.initialisation()

    def initialisation(self):
        self.setWindowTitle("Fenêtre avec un Label")
        self.resize(400, 300)
        
        # Création du label
        label = QLabel("Bienvenue sur PySide !", self)
        label.move(50, 50)  # Position du label (x=50, y=50)

        self.show()

if __name__ == "__main__":
    app = QApplication(sys.argv)
    fenetre = Fenetre()
    app.exec()
```

Remarque:
```python
self.label.setText(message)
```
permet d'écrit la valeur de message dans le Label "label"
