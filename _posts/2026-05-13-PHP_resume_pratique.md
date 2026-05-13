---
title: PHP – Résumé pratique
author: Gérard LE REST
date: 2025-05-13 11:30:00 +0800
categories: [PHP, Cours]
tags: [PHP, Backend]
---

# 📄 PHP – Résumé pratique (usage courant)

## 🔹 Qu’est-ce que PHP ?

**PHP** est un langage principalement utilisé pour :

- les sites web dynamiques
- les formulaires
- les bases de données
- les API
- le back-end

➡️ Très utilisé sur le web  
➡️ Intégré facilement avec HTML  
➡️ Simple pour débuter

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

| PHP | Description |
| --- | --- |
| string | texte |
| int | entier |
| float | nombre décimal |
| bool | vrai / faux |
| array | tableau |

---

# 🔹 Concaténation

```php
<?php

$nom = "Gérard";

echo "Bonjour " . $nom;
```

---

# 🔹 Conditions

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

# 🔹 Foreach

```php
<?php

$couleurs = ["rouge", "vert", "bleu"];

foreach ($couleurs as $couleur) {

    echo $couleur;
}
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

# 🔹 GET

La méthode **GET** permet d’envoyer des données dans l’URL.

Exemple :

```text
http://localhost/test.php?nom=Dupont
```

---

# 🔹 Récupération GET

```php
<?php

$nom = $_GET["nom"];

echo $nom;
```

---

# 🔹 POST

La méthode **POST** permet d’envoyer des données de formulaire.

---

# 🔹 Formulaire HTML

```html
<form method="POST">

    <input type="text" name="nom">

    <button type="submit">
        Valider
    </button>

</form>
```

---

# 🔹 Récupération POST

```php
<?php

$nom = $_POST["nom"];

echo $nom;
```

---

# 🔹 Sécurisation minimale

```php
<?php

$nom = htmlspecialchars($_POST["nom"]);
```

➡️ Évite l’injection HTML ou JavaScript.

---

# 🔹 Session

```php
<?php

session_start();

$_SESSION["nom"] = "Gérard";
```

---

# 🔹 PDO – Connexion MySQL

```php
<?php

$pdo = new PDO(

    "mysql:host=localhost;dbname=test;charset=utf8",
    "root",
    ""
);
```

---

# 🔹 SELECT

```php
<?php

$requete = $pdo->query(

    "SELECT * FROM patient"
);

$patients = $requete->fetchAll();
```

---

# 🔹 Requête préparée

```php
<?php

$requete = $pdo->prepare(

    "SELECT * FROM patient
    WHERE nom = ?"
);

$requete->execute([$nom]);

$patient = $requete->fetch();
```

➡️ Protection contre les injections SQL.

---

# 🔹 INSERT

```php
<?php

$requete = $pdo->prepare(

    "INSERT INTO patient(nom)
    VALUES(?)"
);

$requete->execute([$nom]);
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

class Personne {

    public string $nom;
}

class Patient extends Personne {

}
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

# 🔹 Symfony et GET / POST

Avec Symfony, on utilise généralement l’objet `Request`.

GET :

```php
$id = $request->query->get("id");
```

POST :

```php
$nom = $request->request->get("nom");
```

➡️ Symfony simplifie la manipulation des requêtes HTTP.

---

# 🔹 À retenir

> PHP est surtout un langage de logique serveur.

Le plus important :

- tableaux
- fonctions
- GET / POST
- PDO
- objet
- interfaces
- code simple et lisible

Le reste viendra naturellement avec les projets.
