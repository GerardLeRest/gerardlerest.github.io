---
title: Traitement des fichiers en Python
author: Gérard LE REST
date: date: 2026-01-10 14:48:00
categories: [Python, Cours]
tags: [Fichier, dossier]
---

# Traitement des fichiers en Python

## Comparaison `os` / `os.path` et `pathlib.Path`

*(document court et synthétique)*

---

## 1. Deux approches

| Aspect          | `os.listdir()` / `os.path` | `pathlib.Path` |
| --------------- | -------------------------- | -------------- |
| Approche        | Fonctionnelle              | Orientée objet |
| Concept central | Chaînes (`str`)            | Objet `Path`   |
| Style           | Hérité                     | Moderne        |
| Lisibilité      | Moyenne                    | Excellente     |
| Portabilité     | À gérer                    | Native         |

---

## 2. Lister des fichiers

### `os`

```python
import os
fichiers = os.listdir("data")
```

### `pathlib`

```python
from pathlib import Path
fichiers = Path("data").iterdir()
```

---

## 3. Tester un chemin

### Existence

**`os`**

```python
import os
os.path.exists("data/notes.txt")
```

**`pathlib`**

```python
from pathlib import Path
Path("data/notes.txt").exists()
```

---

### Fichier ou dossier

**`os`**

```python
import os
os.path.isfile("data/notes.txt")
```

**`pathlib`**

```python
from pathlib import Path
Path("data/notes.txt").is_file()
```

---

## 4. Construire un chemin

**`os`**

```python
import os
chemin = os.path.join("data", "notes.txt")
```

**`pathlib`**

```python
from pathlib import Path
chemin = Path("data") / "notes.txt"
```

---

## 5. Filtrer des fichiers

**`os`**

```python
import os
[f for f in os.listdir("data") if f.endswith(".txt")]
```

**`pathlib`**

```python
from pathlib import Path
Path("data").glob("*.txt")
```

---

## 6. Création de fichiers (résumé essentiel)

### Principe fondamental

> En Python, un fichier est **créé par une opération d’écriture**.  
> `os` et `pathlib` ne font qu’**encadrer** cette opération.

---

### Créer un fichier vide

**`os`**

```python
open("data/fichier.txt", "w").close()
```

**`pathlib`**

```python
from pathlib import Path
Path("data/fichier.txt").touch()
```

---

### Créer un fichier et écrire dedans

**`os`**

```python
with open("data/fichier.txt", "w", encoding="utf-8") as f:
    f.write("Bonjour")
```

**`pathlib`**

```python
from pathlib import Path
Path("data/fichier.txt").write_text("Bonjour", encoding="utf-8")
```

---

### Créer seulement s’il n’existe pas

**`os`**

```python
import os
if not os.path.exists("data/fichier.txt"):
    open("data/fichier.txt", "w").close()
```

**`pathlib`**

```python
from pathlib import Path
Path("data/fichier.txt").touch(exist_ok=False)
```

---

## 7. Conclusion

- `os` : approche bas niveau, fonctionnelle, historique  
- `pathlib` : approche objet, lisible, cohérente  

👉 **Aujourd’hui, `pathlib` est recommandé** pour le traitement et la création de fichiers.
