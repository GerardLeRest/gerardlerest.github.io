---
title: "I - Champs Texte"
date: 2025-06-17 17:46:00 +0800
categories: [cours]
tags: [python, pyside6]
---

## 1. Le widget à utiliser
✅ En PySide, un champ de saisie texte s'appelle :
QLineEdit
## 2. Syntaxe ultra simple
from PySide6.QtWidgets import QLineEdit
champ_texte = QLineEdit()
✅ C’est tout !
Ensuite, tu peux :
- L’ajouter dans un layout (addWidget(champ_texte)),
- Changer son texte avec setText("..."),
- Lire ce que l’utilisateur a écrit avec text().
## 3. Exemple minimal
```python
from PySide6.QtWidgets import QApplication, QWidget, QLineEdit, QVBoxLayout
import sys

class Fenetre(QWidget):
    def __init__(self):
        super().__init__()
        self.initialiser_fenetre()

    def initialiser_fenetre(self):
        self.setWindowTitle("Champ texte")
        self.resize(400, 300)

        layout = QVBoxLayout()

        # Création du champ de texte
        self.champ_nom = QLineEdit()
        self.champ_nom.setPlaceholderText("Entrez votre nom")
        layout.addWidget(self.champ_nom)
        self.setLayout(layout)
        self.show()

if __name__ == "__main__":
    app = QApplication(sys.argv)
    fenetre = Fenetre()
    app.exec()
```
✅ Ce que fait ce code :
- Crée un QLineEdit vide,
- Ajoute un texte gris "Entrez votre nom" en guide d'indication (setPlaceholderText),
- Permet à l’utilisateur de taper dedans.
