---
# the default layout is 'page'

title: Projet MemoVue  
icon: fas fa-wrench  
order: 6  
---

code source sur github: [MemoVue](https://github.com/GerardLeRest/MemoVue)

## 1. Présentation de VisuMemo

J'ai toujours eu des difficultés à mémoriser les prénoms et les noms de mes élèves. Je me suis dit qu'une application pourrait m'aider, et peut-être aussi mes collègues.  
L'utilisateur peut choisir entre trois configurations :

- prénom et nom  
- prénom seul  
- nom seul  

Quatre modes d'apprentissage sont proposés :

- mode **Apprentissage** : les prénoms et noms défilent en même temps que les portraits  
- mode **Test mental** : le portrait apparaît avec des `???`, laissant le temps à l'utilisateur de réfléchir. En appuyant sur le bouton `→` (sous la photo), la solution apparaît  
- mode **Test écrit** : on écrit le prénom et/ou le nom. Il faut utiliser la zone en haut à droite avec les trois boutons : *Valider*, *Effacer* et *Suite*
- mode **Recherche** : on peut rechercher un ou plusieurs individus présents dans l'organisme
[Video de presentation](https://youtu.be/FgAwiuIiPuc)
vidéo de présentation: 

Trois catégories ont été créées :

- École  
- Entreprise  
- Parlement  

Chaque catégorie est liée à sa propre base de données. Toutes les bases ont la même structure (voir `tables.sql` dans `fichiers/eleves`). Il suffit ensuite de modifier les trois fichiers CSV si l'on souhaite adapter le logiciel à son propre organisme. On peut même ajouter des organismes supplémentaires.

![Choix_organisme](assets/img/choix_organisme.png)

## 2. Un peu de code

Ce code désactive ou active les widgets pour l'option recherche dans le lycée :

```python
def effacerReponses(self) -> None:
        """effacer réponses"""
        # effacer champs des noms et prénom
        self.prenomEntry.setEnabled(True)
        self.prenomEntry.clear()
        self.nomEntry.setEnabled(True)
        self.nomEntry.clear()
        # effacer icone
        self.image = QPixmap(os.path.join(repertoireRacine, "fichiers", "icones", transparent.png"))
        self.labelImageGauche.setPixmap(self.image) 
        # désactiver - Nbres bonne réponse  
        self.nbreRep.setEnabled(False) 
```

## 3. Technologie

Python 3, SQLite, PySide6

## 4. Interface

![Interface](assets/img/interface.png)

## 5. Conclusion

Le programme fonctionne parfaitement. Après être passé de Tkinter à PySide6, j’ai intégré deux premiers organismes (école et entreprise). Le projet est déjà pleinement opérationnel, mais comme tout projet vivant, il peut encore être amélioré.
Vos remarques, suggestions ou retours sont les bienvenus.
