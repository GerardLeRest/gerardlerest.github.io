---
title: Symfony – Les tests
author: Gérard LE REST
date: 2026-06-03 13:00:00 +0800
categories: [Symfony, Cours]
tags: [symfony, tests, phpunit]
---

# Cours 38 — Les tests

## Introduction

Les tests permettent de vérifier automatiquement le bon fonctionnement d'une application.

Symfony utilise principalement PHPUnit.

---

## Créer un test

Commande :

```bash
php bin/console make:test
```

Symfony demande :

```text
What kind of test do you want ?
```

---

## Exemple de test

```php
namespace App\Tests;

use PHPUnit\Framework\TestCase;

class CalculTest extends TestCase
{
    public function testAddition(): void
    {
        $resultat = 2 + 3;

        $this->assertEquals(
            5,
            $resultat
        );
    }
}
```

---

## Lancer les tests

```bash
php bin/phpunit
```

---

## Vérifier une valeur

```php
$this->assertEquals(
    5,
    $resultat
);
```

---

## Vérifier qu'une valeur existe

```php
$this->assertNotNull(
    $patient
);
```

---

## Vérifier un booléen

```php
$this->assertTrue(
    $resultat
);
```

---

## Exemple simple

```php
public function testPatientExiste(): void
{
    $patient = new Patient();

    $this->assertNotNull(
        $patient
    );
}
```

---

## Comprendre le processus

```text
Test
↓
Exécution
↓
Vérification
↓
Succès ou échec
```

---

## Pourquoi tester ?

Permet de :

- détecter les erreurs ;
- sécuriser les modifications ;
- vérifier le fonctionnement du code ;
- faciliter la maintenance.

---

## Conclusion

Les tests vérifient automatiquement le fonctionnement d'une application.

Éléments à retenir :

```bash
php bin/console make:test

php bin/phpunit
```

Méthodes fréquentes :

```php
assertEquals()

assertNotNull()

assertTrue()
```
