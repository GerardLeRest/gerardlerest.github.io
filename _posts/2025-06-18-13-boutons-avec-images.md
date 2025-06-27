---
title: "13 - Boutons avec images"
date: 2025-06-17 20:33:05 +0800
categories: [cours]
tags: [python, pyside6]
---

## Introduction

Dans PySide6, on peut créer des boutons graphiques contenant une **image seule**, ou une **image avec du texte**.  
Le widget utilisé est `QPushButton`, auquel on peut associer une image via `QIcon`.

---

## Méthode 1 : Bouton avec une image seule

```python
from PySide6.QtWidgets import QApplication, QPushButton, QWidget, QVBoxLayout
from PySide6.QtGui import QIcon
import sys

class Fenetre(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Bouton avec image")

        bouton = QPushButton()
        bouton.setIcon(QIcon("chemin/vers/image.png"))
        bouton.setIconSize(QSize(64, 64))  # taille d'affichage de l'image
        bouton.setFixedSize(80, 80)        # taille du bouton (optionnel)

        layout = QVBoxLayout()
        layout.addWidget(bouton)
        self.setLayout(layout)

if __name__ == "__main__":
    app = QApplication(sys.argv)
    fen = Fenetre()
    fen.show()
    app.exec()
    fichiers/photos/1S1/Fernandez_Sarah.jpg
```

## Méthode 2 : Bouton avec texte et image

## Méthode 3 : Image comme fond de bouton (CSS)
