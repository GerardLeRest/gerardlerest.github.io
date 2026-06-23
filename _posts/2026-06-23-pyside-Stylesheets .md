---
title: Styliser une interface PySide6 avec les Stylesheets (QSS)
author: Gérard LE REST
date: 2026-06-23 03:00:00 +0200
categories: [Pyside6, Python, Cours]
tags: [stylesheet, qss, design, interface]

---

# Styliser une interface PySide6 avec les Stylesheets (QSS)

## 1. Principe général

Les Stylesheets Qt (QSS) permettent de modifier l'apparence des widgets.

Leur syntaxe est très proche du CSS utilisé en développement web.

Grâce aux QSS, il est possible de :

* changer les couleurs ;
* modifier les polices ;
* ajouter des bordures ;
* créer des coins arrondis ;
* ajouter des marges ;
* ajouter des espacements ;
* personnaliser l'apparence des boutons, champs de saisie, labels, etc.

---

## 2. Syntaxe de base

```python
widget.setStyleSheet("""
    propriété: valeur;
""")
```

Exemple :

```python
bouton.setStyleSheet("""
    background-color: lightblue;
""")
```

---

## 3. Changer la couleur d'un bouton

```python
bouton.setStyleSheet("""
    QPushButton {
        background-color: #4CAF50;
        color: white;
    }
""")
```

Résultat :

* fond vert ;
* texte blanc.

---

## 4. Ajouter des coins arrondis

```python
bouton.setStyleSheet("""
    QPushButton {
        background-color: #4CAF50;
        color: white;
        border-radius: 10px;
    }
""")
```

Résultat :

```text
╭──────────────╮
│   Valider    │
╰──────────────╯
```

---

## 5. Ajouter une bordure

```python
champ.setStyleSheet("""
    QLineEdit {
        border: 2px solid gray;
    }
""")
```

Résultat :

Le champ possède une bordure grise de 2 pixels.

---

## 6. Ajouter de l'espace intérieur (padding)

```python
champ.setStyleSheet("""
    QLineEdit {
        padding: 8px;
    }
""")
```

Résultat :

Le texte ne touche plus les bords du champ.

---

## 7. Bordure + coins arrondis + padding

```python
champ.setStyleSheet("""
    QLineEdit {
        border: 1px solid gray;
        border-radius: 8px;
        padding: 6px;
    }
""")
```

C'est probablement le style que tu utiliseras le plus souvent.

---

## 8. Modifier la couleur de fond d'une fenêtre

```python
self.setStyleSheet("""
    QWidget {
        background-color: #f5f5f5;
    }
""")
```

Résultat :

Fond gris très clair.

---

## 9. Modifier un QLabel

```python
label.setStyleSheet("""
    QLabel {
        color: navy;
        font-size: 18px;
        font-weight: bold;
    }
""")
```

Résultat :

* texte bleu foncé ;
* taille plus grande ;
* gras.

---

## 10. Changer la police

```python
label.setStyleSheet("""
    QLabel {
        font-family: Arial;
        font-size: 20px;
    }
""")
```

---

## 11. Effet au survol de la souris

```python
bouton.setStyleSheet("""
    QPushButton {
        background-color: #4CAF50;
        color: white;
        border-radius: 8px;
    }

    QPushButton:hover {
        background-color: #45a049;
    }
""")
```

Résultat :

Le bouton devient plus foncé lorsque la souris passe dessus.

---

## 12. Modifier tous les boutons de la fenêtre

```python
self.setStyleSheet("""
    QPushButton {
        background-color: #2196F3;
        color: white;
        border-radius: 8px;
        padding: 8px;
    }
""")
```

Tous les boutons héritent automatiquement du style.

---

## 13. Ajouter de l'espace entre les widgets

```python
layout.setSpacing(15)
```

Résultat :

15 pixels entre chaque widget.

---

## 14. Ajouter des marges

```python
layout.setContentsMargins(
    20,
    20,
    20,
    20
)
```

Ordre :

```text
gauche, haut, droite, bas
```

Résultat :

20 pixels libres autour du contenu.

---

## 15. Exemple complet de formulaire moderne

```python
self.setStyleSheet("""
    QWidget {
        background-color: #f5f5f5;
    }

    QLabel {
        font-size: 14px;
        font-weight: bold;
    }

    QLineEdit {
        border: 1px solid gray;
        border-radius: 8px;
        padding: 6px;
        background-color: white;
    }

    QPushButton {
        background-color: #4CAF50;
        color: white;
        border-radius: 8px;
        padding: 8px;
    }

    QPushButton:hover {
        background-color: #45a049;
    }
""")
```

Avec seulement quelques lignes, ton interface devient beaucoup plus moderne.

---

## 16. Ce qu'il faut retenir

✅ `background-color`
change la couleur de fond

✅ `color`
change la couleur du texte

✅ `border`
ajoute une bordure

✅ `border-radius`
crée des coins arrondis

✅ `padding`
ajoute de l'espace intérieur

✅ `font-size`
modifie la taille du texte

✅ `font-weight`
met le texte en gras

✅ `hover`
modifie l'apparence lors du survol

---

## Résumé

Propriété Utilisation

---

background-color Couleur de fond

color Couleur du texte

border Bordure

border-radius Coins arrondis

padding Espace intérieur

font-size Taille du texte

font-weight Texte gras

hover Effet au survol

spacing Espace entre widgets

contentsMargins Marge autour du layout

Pour moderniser rapidement une interface PySide6, les propriétés les plus utiles sont :

* border-radius
* padding
* background-color
* hover
* setSpacing()
* setContentsMargins()

Avec ces quelques outils, il est possible de transformer une interface très simple en une interface agréable et moderne.
