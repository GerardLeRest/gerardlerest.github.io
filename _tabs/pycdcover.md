---
# the default layout is 'page'

title: PyCDCover - V2
icon: fas fa-wrench  
order: 4 
---

code source sur github: [PyCDCover](https://github.com/GerardLeRest/pycdcover-v2)

## 1. Présentation de PyCDCover

PyCDCover est un générateur de jaquettes:
- pour des maquettes d'albums (un album/CD)
- pour des CD multi-albums (plusieurs albums par CD)
Il est également possible de travailler directement avec des dossiers de fichiers musicaux 

## 2. Fonctionnement du logiciel

Avant d'utiliser le CD, il faut taguer les chansons, soit dans celles du dossier ou du
CD (easytag, par exemple). Sans ces informations (artist, album, année, genre, titres), le logiciels ne pourra pas fournir les informations nécessaire.
Au minimum, il faut taguer les artistes et les albums. Ces deux informtions sont indispensables pour récuperer la photo de 
l'album.
De la gauche à la droite, il faut appuyer sur:
1 - Donner un nom au CD (pour une quette - 1 album), donner le nom de l'ariste.
2 - Récupérer les tags du dossier ou du CD
3 - Éditer et/ou modifier les valeus des tags
4 - Récupérer les images à partir de Itunes ou Musicbrainz
4 - Créer les faces avant et arrières du CD
5 - Générer le PDF

PDF CD_Maquette.pdf:
[Télécharger le PDF]({{ '/assets/CD_maquette.pdf' | relative_url }})

PDF CD_Multi-albums.pdf:
[Télécharger le PDF]({{ '/assets/CD_Multi-albums.pdf' | relative_url }})


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
        self.dossier_racine = Path(__file__).parent.parent
        self.dossier_polices = self.dossier_racine / "ressources" / "polices"
        self.dossier_pycdcover = Path.home() / "PyCDCover"

    def titre_horizontal(self) -> None:
        """Création de l'image horizontale du titre"""
        print("titre_horizontal")
        imageH = Image.new("RGB", (self.L_devant, 220), "white")
        draw = ImageDraw.Draw(imageH)
        police1 = self.dossier_polices / "FreeSerif.ttf"
        try:
            font1 = ImageFont.truetype(str(police1), 60)
        except OSError:
            font1 = ImageFont.load_default()
        bbox = draw.textbbox((0, 0), self.titre, font=font1)
        largeur_texte = bbox[2] - bbox[0]
        x = (self.L_devant - largeur_texte) / 2
        y = 60
        draw.text((x, y), self.titre, fill="black", font=font1)
        imageH.save(self.dossier_pycdcover / "TitreH.png", "PNG")
```

## 3. Technologie

Python 3, PySide6, Reportlab, pillow

## 4. Interface

![PyCDCover]({{ '/assets/img/PyCDCover.png' | relative_url }})

## 5. Conclusion

PyCDCOver a été le deuxième logiciel conséquent que j'ai créé. Son interface était trop sommaire pour qu'il fut beaucoup utilisé. Mais il était référencé, donc
je ne sais pas vraiment qu'est-ce qu'il en est. Pyside6m'a permis d"améiorer plus robuste en uilisant la technologie MVC et une interface plus attrayante, même
si la nouvelle interface est perfectible.
