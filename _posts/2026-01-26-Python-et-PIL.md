---
title: Python et PIL (Pillow)
author: Gérard LE REST
date: 2026-01-26 17:53:00 +0800
categories: [Python, Cours]
tags: [Image, PIL]
---

# Python et PIL (Pillow)

> **Objectif** : comprendre PIL par les **blocs essentiels**, avec **peu de texte** et **du code lisible**.
> À relire souvent. À utiliser comme fiche.

---

## 1. Ce qu’est PIL (Pillow)

- Bibliothèque Python pour **manipuler des images**
- Ouvre, transforme, compose, écrit du texte
- Utilisée dans tes projets (PDF, jaquettes, UI)

```bash
pip install pillow
```

```python
from PIL import Image, ImageDraw, ImageFont
```

---

## 2. Ouvrir et afficher une image

```python
from PIL import Image

img = Image.open("photo.jpg")
img.show()          # aperçu rapide
print(img.size)     # (largeur, hauteur)
print(img.mode)     # RGB, RGBA, L...
```

**Bloc mental** : *ouvrir → observer*

---

## 3. Redimensionner (piège classique)

```python
img2 = img.resize((400, 300))
img2.save("petite.jpg")
```

➡️ `resize()` **ne modifie pas l’original**

---

## 4. Redimensionner en gardant les proportions

```python
img.thumbnail((400, 300))
img.save("proportionnelle.jpg")
```

➡️ `thumbnail()` **modifie l’image en place**

---

## 5. Créer une image vide

```python
img = Image.new("RGB", (400, 300), "white")
img.save("vide.jpg")
```

**Très important** : base pour composition, PDF, jaquettes

---

## 6. Coller une image dans une autre

```python
fond = Image.new("RGB", (600, 400), "white")
photo = Image.open("photo.jpg")

fond.paste(photo, (50, 50))
fond.save("compose.jpg")
```

**Bloc mental** : *fond → élément → position*

---

## 7. Gérer la transparence (RGBA)

```python
fond = Image.new("RGBA", (600, 400), (255, 255, 255, 255))
logo = Image.open("logo.png").convert("RGBA")

fond.paste(logo, (100, 100), logo)
fond.save("alpha.png")
```

➡️ Le **3ᵉ argument** est le masque

---

## 8. Dessiner du texte

```python
from PIL import ImageDraw, ImageFont

img = Image.new("RGB", (400, 200), "white")
draw = ImageDraw.Draw(img)

font = ImageFont.truetype("Arial.ttf", 20)
draw.text((20, 50), "Bonjour", fill="black", font=font)

img.save("texte.jpg")
```

➡️ Sans police : `ImageFont.load_default()`

---

## 9. Mesurer un texte (centrage)

```python
bbox = draw.textbbox((0, 0), "Titre", font=font)
largeur = bbox[2] - bbox[0]
hauteur = bbox[3] - bbox[1]
```

➡️ Indispensable pour **centrer proprement**

---

## 10. Sauvegarder proprement

```python
img.save("image.png")
img.save("image.jpg", quality=95)
```

Formats courants : PNG, JPG, JPEG, PDF

---

## 11. Les pièges classiques

- oublier que certaines méthodes **retournent une nouvelle image**
- mélanger RGB / RGBA
- ne pas mesurer le texte avant de le placer
- écraser l’image source sans le vouloir

---

## 12. Structure recommandée (artisan)

```python
class ImageComposer:
    def __init__(self, taille):
        self.img = Image.new("RGB", taille, "white")

    def coller(self, image, position):
        self.img.paste(image, position)

    def sauver(self, chemin):
        self.img.save(chemin)
```

➡️ PIL = **métier**, pas UI

---

## 13. À retenir (essentiel)

- PIL travaille par **blocs simples**
- Tu composes plus que tu ne calcules
- Une bonne fiche évite 80 % des pièges

> **Ce cours est volontairement court.**
> Il est fait pour être relu, pas appris par cœur.title: Traitement des fichiers en Python
> author: Gérard LE REST
> date: 2026-01-10 14:48:00 +0800
> categories: [Python, Cours]
> tags: [fichier, dossier]
