---
# the default layout is 'page'

title: Projet Piveo
icon: fas fa-wrench
order: 6

---

## 1. Présentation de Piveo

J'a toujours eu des difficultés à mémoriser les prénoms et les noms de mes élèves. Je me suis dit qu'une application pourrait m'aider mais aussi mes collègues.

## 2. Présentation

![Accueil](assets/img/piveo-accueil.png)

Le logiciel Piveo s'utilise ainsi:

- On sélectionne l'orgnisme que l'on souhaite (voir ci-dessus)

- Puis on choisit le groupe avec les combobox (ici: Classe et Options) - voir ci-dessous

- on sectionne ensuite le mode de mémorisation (apprentissage, par mode orale ou écrit

- La partie de gauche permet de faire défiler les élèves tout en donnant leurs informations

- Un mode de recherche permet de retrouver un(des) élèves suivant leurs noms/prénoms

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

Python, SQLite, Tkinter

## 5. Conclusion

Le programme fonctionne parfaitement, L'interface a été retravaillée avec Pyside6.
La prochaine étape consistera à créer un système MVC pour une lecture plus lisible.

# 6. liens

[Github - Piveo](https://github.com/GerardLeRest/Piveo) <br>
[téléchargement - Piveo](https://github.com/GerardLeRest/Piveo/releases) <br>
[wiki ubuntu-fr - piveo](https://doc.ubuntu-fr.org/piveo)
