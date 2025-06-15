---
# the default layout is 'page'
icon: fas fa-rectangle-history-circle-user
order: 5
---
# Projet - SoigneMoi

Ce projet est celui que j'ai réakisé à la fin de mon année de bachelor CDA (Concepteur Développeur d'Applications).
Le projet est composée de trois élémnts:
- un site web intérragi avec les patients et les soignants
- un logiciel bureautique pour les secrétaiat
- une appplication mobile pour les médecins

# Projet - SoigneMoi

Ce projet est celui que j'ai réalisé à la fin de mon année de Bachelor CDA (Concepteur Développeur d'Applications).

Le projet est composé de trois éléments :
- un site web qui permet l’interaction entre les patients et les soignants,
- un logiciel bureautique destiné au secrétariat,
- une application mobile pour les médecins.

# 1. Le site web

## Présentation

Le site est couplé à une base de données.

**Technologies utilisées :** Slim, Symfony, PHP, Twig, HTML.

J’ai commencé par utiliser Slim. J’ai dû construire le site brique par brique, ce qui m’a permis de bien comprendre la structure d’un framework.

Puis, après l’examen, j’ai souhaité remplacer Slim par Symfony. Cela m’a permis d’aller au bout du projet, en y intégrant une gestion des rôles. Symfony est tout de même plus pragmatique.

J’ai choisi d’utiliser un template Bootstrap pour soigner le rendu du site. Dans les trois premières pages, je me suis contenté de modifier le texte. Pour les quatre dernières, j’ai adapté le site **Medilab** à mon projet.

Les différents formulaires sont connectés à une base de données MySQL, où les données sont sauvegardées.

## Un peu de code

La méthode suivante permet à la secrétaire de récupérer les informations des patients sortants :

```php
// Sorties
    #[Route('/sorties', name: 'app_sorties_secretariat', methods: ['GET'])]
    //Transmission des données des patients sortant le jour même
        public function donneesSorties (Request $request) : Response
    {
        try{
            $qb = $this->emi->createQueryBuilder();
            $qb->select('p.id', 'p.prenom', 'p.nom', 'p.adressePostale')
               ->from(Sejour::class, 's')
               ->join('s.patient', 'p')
               ->Where('s.dateFin = CURRENT_DATE()');
            $query = $qb->getQuery();
            $this->donnees = $query->getResult();
            return $this->json($this->donnees);
        } catch(Exception $e){
            return new JsonResponse(["Erreur" => $e->getMessage()]);
        }
    }
    ```
    
    <img src="assets/img/site-web.png" alt="Site-web" style="max-width:300px;">


# 2.  l'applicaion "Secretariat
