---
# the default layout is 'page'

title: Projet SoigneMoi
icon: fas fa-wrench
order: 5

---

Ce projet est celui que j’ai réalisé à la fin de mon année de bachelor CDA (Concepteur Développeur d’Applications).

Le projet est composé de trois applications :

- un site web qui permet l’interaction entre les patients et les soignants ;

- un logiciel bureautique destiné au secrétariat ;

- une application mobile pour les médecins. 

![chirugien](assets/img/soignemoi-chirurgiens.png)

## 1. Le site internet "SoigneMoi"

### Présentation

Le site est couplé à une base de données MySQL.

J’ai commencé par utiliser Slim. J’ai dû construire le site brique après brique, ce qui m’a permis de bien comprendre la structure d’un framework.

Puis, après l’examen, j’ai souhaité remplacer Slim par Symfony. Cela m’a permis d’aller au bout du projet en y intégrant une gestion des rôles. Symfony est tout de même plus pragmatique.

J’ai choisi d’utiliser un template Bootstrap pour soigner le rendu du site. Dans les trois premières pages, je me suis contenté de modifier le texte. Pour les quatre dernières, j’ai adapté le site **Medilab** à mon projet.

Les différents formulaires sont connectés à une base de données MySQL, où les données sont enregistrées.

### Un peu de code

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

### Technologies

Langages: PHP, HTML, Twig, CSS, MySQL

Frameworks : Slim, Symfony

### Page d’accueil

![Site web](assets/img/soignemoi-site_web.png)

### Conclusion

les deux framework utilisés ont eu leur fonction, le premier (Slim) pour comprendre la construction d'un framework, le deuxième m'a montré un outil plus simple. Dans ma première version, je ne suis pas arrivé à gérer les notions de rôles, ce que Symfony m'a permis de le faire.
Cette partie a été riche en apprentissage.

## 2. L'application « Secrétariat »

### Présentation

Cette application permet aux secrétaires d'obtenir des informations sue les patients entrants ou sortants. Les identités s'affichent dans des fenêtres. Pour avoir des informations plus détaillées, il suffit de cliquer sur la ligne du patient.

### Un peu de code

Cette application permet aux secrétaires d'obtenir des informations sur les patients entrants ou sortants. Les identités s'affichent dans des fenêtres. Pour avoir des informations plus détaillées, il suffit de cliquer sur la ligne du patient.

```python
def identite(self) -> None:
        """Appelée quand l'utilisateur sélectionne une ligne"""
        selected_items = self.table.selectedItems()
        if not selected_items or len(selected_items) < 3:
            return

        id_text = selected_items[0].text().strip()
        id = int(id_text)
        prenom = selected_items[1].text()
        nom = selected_items[2].text()
        identite = f"{prenom} {nom}"

        details = AffichageDetails(identite, id)  # Fenêtre de détails du patient
        details.setWindowFlag(Qt.Window)  # Pour une vraie fenêtre indépendante
        details.show() # affichage de la fentre de détails du patient
        details.exec() # blocage de la fennêtre parente
```

### Technologie

python, json, pyside6, pillow, Mysql, traitement de fichiers

### vue des interfaces

![Secretariat](assets/img/soignemoi-secretariat.png)

## 3. Application "Medecin"

### Présentation

Cette application mobile a été développée avec Java pour Android. Elle permet à un médecin de fournir des avis et des prescriptios pour un patient.

### un peu de code

Voici la construction des valeurs de "Prescriptions":

```java
private void valider() {
        // Récupérer les valeurs des EditText
        String texteNomMedicament = nomMedicament.getText().toString();
        String textePosologie = posologie.getText().toString();
        String texteDateDeDebut = dateDeDebut.getText().toString();
        String texteDateDeFin = dateDeFin.getText().toString();

        String messageErreur = "";
        if (texteNomMedicament.isEmpty() 
                || textePosologie.isEmpty() 
                || texteDateDeDebut.isEmpty()
                || texteDateDeFin.isEmpty()) {
            messageErreur = "Au moins un des champs n'a pas été saisi.";
        }

        if (!messageErreur.isEmpty()) {
            int duration = Toast.LENGTH_SHORT; //durée standart
            Toast toast = Toast.makeText(ActivitePrescription.this, messageErreur, duration);
            toast.show();
        } else {
            // Remplissage du tableauPrescriptions
            tableauPrescription.put("nomMedicament", texteNomMedicament);
            tableauPrescription.put("posologie", textePosologie);
            tableauPrescription.put("dateDeDebut", texteDateDeDebut);
            tableauPrescription.put("dateDeFin", texteDateDeFin);

            // récupération de l'intent de l'activité Avis
            Intent intent = getIntent(); //deux valeurs enoyés pas "Avis""

            // ajouter les deux clés étrangères
            // récupérer les valeurs de l'activité Avis
            if (intent != null){
                idMedecin = intent.getStringExtra("idMedecin");
                idPatient = intent.getStringExtra("idPatient");
                if (idMedecin!=null && idPatient!=null) {
                    tableauPrescription.put("idMedecin", idMedecin);
                    tableauPrescription.put("idPatient", idPatient);
                }
            }

                transfertJSON(); // transférer les données
        }
    }
```

### Technologie

Java pour Android, MySQL

### Vues des trois pages de l'application

![medecin](assets/img/soignemoi-medecin.png)

### Conclusion

Android pour java est assez facile à prendre en mains. La partie réseau est tout même complexe avec des outils de dépannage pas forcément convaincant. Mais le rendu final est plutôt satisfaisant.

## 4. Liens
github: [Soignemoi-Symfony](https://github.com/GerardLeRest/soignemoi-symfony) <br>
site internet: [soignemoi.net](https://www.soignemoi.net)

*: image des chirurgiens -   izhar-ahamed - pixabay
