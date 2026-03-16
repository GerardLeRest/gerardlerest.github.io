---
title: QLineEdit
author: Gérard LE REST
date: 2026-02-15 19:00:00 +0800
categories: [Pyside6, Python, Cours]
tags: [QLineEdit]
---

# QLineEdit — L’essentiel (PySide6)

👉 Champ de saisie **texte sur une seule ligne**  
👉 Permet à l’utilisateur d’entrer une information courte (nom, recherche, mot de passe, etc.)

---

## ✅ Création

```python
champ = QLineEdit()
```

➡️ Crée un champ de saisie vide.

---

## ✏️ Lire / écrire

```python
champ.text()             # lire le texte
champ.setText("Bonjour") # écrire
champ.clear()            # effacer
```

➡️ Permet de récupérer, modifier ou supprimer le contenu du champ.

---

## 🪧 Texte indicatif

```python
champ.setPlaceholderText("Votre nom")
```

➡️ Affiche un texte grisé pour guider l’utilisateur tant que le champ est vide.

---

## 🔒 Mot de passe

```python
champ.setEchoMode(QLineEdit.Password)
```

➡️ Cache les caractères saisis (●●●●).

---

## 🎯 Détecter Entrée

```python
champ.returnPressed.connect(ma_fonction)
```

➡️ Lance une action quand l’utilisateur appuie sur la touche Entrée.

---

## 📌 Résumé ultra-court

👉 `QLineEdit` = saisir du texte  
👉 Widget standard pour les formulaires et recherches

👉 `text()` = lire  
👉 Récupère ce que l’utilisateur a tapé

👉 `setText()` = modifier  
👉 Permet de remplir automatiquement le champ

👉 `placeholder` = aide visuelle  
👉 Indique ce qu’il faut saisir

👉 `Password` = cacher  
👉 Protège les informations sensibles

👉 `returnPressed` = validation  
👉 Utile pour valider sans bouton
