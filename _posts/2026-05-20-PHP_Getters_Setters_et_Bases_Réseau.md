---
title: PHP – Getters, Setters et Bases Réseau
author: Gérard LE REST
date: 2026-05-20 16:00:00 +0800
categories: [PHP, Cours]
tags: [PHP, Backend]
---

# Cours PHP — Getters, Setters et Bases Réseau

## 1. Introduction

En PHP orienté objet, les getters et setters permettent de protéger les données d’une classe.

Ils servent à :

- lire une valeur privée,
- modifier une valeur privée,
- contrôler les données,
- rendre le code plus propre et sécurisé.

---

# 2. Classe simple

```php
<?php

class Personne {

    public string $nom;

    public function __construct(string $nom)
    {
        $this->nom = $nom;
    }

    public function afficherNom()
    {
        echo $this->nom;
    }
}
```

## Explications

- `class Personne` : création d’une classe.
- `public string $nom` : propriété publique.
- `__construct()` : constructeur.
- `$this` : représente l’objet courant.

---

# 3. Pourquoi utiliser private ?

Si une propriété est publique, tout le monde peut la modifier.

Exemple dangereux :

```php
$personne->nom = "";
```

On préfère donc :

```php
private string $nom;
```

---

# 4. Les Getters

Un getter permet de lire une propriété privée.

```php
<?php

class Personne {

    private string $nom;

    public function __construct(string $nom)
    {
        $this->nom = $nom;
    }

    public function getNom(): string
    {
        return $this->nom;
    }
}
```

## Utilisation

```php
$personne = new Personne("Paul");

echo $personne->getNom();
```

---

# 5. Les Setters

Un setter permet de modifier une propriété privée.

```php
<?php

class Personne {

    private string $nom;

    public function setNom(string $nom): void
    {
        $this->nom = $nom;
    }
}
```

## Utilisation

```php
$personne->setNom("Jean");
```

---

# 6. Getters et Setters complets

```php
<?php

class Personne {

    private string $nom;

    public function __construct(string $nom)
    {
        $this->nom = $nom;
    }

    public function getNom(): string
    {
        return $this->nom;
    }

    public function setNom(string $nom): void
    {
        $this->nom = $nom;
    }
}
```

---

# 7. Validation dans un Setter

Le setter peut vérifier les données (parfois très sensibles qui ne doivent pas être mofiiées directement.

```php
public function setNom(string $nom): void
{
    if(strlen($nom) > 2)
    {
        $this->nom = $nom;
    }
}
```

---

# 8. Les bases réseau en PHP

PHP est très utilisé pour :

- les sites web,
- les API,
- les formulaires,
- les échanges client/serveur.

---

# 9. Le principe client / serveur

## Client

Le navigateur :

- Chrome,
- Firefox,
- Edge.

## Serveur

Machine qui exécute PHP :

- Apache,
- Nginx,
- serveur Symfony.

---

# 10. Fonctionnement d’une requête

1. Le navigateur envoie une requête.
2. Le serveur reçoit la requête.
3. PHP exécute le code.
4. Le serveur renvoie du HTML.

---

# 11. Les variables GET

Les données peuvent être envoyées dans l’URL.

```text
http://localhost/index.php?nom=Paul
```

## Récupération

```php
<?php

echo $_GET['nom'];
```

---

# 12. Les formulaires POST

## HTML

```html
<form method="POST">
    <input type="text" name="nom">
    <button>Envoyer</button>
</form>
```

## PHP

```php
<?php

echo $_POST['nom'];
```

---

# 13. Connexion à une base MySQL avec PDO

```php
<?php

$pdo = new PDO(
    "mysql:host=localhost;dbname=test",
    "root",
    ""
);
```

---

# 14. Requête préparée

```php
<?php

$requete = $pdo->prepare(
    "SELECT * FROM users WHERE nom = ?"
);

$requete->execute([$nom]);
```

---

# 15. Résumé

## Getters

- lisent les données.

## Setters

- modifient les données,
- contrôlent les valeurs.

## PHP Réseau

- reçoit des requêtes HTTP,
- communique avec un navigateur,
- échange avec une base de données.

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
