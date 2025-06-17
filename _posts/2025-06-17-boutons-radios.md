---
title: "K - boutons radios"
date: 2025-06-17 18:32:05 +0800
categories: [cours]
tags: [python, pyside6]
---

## 1. Objectif :

Permettre à l’utilisateur de choisir une seule option parmi plusieurs (ex : Prénom+Nom, Prénom, Nom dans ton cas).  
🔧 Utilisation de base :

from PySide6.QtWidgets import QRadioButton, QVBoxLayout, QWidget, QApplication

app = QApplication(\[\])

fenetre = QWidget()

## 2. Création des boutons radio

radio1 = QRadioButton("Prénom+Nom")  
radio2 = QRadioButton("Prénom")  
radio3 = QRadioButton("Nom")

## 3. Définir un bouton coché par défaut

radio1.setChecked(True)

## 4. Ajout dans un layout vertical

layout = QVBoxLayout()  
layout.addWidget(radio1)  
layout.addWidget(radio2)  
layout.addWidget(radio3)

fenetre.setLayout(layout)  
fenetre.show()  
app.exec()

💡 Regroupement logique avec QButtonGroup

Si tu veux récupérer plus facilement le bouton sélectionné :

from PySide6.QtWidgets import QButtonGroup

## 5. Créer un groupe de boutons

groupe = QButtonGroup()  
groupe.addButton(radio1, 1)  
groupe.addButton(radio2, 2)  
groupe.addButton(radio3, 3)

## 6. Récupérer l’ID du bouton sélectionné

def selection():  
print("ID sélectionné :", groupe.checkedId())

## 7. Par exemple, appel de cette fonction via un bouton "Valider"

🧩 Dans ton interface

Tu utilises :

Trois options radio côte à côte,
L’option par défaut est Prénom+Nom,
Tu peux ajouter ces boutons dans un QHBoxLayout pour garder une présentation horizontal
