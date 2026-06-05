---
title: PHP – Résumé pratique
author: Gérard LE REST
date: 2026-05-13 11:30:00 +0800
categories: [PHP, Cours]
tags: [php, backend]
---

# 📄 PHP – Résumé pratique (bases du langage)

## 🔹 Qu’est-ce que PHP ?

PHP est un langage de programmation.

Il permet notamment de :

- manipuler des données
- utiliser des tableaux
- créer des fonctions
- programmer en objet
- automatiser des traitements

➡️ PHP est simple pour débuter  
➡️ Très utilisé dans le développement back-end

---

# 🔹 Structure minimale

```php
<?php

echo "Bonjour";
```

---

# 🔹 Variables

```php
<?php

$nom = "Gérard";
$age = 56;

echo $nom;
```

➡️ Une variable PHP commence toujours par `$`.

---

# 🔹 Types courants

| PHP    | Description    |
| ------ | -------------- |
| string | texte          |
| int    | entier         |
| float  | nombre décimal |
| bool   | vrai / faux    |
| array  | tableau        |

---

# 🔹 Concaténation

```php
<?php

$nom = "Gérard";

echo "Bonjour " . $nom;
```

---

# 🔹 Conditions (if...else if...else)

```php
<?php

$age = 18;

if ($age >= 18) {

    echo "Majeur";
}
else {

    echo "Mineur";
}
```

---

# 🔹 Boucle while

```php
<?php

$i = 1;

while ($i <= 5) {

    echo $i;

    $i++;
}
```

---

# 🔹 Boucle for

```php
<?php

for ($i = 1; $i <= 5; $i++) {

    echo $i;
}
```

---

# 🔹 Tableaux simples

```php
<?php

$couleurs = ["rouge", "vert", "bleu"];

echo $couleurs[0];
```

---

# 🔹 Ajouter un élément dans un tableau

```php
<?php

$couleurs = ["rouge", "vert"];

$couleurs[] = "bleu";

print_r($couleurs);
```

---

# 🔹 Retirer un élément d’un tableau

```php
<?php

$couleurs = ["rouge", "vert", "bleu"];

unset($couleurs[1]);

print_r($couleurs);
```

---

# 🔹 Nombre d’éléments d’un tableau

```php
<?php

$couleurs = ["rouge", "vert", "bleu"];

echo count($couleurs);
```

---

# 🔹 Tableau associatif

```php
<?php

$personne = [

    "nom" => "LE REST",
    "prenom" => "Gérard"
];

echo $personne["nom"];
```

---

# 🔹 Ajouter une valeur dans un tableau associatif

```php
<?php

$personne = [

    "nom" => "LE REST"
];

$personne["prenom"] = "Gérard";

print_r($personne);
```

---

# 🔹 Modifier une valeur

```php
<?php

$personne = [

    "nom" => "LE REST"
];

$personne["nom"] = "DUPONT";

print_r($personne);
```

---

# 🔹 Retirer une valeur

```php
<?php

$personne = [

    "nom" => "LE REST",
    "prenom" => "Gérard"
];

unset($personne["prenom"]);

print_r($personne);
```

➡️ `unset()` permet de supprimer une clé du tableau associatif.

---

# 🔹 Foreach

```php
<?php

$couleurs = ["rouge", "vert", "bleu"];

foreach ($couleurs as $couleur) {

    echo $couleur;
}
```

---

# 🔹 Fonctions

```php
<?php

function addition($a, $b) {

    return $a + $b;
}

$resultat = addition(5, 3);

echo $resultat;
```

---

# 🔹 Typage simple

```php
<?php

function addition(int $a, int $b): int {

    return $a + $b;
}
```

---

# 🔹 Inclusion de fichiers

```php
<?php

require "fonctions.php";
```

---

# 🔹 Classe simple

```php
<?php

class Patient {

    public string $nom;
}
```

---

# 🔹 Constructeur

```php
<?php

class Patient {

    public string $nom;

    public function __construct(string $nom) {

        $this->nom = $nom;
    }
}
```

---

# 🔹 Création d’objet

```php
<?php

$patient = new Patient("Dupont");

echo $patient->nom;
```

---

# 🔹 Méthode

```php
<?php

class Patient {

    public function direBonjour(): void {

        echo "Bonjour";
    }
}
```

---

# 🔹 Héritage

```php
<?php

<?php

class Personne {

    public string $nom;

    // Constructeur de la classe parent
    public function __construct(string $nom) {

        $this->nom = $nom;
    }
}

class Patient extends Personne {

    // Constructeur de la classe enfant
    public function __construct(string $nom) {

        // Appel du constructeur parent
        parent::__construct($nom);
    }
}

// Création d'un patient
$patient = new Patient("Dupont");

echo $patient->nom;
```

---

# 🔹 Interface

```php
<?php

interface Affichable {

    public function afficher(): void;
}
```

Implémentation :

```php
<?php

class Patient implements Affichable {

    public function afficher(): void {

        echo "Patient";
    }
}
```

---

# 🔹 Namespace

```php
<?php

namespace App\Entity;
```

---

# 🔹 Utilisation d’une classe

```php
<?php

use App\Entity\Patient;
```

---

# 🔹 À retenir

Le plus important en PHP :

- variables
- conditions
- boucles
- tableaux
- fonctions
- programmation objet
- héritage
- interfaces

➡️ Le web, les formulaires, PDO et Symfony viendront ensuite.
