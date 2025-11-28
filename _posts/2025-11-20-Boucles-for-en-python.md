---
title: Boucles for en Python
author: Gérard LE REST
date: 2025-11-20 17:34:00 +0800
categories: [Python, Cours]
tags: [for, enuerate]
---

# Les différentes formes de `for` en Python (avec résultats)

## 1. Boucle `for` classique

```python
fruits = ["pomme", "banane", "kiwi"]

for fruit in fruits:
    print(fruit)
```

Résultat :
pomme
banane
kiwi

## 2. Boucle for avec index : enumerate()

```python
fruits = ["pomme", "banane", "kiwi"]

for index, fruit in enumerate(fruits):
    print(index, fruit)
```

Résultat :
0 pomme
1 banane
2 kiwi
Avec un index qui commence à 1

```python
for index, fruit in enumerate(fruits, start=1):
    print(index, fruit)
```

Résultat :
1 pomme
2 banane
3 kiwi

## 3. Boucle for en une ligne (list comprehension)

```pyton
[print(fruit) for fruit in fruits]
```

Résultat :
pomme
banane
kiwi

## 4. Création d’une nouvelle liste en une ligne

```python
longs = [fruit for fruit in fruits if len(fruit) > 5]
print(longs)
```

Résultat :
['pomme', 'banane']

## 5. Avec enumerate() en une ligne

```Pyrhon
for [print(i, fruit) for i, fruit in enumerate(fruits)]
```

Résultat :
0 pomme
1 banane
2 kiwi

---

Si tu veux, je peux aussi ajouter les exemples avec `range()` ou les boucles imbriquées.
