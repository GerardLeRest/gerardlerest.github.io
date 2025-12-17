---
# the default layout is 'page'

title: Projet PyCDCover
icon: fas fa-wrench  
order: 7 
---

[Téléchargement PyCDCover](https://github.com/GerardLeRest/pycdcover-v2)

## 1. Présentation de PyCDCover

PyCDCover est un générateur de jaquettes:

- pour des maquettes d'albums (un album par CD)

- pour des CD multi-albums (plusieurs albums par CD)
  
  Il est également possible de travailler directement avec des dossiers de fichiers musicaux 

## 2. Fonctionnement du logiciel

Avant d'utiliser le CD, il faut taguer les chansons, soit dans celles du dossier ou soit dans celles du CD. On peut utiliser Easytag, par exemple. Sans ces informations (artist, album, année, genre, titres), le logiciels ne pourra pas traiter ces informations nécessaires.
Les tags récupérés, le nom de l'artistes et de l'album permettent de récpérer depuis des sites internet la photo de la jaquette.

Sur le logiciel, de la gauche vers la droite, il faut appuyer sur:

1. Donner un nom au CD. Pour une maquette - 1 album), il faut donner le nom de l'ariste à ce titre.

2. Récupérer les tags du dossier ou du CD

3. Éditer et/ou modifier les valeus des tags

4. Récupérer les images à partir de Itunes ou Musicbrainz

5. Créer les faces avant et arrières du CD

6. Générer le PDF
- cette maquette a été faite avec l'accord du groupe
  @CENT DÉTRESSES
  ![CD_maquette](assets/img/CD_maquette.png)
  *Figure 1 :CD-maquette*

- Cette jaquette multi-album présente les images en petit format, à but démonstratif et non lucratif.
  ![CD-maquette_multi-albums](assets/img/CD_multi-albums.png)
  *Figure 2 :CD-multi-albums*

## 3. Un peu de code

Ce code désactive ou active les widgets pour l'option recherche dans le lycée :

```python
class Titres:
    """Crée les images des titres (horizontal et verticaux) pour la jaquette CD."""

    def __init__(self, L_devant: int, H_back_cover: int, titre: str) -> None:
        self.titre = titre
        self.L_devant = L_devant
        self.H_back_cover = H_back_cover
        self.x = 0
        self.y = 0
        # dossiers
        self.dossier_racine = Path(__file__).parent.parents
        self.dossier_polices = self.dossier_racine / "ressources" / "polices"
        self.dossier_pycdcover = Path.home() / "PyCDCover"

    def titre_horizontal(self) -> None:
        """Création de l'image horizontale du titre"""
        # image contenant le titre horizontal
        imageH = Image.new("RGB", (self.L_devant, 220), "white")
        draw = ImageDraw.Draw(imageH)
        police1 = self.dossier_polices / "FreeSerif.ttf"
        font1 = ImageFont.truetype(str(police1), 60)
        bbox = draw.textbbox((0, 0), self.titre, font=font1)
        largeur_texte = bbox[2] - bbox[0]
        x = (self.L_devant - largeur_texte) / 2
        y = 60
        draw.text((x, y), self.titre, fill="black", font=font1)
        imageH.save(self.dossier_pycdcover / "TitreH.png", "PNG")
```

## 3. Technologie

Python 3, PySide6, Reportlab, Pillow

## 4. Interface

![PyCDCover](assets/img/PyCDCover.png)

## 5. Conclusion

PyCDCOver a été le deuxième logiciel conséquent que j'ai créé. Son interface était trop sommaire pour qu'il fut beaucoup utilisé. Mais il était référencé, donc
je ne sais pas vraiment qu'est-ce qu'il en est. Pyside6m'a permis d"améiorer plus robuste en uilisant la technologie MVC et une interface plus attrayante, même
si la nouvelle interface est perfectible.
