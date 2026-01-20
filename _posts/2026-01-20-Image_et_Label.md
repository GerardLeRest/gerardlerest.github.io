---
title: Image et Label
author: Gérard LE REST
date: 2026-01-20 17:47:00 +0800
categories: [Pyside6, Cours]
tags: [Label, Image]
---

# Comment insérer une image dans un QLabel

## 1. Importer ce qu’il faut

Tu dois utiliser :

- QLabel (normal, pour afficher du texte ou une image),

- QPixmap (spécial pour charger une image).
  
  ```python
  from PySide6.QtWidgets import QLabel
  from PySide6.QtGui import QPixmap
  ```

## 2. Code de base

Voici le minimum pour afficher une image :

```python
self.label_image = QLabel(self)  # Création du label vide
pixmap = QPixmap("chemin/vers/ton_image.png")  # Chargement de l'image
self.label_image.setPixmap(pixmap)  # Mettre l'image dans le label
self.label_image.move(100, 100)  # (facultatif) Positionner le label
```

✅ Attention :

- Le chemin vers l’image doit être correct (relatif ou absolu).

- L'image sera affichée dans le label.

- Le label prendra automatiquement la taille de l'image sauf si tu forces une taille différente.
  
  ## 3. Exemple complet dans une fenêtre

```python
from PySide6.QtWidgets import QApplication, QWidget, QLabel
from PySide6.QtGui import QPixmap
import sys

class Fenetre(QWidget):
    def __init__(self):
        super().__init__()
        self.initialiser_fenetre()

    def initialiser_fenetre(self):
        self.setWindowTitle("Image dans un QLabel")
        self.resize(400, 300)

        self.label_image = QLabel(self)
        pixmap = QPixmap("mon_image.png")  # Remplacer par ton chemin d'image
        self.label_image.setPixmap(pixmap)
        self.label_image.move(50, 50)

        self.show()

if __name__ == "__main__":
    app = QApplication(sys.argv)
    fenetre = Fenetre()
    app.exec()
```