---
title: Installer une Appimage
author: Gérard LE REST
date: 2025-12-08 20:00:00 +0800
categories: [Linux, Tutoriel]
tags: [AppImage]
---

# 1 Installation

- créer le dossier "PyCdCover-appimage. Y enclure:

- ### **Dossiers à inclure dans AppDir**
  
  | Dossier         | Pourquoi ?                                          |
  | --------------- | --------------------------------------------------- |
  | **Controleur/** | Contient le contrôleur du programme.                |
  | **Modele/**     | Contient les classes métier (PDF, gabarit…).        |
  | **Vue/**        | Interface graphique PySide6.                        |
  | **ressources/** | Images, templates, fichiers utilisés à l’exécution. |
  
  ### **📄 Fichiers à inclure**
  
  | Fichier              | Utilité                                              |
  | -------------------- | ---------------------------------------------------- |
  | **pycdcover.py**     | Script principal qui lance l’application.            |
  | **pycdcover.png**    | Icône de l’application (pour l’AppImage).            |
  | **LICENSE.md**       | Obligatoire dans un paquet si tu veux le distribuer. |
  | **README.md**        | Recommandé mais pas obligatoire.                     |
  | **requirements.txt** | liste des dépendances                                |
  
  | Fichier                         | Utilité                                                                                   |
  | ------------------------------- |:----------------------------------------------------------------------------------------- |
  | **build_appimage.sh**           | script maison qui pilote toute la construction                                            |
  | **linuxdeploy-x86_64.AppImage** | téléchargeable<br/>fabrique l’AppImage PyCDCover_2.0.0_x86_64.AppImage à la fin du script |

- Rendre exécutable "linuxdeploy-x86_64.Appimage":
  
  ```bash
  chmod +x linuxdeploy-x86_64.AppImage
  ```

- Rendre exécutable "build_appimage.sh":

- ```bash
  chmod +x build_appimage.sh
  ```

- exécuter "build_appimage.sh":
  
  ```bash
  ./build_appimage.sh
  ```
  
  l'AppImage est construite. La rendre exécutable:
  
  ```bash
  chmod +x PyCDCover_2.0.0_x86_64.AppImage
  ```
  
  et puis l'exécuter:
  
  ```bash
  ./PyCDCover_2.0.0_x86_64.AppImage
  ```
  
  # 2 intégration dans Ubuntu
  
  ```bash
  sudo mkdir -p /opt/PyCDCover
  ```
  
  ```bash
  sudo cp PyCDCover_2.0.0_x86_64.AppImage /opt/PyCDCover/
  ```
  
  ```bash
  sudo chmod +x /opt/PyCDCover/PyCDCover_2.0.0_x86_64.AppImage
  ```
  
  # 3 Installation de l'icone

- ```
  chmod +x build_appimage.sh
  ```

Utiliser alacarte sous ubuntu pour construire l'icone.
