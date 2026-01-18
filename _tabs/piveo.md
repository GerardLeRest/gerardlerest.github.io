---
# the default layout is 'page'

title: Projet Piveo
icon: fas fa-wrench
order: 6
---

[téléchargement Piveo](https://github.com/GerardLeRest/Piveo/releases)

## 1. Présentation de Piveo

J'a toujours eu des difficultés à mémoriser les prénoms et les noms de mes élèves. Je me suis dit qu'une application pourrait m'aider mais aussi mes collègues.

## Présentation

![Accueil](assets/img/accueil.png)

Le logiciel Piveo s'utilise ainsi:

- On sélectionne l'orgnisme que l'on souhaite (voir ci-dessus)
- Puis on choisit le groupe avec les combobox (ici: Classe et Options) - voir ci-dessous
- on sectionne ensuite le mode de mémorisation (apprentissage, par mode orale ou écrit

- La partie de gauche permet de faire défiler les élèves tout en donnant leurs informations
- Un mode de recherche permet de rotrouver un(des) élèves suivant leurs noms/prénoms

## 3 Un peu de code

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

## 4 Technologie

Python, SQLite, Tkinter

## 5 Interface

![VisuMemo](assets/img/visu_memo.png)

## 6 Conclusion

Le programme fonctionne parfaitement, L'interface a été retravaillé avec Pyside6.
