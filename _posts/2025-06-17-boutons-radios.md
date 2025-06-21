---
title: "K - boutons radios"
date: 2025-06-17 18:32:05 +0800
categories: [cours]
tags: [python, pyside6]
---
## 1. Étapes simples

- Importer les classes suivantes : QRadioButton, QHBoxLayout, QVBoxLayout, QLabel, QPushButton
- Créer une fenêtre avec un QVBoxLayout principal
- Ajouter un QLabel fixe pour le titre
- Créer trois boutons radio avec un texte
- Les ajouter dans un QHBoxLayout
- Ajouter un bouton "Valider" pour tester quel bouton est coché
- Afficher le résultat dans un second QLabel

## 2. Code complet

```python
from PySide6.QtWidgets import (
    QApplication, QWidget, QRadioButton, QLabel,
    QHBoxLayout, QVBoxLayout, QPushButton
)
import sys

class Fenetre(QWidget):

    def __init__(self):
        super().__init__()
        self.initialisation()

    def initialisation(self):
        self.setWindowTitle("Boutons radio avec layout")
        self.resize(400, 200)

        # Label fixe
        label_choix = QLabel("Choisissez une option :")

        # Boutons radio
        self.radio1 = QRadioButton("Option A")
        self.radio2 = QRadioButton("Option B")
        self.radio3 = QRadioButton("Option C")

        # Cocher une option par défaut (facultatif)
        self.radio1.setChecked(True)

        # Layout horizontal pour les boutons radio
        layout_radio = QHBoxLayout()
        layout_radio.addWidget(self.radio1)
        layout_radio.addWidget(self.radio2)
        layout_radio.addWidget(self.radio3)

        # Bouton pour valider le choix
        bouton_valider = QPushButton("Valider")
        bouton_valider.clicked.connect(self.verifier_choix)

        # Label pour afficher le choix sélectionné
        self.label_resultat = QLabel("")

        # Layout principal
        layout_principal = QVBoxLayout()
        layout_principal.addWidget(label_choix)
        layout_principal.addLayout(layout_radio)
        layout_principal.addWidget(bouton_valider)
        layout_principal.addWidget(self.label_resultat)

        self.setLayout(layout_principal)
        self.show()

    def verifier_choix(self):
        if self.radio1.isChecked():
            self.label_resultat.setText("Vous avez choisi : Option A")
        elif self.radio2.isChecked():
            self.label_resultat.setText("Vous avez choisi : Option B")
        elif self.radio3.isChecked():
            self.label_resultat.setText("Vous avez choisi : Option C")

if __name__ == "__main__":
    app = QApplication(sys.argv)
    fenetre = Fenetre()
    app.exec()
``
