---
title: Installer un exe
author: Gérard LE REST
date: 2025-12-05 16:40:00 +0800
categories: [Windows, Tutoriel]
tags: [exe, PyInstaller, Inno Setup]
---

# 1. Constitution du dossier "PyCDCover-Windows"

- Vue
- Controleur
- locales
- Modele
- ressources
- icone.ico
- pycdcover.pyw
- pycdcover.iss
- requirements.txt

# 2. Création du premier exécutable dans dist

- cmd:
  
  ```nginx
  pyinstaller --onefile --windowed ^
    --icon=icone.ico ^
    --add-data "ressources;ressources" ^
    --add-data "Vue;Vue" ^
    --add-data "Controleur;Controleur" ^
    --add-data "locales;locales" ^
    --add-data "Modele;Modele" ^
    pycdcover.pyw
  ```

- powershell:
  
  ```csharp
  pyinstaller --onefile --windowed `
    --icon=icone.ico `
    --add-data "ressources;ressources" `
    --add-data "Vue;Vue" `
    --add-data "Controleur;Controleur" `
    --add-data "locales;locales" `
    --add-data "Modele;Modele" `
    pycdcover.pyw
  ```

# 3 Installateur Inno Setup

Mettre pycdcover.iss à la racine du projet windows.
Cliquer sur build et suivre les instructions

Le fichier "PyCDCover-Setup.exe" final est dans le dossier "output"
