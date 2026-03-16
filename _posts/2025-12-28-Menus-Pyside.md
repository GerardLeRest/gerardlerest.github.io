---
title: Les menus Pyside6
author: Gérard LE REST
date: 2025-12-28 18:49:00 +0800
categories: [Pyside6, Python, Cours]
tags: [menus]
---
# 📘 PySide6 — Les menus avec QMenu (cours clair et structuré)

Ce cours explique **simplement** comment fonctionnent les menus en PySide6,
en utilisant **explicitement `QMenu`**, sans raccourcis peu lisibles.

---

## 🎯 Objectifs

À la fin de ce cours, tu sauras :

- créer un menu simple
- ajouter un séparateur
- créer un sous-menu
- créer un sous-menu avec **choix exclusif et coches**
- connecter une action à une méthode (`test()`)

---

## 🧠 Principe fondamental

- `QMenuBar` : la barre de menus (en haut de la fenêtre)
- `QMenu` : un menu ou un sous-menu
- `QAction` : une ligne cliquable dans un menu

👉 **Un menu est un objet (`QMenu`) que l’on crée, puis que l’on ajoute à la barre.**

---

## 🧱 Base minimale (obligatoire)

Les menus fonctionnent uniquement avec `QMainWindow`.

```python
import sys
from PySide6.QtWidgets import QApplication, QMainWindow, QMenu
from PySide6.QtGui import QAction
```

---

# 1️⃣ Menu simple avec séparateur et action `test()`

## 🎯 Objectif

Menu **Fichier** :

- Ouvrir → affiche `test`
- ─────────
- Quitter → ferme l’application

---

## 💻 Code complet

```python
import sys
from PySide6.QtWidgets import QApplication, QMainWindow, QMenu
from PySide6.QtGui import QAction

class Fenetre(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Menus PySide6")

        # Barre de menus
        menu_bar = self.menuBar()

        # Menu Fichier (création explicite)
        menu_fichier = QMenu("Fichier", self)

        # Actions
        action_ouvrir = QAction("Ouvrir", self)
        action_quitter = QAction("Quitter", self)

        # Connexions
        action_ouvrir.triggered.connect(self.test)
        action_quitter.triggered.connect(self.close)

        # Insertion dans le menu
        menu_fichier.addAction(action_ouvrir)
        menu_fichier.addSeparator()
        menu_fichier.addAction(action_quitter)

        # Ajout à la barre
        menu_bar.addMenu(menu_fichier)

    def test(self):
        print("test")

app = QApplication(sys.argv)
fenetre = Fenetre()
fenetre.show()
sys.exit(app.exec())
```

---

# 2️⃣ Menu avec sous-menu

```python
menu_edition = QMenu("Édition", self)
menu_preferences = QMenu("Préférences", self)

action_general = QAction("Général", self)

menu_preferences.addAction(action_general)
menu_edition.addMenu(menu_preferences)

self.menuBar().addMenu(menu_edition)
```

---

# 3️⃣ Sous-menu avec choix exclusif et coches (✓)

Menu **Affichage → Thème** :

- ✓ Système (par défaut)
- ☐ Clair
- ☐ Sombre

```python
from PySide6.QtGui import QActionGroup

menu_affichage = QMenu("Affichage", self)
menu_theme = QMenu("Thème", self)

groupe_theme = QActionGroup(self)
groupe_theme.setExclusive(True)

action_systeme = QAction("Système", self, checkable=True)
action_clair = QAction("Clair", self, checkable=True)
action_sombre = QAction("Sombre", self, checkable=True)

action_systeme.setChecked(True)

for action in (action_systeme, action_clair, action_sombre):
    groupe_theme.addAction(action)
    menu_theme.addAction(action)

menu_affichage.addMenu(menu_theme)
self.menuBar().addMenu(menu_affichage)
```

---

## ✅ Conclusion

Les menus PySide6 deviennent simples dès que :

- les objets sont explicites
- la hiérarchie est visible
- on évite les raccourcis opaques
