---

title: BP et Méthode
author: Gérard LE REST
date: 2026-01-20 15:24:00 +0800
categories: [Pyside6, Cours]
tags: [bouton poussoir]

---

# Comment lancer une méthode avec un bouton en PySide

## 1. Principe général

- Un bouton (QPushButton) peut émettre un signal quand tu cliques dessus.
- Ce signal (clicked) peut être connecté à n'importe quelle méthode de ta classe.

## 2. Syntaxe de base

```python
bouton.clicked.connect(self.nom_de_la_methode)
```

✅ Important :  
Pas de parenthèses après self.nom_de_la_methode  
Sinon tu appelles la fonction immédiatement au lieu de lui dire d'attendre le clic.

## 3. Exemple simple

```python
from PySide6.QtWidgets import QApplication, QWidget, QPushButton
import sys

class Fenetre(QWidget):
    def __init__(self):
        super().__init__()
        self.initialiser_fenetre()

    def initialiser_fenetre(self):
        self.setWindowTitle("Bouton qui lance une méthode")
        self.resize(400, 300)

        # Création du bouton
        bouton = QPushButton("Clique ici", self)
        bouton.move(150, 130)

        # Connexion du clic à une méthode de la classe
        bouton.clicked.connect(self.ma_methode)

        self.show()

    def ma_methode(self):
        print("Le bouton a été cliqué !")

if __name__ == "__main__":
    app = QApplication(sys.argv)
    fenetre = Fenetre()
    app.exec()
```

## 4\. Ce que fait ce code

Action Résultat

* * *

Clique sur le bouton La méthode ma_methode() est appelée  
Que fait la méthode ? Elle affiche Le bouton a été cliqué ! dans la console.

✅ C'est toujours comme ça :

- Tu crées un bouton,
- Tu connectes son clicked à ta méthode sans parenthèses,
- Et ta méthode est exécutée seulement quand l'utilisateur clique.