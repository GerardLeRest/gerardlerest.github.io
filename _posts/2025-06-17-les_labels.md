 ---

 title: "Créer une fenêtre vide"
 date: 2025-06-17
 categories: [cours]
 tags: [Python, pyside6]

## 1. Objectif

- Créer une fenêtre **vide** (sans texte ni bouton pour l’instant).
- Utiliser une **classe** pour organiser ton code.
- Lancer proprement l’application.

## 2. Structure de base

- **Importer** les modules nécessaires (`QApplication`, `QWidget`, `sys`).
- **Créer une classe** qui hérite de `QWidget`.
- **Initialiser** la fenêtre (titre, taille)
- **Afficher** la fenêtre avec `show()`.
- **Lancer** l’application avec `app.exec()`.

## 3. Code complet

```python
from PySide6.QtWidgets import QApplication, QWidget  
import sys

class Fenetre(QWidget):  
    def __init__(self):  
        super().__init__()  
        self.initialiser_fenetre()

    def initialiser_fenetre(self):  
        self.setWindowTitle("Fenêtre vide")  
        self.resize(400, 300)  
        self.show()

if __name__ == "__main__":  
  app = QApplication(sys.argv)  
  fenetre = Fenetre()  
  app.exec()
```
