---
title: Le QHBoxLayout
author: Gérard LE REST
date: 2026-01-20 18:13:00 +0800
categories: [Pyside6, Cours]
tags: [Label, Fenêtre]

---

## 1. Objectif

- Organiser des widgets côte à côte (horizontalement).

- Ne plus utiliser .move(x, y) à la main.
  
  ## 2. Syntaxe simple

```python
from PySide6.QtWidgets import QHBoxLayout
```

Ensuite :

- Créer un QHBoxLayout,

- Ajouter tes widgets dedans,

- L'appliquer à la fenêtre ou à une partie de la fenêtre.
  
  ## 3 Exemple simple

```python
from PySide6.QtWidgets import QApplication, QWidget, QPushButton, QHBoxLayout  
import sys

class Fenetre(QWidget):  
    def **init**(self):  
        super().**init**()  
        self.initialiser_fenetre()

    def initialiser_fenetre(self):
    self.setWindowTitle("Exemple avec QHBoxLayout")
    self.resize(400, 300)

    # Création du layout horizontal
    layout = QHBoxLayout()

    # Création des boutons
    bouton1 = QPushButton("Gauche")
    bouton2 = QPushButton("Centre")
    bouton3 = QPushButton("Droite")

    # Ajout des boutons au layout
    layout.addWidget(bouton1)
    layout.addWidget(bouton2)
    layout.addWidget(bouton3)

    # Appliquer le layout à la fenêtre
    self.setLayout(layout)

    self.show()

if **name** == "**main**":  
app = QApplication(sys.argv)  
fenetre = Fenetre()  
app.exec()
```

✅ Ce que fait ce code :

- Les trois boutons sont alignés de gauche à droite automatiquement.

- Ils bougent proprement si tu redimensionnes la fenêtre.
  
  ## 4 QVBoxLayout
  
  Pour aligner les éléments verticalement, on utilise QVBoxLayout