---
# the default layout is 'page'

title: Piveo
icon: fas fa-wrench
order: 6

---

"**Piveo** est une application **libre et gratuite** conçue pour aider les enseignants et les entreprises à apprendre et mémoriser rapidement les noms et les prénoms."

## 1. Présentation de Piveo

J’ai toujours eu des difficultés à mémoriser les prénoms et les noms de mes élèves.  
Je me suis dit qu’une application pourrait m’aider, mais aussi aider mes collègues.

---

## 2. Comment utiliser Piveo pour apprendre les prénoms ?

![Logiciel apprendre noms prénoms - Accueil](assets/img/piveo-accueil.png)

Le logiciel Piveo s’utilise ainsi :

- On sélectionne l’organisme souhaité (voir ci-dessus)
- Puis on choisit le groupe à l’aide des combobox (ici : departement et fonctions)
- On sélectionne ensuite le mode de mémorisation (apprentissage, mode oral,  écrit). Un mode aléatoire est sélectionnable.
- La partie de gauche permet de faire défiler les élèves tout en affichant leurs informations
- Un mode de recherche permet de retrouver un ou plusieurs élèves à partir de leur nom ou prénom

Pour plus d'information cliquer sur les liens ci-dessous

![interface](assets/img/piveo-interface.png)
*interfcae de l'application*

## 3. Un peu de code

Ce code désactive ou active les widgets pour l'option recherche dans le lycée

```python
def configRechercher(self) -> None:
        """Activer ou désactiver les ComboBox et les boutons radio
           selon le mode sélectionné."""
        if (self.SelectModes.get() == "4"):
            # désactiver les radiobuttons
            self.checkbutAleatoire.configure(state="disabled")
            # désactiver les listes des comboBox
            self.combog.configure(state="disabled")
            self.combod.configure(state="disabled")
        else:
            # activer les listes des comboBox
            self.combog.configure(state="normal")
            self.combod.configure(state="normal")
            # activer les radiobuttons
            self.checkbutAleatoire.configure(state="normal")
```

## 4. Technologie

- Python,

- SQLite

- Tkinter

- PySide6

## 5. Un logiciel libre pour l'éducation et les entreprises

Le programme est fonctionnel et stable.  
L’interface a été retravaillée avec PySide6.

La version 2 met en place une architecture de type MVC afin d’améliorer la lisibilité et la maintenance du code, ainsi qu’une interface améliorée.

# 6. liens

[Github - Piveo](https://github.com/GerardLeRest/Piveo-v2) <br>
[téléchargement - Piveo](https://github.com/GerardLeRest/Piveo-v2/releases) <br>
[wiki ubuntu-fr - piveo](https://doc.ubuntu-fr.org/piveo)
