---
title: Refactorisation Python
author: Gérard LE REST
date: 2026-02-11 10:44:00 +0800
categories: [Python, Tutoriel]
tags: [sanke_case, camelcase, constante]
---

# 

## 🎯 Objectif

Renommer des variables Python :

- sans casser le code
- sans créer d’incohérences
- en respectant les bonnes pratiques
- avec une démarche progressive et sécurisée

---

## 1. Respecter les conventions (PEP 8)

En Python standard :

- Variables → `snake_case`
- Fonctions → `snake_case`
- Méthodes → `snake_case`
- Classes → `CamelCase`
- Constantes → `MA_CONSTANTE`
- Attributs internes → `_mon_attribut`
- noms de fichier → snake_case

Exemple :

```python
class EleveManager:

    def charger_donnees(self, fichier_csv):
        nombre_eleves = 0
```

## 2. Utiliser un renommage intelligent (VS Code)

Toujours utiliser :
F2 → Rename Symbol

⚠️ Ne pas utiliser "Rechercher / Remplacer" global.
