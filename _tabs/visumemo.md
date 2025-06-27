---
# the default layout is 'page'

title: Projet VisuMemo
icon: fas fa-wrench
order: 6
---

github: [VisuMemo](https://github.com/GerardLeRest/VisuMemo)

## 1. Présentation de VisuMemo

J'a toujours eu des difficultés à mémoriser les prénoms et les noms de mes élèves. Je me suis dit qu'une application pourrait m'aider mais aussi mes collègues.

## 2 Un peu de code

Ce code désactive ou active les widgets pour l'option recherche dans le lycée

```python
def configRechercher(self) -> None:
        """activer/désactiver les listes les comboBox, des radiobuttons
           et des labels"""
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

## 3 Technologie

Python, SQLite, Tkinter

## 4 Interface

![VisuMemo](assets/img/visu_memo.png)

## 5 Conclusion

Le programme fonctionne parfaitemnt, Je viens de passer de Tkinter à PySide6. Je travaille actuellent sur des versions pour l'asssemblée nationale et pour les entreprises.
