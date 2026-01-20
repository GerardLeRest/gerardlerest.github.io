---
title: Combiner plusieurs Layouts
author: Gérard LE REST
date: 2026-01-20 17:52:00 +0800
categories: [Pyside6, Cours]
tags: [Label, Fenêtre]

---

# Combiner plusieurs Layouts

## 1. Pourquoi combiner les Layouts ?

✅ Pour créer des interfaces complexes mais bien organisées :

- Un morceau vertical,

- Un morceau horizontal,

- Et tout ça qui s’adapte automatiquement à la fenêtre.  
  ✅ C’est comme construire un meuble :

- Une étagère verticale,  

- Avec des tiroirs horizontaux à l’intérieur.
  
  ## 2. Principe simple

- Tu crées un layout principal (QVBoxLayout par exemple).

- Tu crées des sous-layouts (QHBoxLayout par exemple).

- Tu ajoutes les sous-layouts dans le layout principal.
  
  ## 3.  Exemple clair

```python
from PySide6.QtWidgets import QApplication, QWidget, QPushButton, QVBoxLayout, QHBoxLayout
import sys

class Fenetre(QWidget):
    def __init__(self):
        super().__init__()
        self.initialiser_fenetre()

    def initialiser_fenetre(self):
        self.setWindowTitle("Combinaison de Layouts")
        self.resize(400, 300)

        # Layout principal vertical
        layout_principal = QVBoxLayout()

        # Bouton en haut
        bouton_haut = QPushButton("Haut")
        layout_principal.addWidget(bouton_haut)

        # Layout horizontal au milieu
        layout_horizontal = QHBoxLayout()
        bouton_gauche = QPushButton("Gauche")
        bouton_droite = QPushButton("Droite")
        layout_horizontal.addWidget(bouton_gauche)
        layout_horizontal.addWidget(bouton_droite)

        # Ajouter le layout horizontal au layout principal
        layout_principal.addLayout(layout_horizontal)

        # Bouton en bas
        bouton_bas = QPushButton("Bas")
        layout_principal.addWidget(bouton_bas)

        # Appliquer le layout principal à la fenêtre
        self.setLayout(layout_principal)

        self.show()

if __name__ == "__main__":
    app = QApplication(sys.argv)
    fenetre = Fenetre()
    app.exec()
```
