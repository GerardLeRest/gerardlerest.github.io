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

# 2. Création du premier exécutable dans dist - PyCDCover

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

Mettre "pycdcover.iss" (chaGPT - Ci-dessous) à la racine du projet windows.
Cliquer sur Built. Le fichier exe d'InnoSetup est dans le dossier "installer". 

Cliquer sur Run et suivre les instructions.

# 4 fichier Inno Setup (ex pycdcover.iss

```ìss
; -- pycdcover.iss --
; Script Inno Setup pour PyCDCover

[Setup]
AppName=PyCDCover
AppVersion=1.0.0
AppPublisher=Gérard LE REST
AppPublisherURL=https://github.com/gerardlerest
AppSupportURL=https://github.com/gerardlerest
AppUpdatesURL=https://github.com/gerardlerest

DefaultDirName={autopf}\PyCDCover
DefaultGroupName=PyCDCover
OutputDir=installer
OutputBaseFilename=PyCDCover_Setup
Compression=lzma
SolidCompression=yes

; Icône de l’installateur (facultatif)
; SetupIconFile=icon.ico

[Languages]
Name: "french"; MessagesFile: "compiler:Languages\French.isl"

[Files]
; Exécutable principal
Source: "dist\pycdcover\pycdcover.exe"; DestDir: "{app}"; Flags: ignoreversion

; Tous les fichiers générés par PyInstaller
Source: "dist\pycdcover\*"; DestDir: "{app}"; Flags: recursesubdirs createallsubdirs ignoreversion

[Icons]
; Raccourci menu démarrer
Name: "{group}\PyCDCover"; Filename: "{app}\pycdcover.exe"

; Raccourci bureau
Name: "{commondesktop}\PyCDCover"; Filename: "{app}\pycdcover.exe"; Tasks: desktopicon

[Tasks]
Name: "desktopicon"; Description: "Créer une icône sur le bureau"; GroupDescription: "Options supplémentaires"

[Run]
Filename: "{app}\pycdcover.exe"; Description: "Lancer PyCDCover"; Flags: nowait postinstall skipifsilent

```
