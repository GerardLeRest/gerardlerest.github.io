---
# the default layout is 'page'
title: Projet SoigneMoi
icon: fas fa-wrench
order: 5
---

Ce projet est celui que j’ai réalisé à la fin de mon année de bachelor CDA (Concepteur Développeur d’Applications).

Le projet est composé de trois éléments :

- un site web qui permet l’interaction entre les patients et les soignants ;
- un logiciel bureautique destiné au secrétariat ;
- une application mobile pour les médecins.

# 1. Le site web 

## Présentation  

Le site est couplé à une base de données.

J’ai commencé par utiliser Slim. J’ai dû construire le site brique après brique, ce qui m’a permis de bien comprendre la structure d’un framework.

Puis, après l’examen, j’ai souhaité remplacer Slim par Symfony. Cela m’a permis d’aller au bout du projet en y intégrant une gestion des rôles. Symfony est tout de même plus pragmatique.

J’ai choisi d’utiliser un template Bootstrap pour soigner le rendu du site. Dans les trois premières pages, je me suis contenté de modifier le texte. Pour les quatre dernières, j’ai adapté le site **Medilab** à mon projet.

Les différents formulaires sont connectés à une base de données MySQL, où les données sont enregistrées.

## Un peu de code

La méthode suivante permet à la secrétaire de récupérer les informations des patients sortants :

```php
// Sorties
// Transmission des données des patients qui sortent le jour même
#[Route('/sorties', name: 'app_sorties_secretariat', methods: ['GET'])]
public function donneesSorties(Request $request): Response
{
    try {
        $qb = $this->emi->createQueryBuilder();
        $qb->select('p.id', 'p.prenom', 'p.nom', 'p.adressePostale')
           ->from(Sejour::class, 's')
           ->join('s.patient', 'p')
           ->where('s.dateFin = CURRENT_DATE()');
        $query = $qb->getQuery();
        $this->donnees = $query->getResult();
        return $this->json($this->donnees);
    } catch (Exception $e) {
        return new JsonResponse(["Erreur" => $e->getMessage()]);
    }
}
```
## Technologies 

Lanages: PHP, HTML, Twig, CSS

Frameworks : Slim, Symfony

## Page d’accueil 

![Site web](assets/img/site_web.png)

# 2. L'application « Secrétariat »
## Présentation
Cette application permet aux secrétaires d'obtenir des informations sue les patients entrants ou sortants. Les identités s'affichent dans des fenêtres. Pour avoir des informations plus détaillées, il suffit de cliquer sur la ligne du patient.
## Un peu de code
Cette application permet aux secrétaires d'obtenir des informations sur les patients entrants ou sortants. Les identités s'affichent dans des fenêtres. Pour avoir des informations plus détaillées, il suffit de cliquer sur la ligne du patient.
```python
def identite(self) -> None:
        """Appelée quand l'utilisateur sélectionne une ligne"""
        selected_items = self.table.selectedItems()
        if not selected_items or len(selected_items) < 3:
            return

        id_text = selected_items[0].text().strip()
        id = int(id_text)
        print("ID sélectionné :", id)
        prenom = selected_items[1].text()
        nom = selected_items[2].text()
        identite = f"{prenom} {nom}"
       
        details = AffichageDetails(identite, id) #None : séparer la fenêtre d'application et cette fenêtre détails
        details.setWindowFlag(Qt.Window)  # Pour une vraie fenêtre indépendante
        details.show()
        details.exec()
```
## technologie
python, json, pyside6, pillow, traitement fichiers

## vue des interfaces
![Secretariat](assets/img/secretariat.png)
