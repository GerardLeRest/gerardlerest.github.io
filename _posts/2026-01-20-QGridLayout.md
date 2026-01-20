---
title: QGridLayout
author: Gerard LE REST
date: 2026-01-20 18:30:00 +0800
categories: [Pyside6, Cours]
tags: [QGridLayout]

---

# QGridLayout – Disposition en grille avec PySide6

## 1. Introduction

QGridLayout est un gestionnaire de mise en page en tableau (grille).  
Il place les widgets en lignes et colonnes, comme dans une feuille de calcul.

C’est idéal pour :

- Aligner des étiquettes et champs (QLabel + QLineEdit)
- Construire des interfaces claires, même complexes
- Contrôler facilement l’emplacement de chaque widget

---

## 2. Structure de base

### 2.1 Syntaxe

layout = QGridLayout()  
layout.addWidget(widget, ligne, colonne)

Tu peux aussi utiliser :

layout.addWidget(widget, ligne, colonne, rowspan, colspan)

Pour étendre un widget sur plusieurs lignes ou colonnes.

---

## 2.2 Exemple simple

```python
from PySide6.QtWidgets import (
    QApplication, QWidget, QLabel, QLineEdit, QGridLayout
)
import sys

class Fenetre(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Formulaire")

        layout = QGridLayout()

        layout.addWidget(QLabel("Prénom :"), 0, 0)
        layout.addWidget(QLineEdit(), 0, 1)

        layout.addWidget(QLabel("Nom :"), 1, 0)
        layout.addWidget(QLineEdit(), 1, 1)

        self.setLayout(layout)

if __name__ == "__main__":
    app = QApplication(sys.argv)
    fen = Fenetre()
    fen.show()
    app.exec()
```

---

## 3. Options utiles

### 3.1 setSpacing

Définit l’espace entre les widgets (par défaut : 6 px)

layout.setSpacing(10)

### 3.2 setContentsMargins

Ajoute une marge autour du layout dans le widget conteneur.

layout.setContentsMargins(20, 10, 20, 10)

---

## 4. Étendre un widget (rowspan / colspan)

layout.addWidget(QPushButton("Valider"), 2, 0, 1, 2)

Ici, le bouton est placé en ligne 2, colonne 0, et occupe 1 ligne et 2 colonnes.

---

## 5. Exemple avancé

layout.addWidget(QLabel("Adresse :"), 2, 0)  
layout.addWidget(QLineEdit(), 2, 1, 1, 2)  (s'étend sur 2 colonnes)

---

## 6. Bonnes pratiques

- Regrouper les widgets logiquement par lignes
- Utiliser rowspan ou colspan pour les titres ou champs larges
- Combiner avec d'autres layouts si besoin (QVBoxLayout, QHBoxLayout, etc.)

---

## 7. Conclusion

QGridLayout est un outil puissant pour créer des interfaces propres, bien alignées, et facilement maintenables.  
C’est souvent le choix par défaut pour les formulaires ou panneaux de configuration.
