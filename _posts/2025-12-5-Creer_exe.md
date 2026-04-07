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
- pycdcover.iss (voir fin du tutoriel)
- requirements.txt



# 2. fichiers exécutables créés avec pyinstaller

## 2.1 PyCDCover

- powershell (vscode)
  
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
on retrouvera l'exécutable dans le dossier "dist": pycdcover.exe.
On peut alors utiliser Inno Setup (voir 3.2)
  
  ## 2.2 PyCDCover: dans le dossier Dist: **Piveo.exe**
  
  - powershell (vscode)
    
    ```csharp
    pyinstaller --onefile --windowed `
      --icon=piveo.ico `
      --add-data "ressources;ressources" `
      --add-data "Vue;Vue" `
      --add-data "Controleur;Controleur" `
      --add-data "locales;locales" `
      --add-data "Modele;Modele" `
      piveo.pyw
    ```
  on retrouvera l'exécutable dans le dossier "dist": pycdcover.exe
  On peut alors utiliser Inno Setup (voir 3.3)

# 3. Installateur Inno Setup - uniquement pour PyCDCover

## 3.1 Introduction

Mettre "pycdcover.iss" (chaGPT - Ci-dessous) à la racine du projet windows.
Le fichier exe d'InnoSetup se retrouve dans le dossier "installer". Il s'appelle: **PyCDCover_Setup.exe** (c' est le fichier éxéctuable à distribuer 
Cliquer sur Built. 
Cliquer sur Run et suivre les instructions.



# 3.2 fichier Inno Setup (fichier: pycdcover.iss) - PycdCover

```ini
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
# 3.3 fichier Inno Setup (fichier: pycdcover.iss) - Piveo
``Ìnno Setup
; -- piveo.iss --
; Script Inno Setup pour Piveo

[Setup]
AppName=Piveo
AppVersion=2.3.0
AppPublisher=Gérard LE REST
AppPublisherURL=https://github.com/gerardlerest
AppSupportURL=https://github.com/gerardlerest
AppUpdatesURL=https://github.com/gerardlerest

DefaultDirName={autopf}\Piveo
DefaultGroupName=Piveo
OutputDir=installer
OutputBaseFilename=Piveo_Setup
Compression=lzma
SolidCompression=yes

; Icône de l’installateur (facultatif)
; SetupIconFile=icon.ico

[Languages]
Name: "french"; MessagesFile: "compiler:Languages\French.isl"

[Files]
; Exécutable principal
Source: "dist\piveo.exe"; DestDir: "{app}"; Flags: ignoreversion

; Tous les fichiers générés par PyInstaller
Source: "dist\*"; DestDir: "{app}"; Flags: recursesubdirs createallsubdirs ignoreversion

[Icons]
; Raccourci menu démarrer
Name: "{group}\Piveo"; Filename: "{app}\piveo.exe"

; Raccourci bureau
Name: "{commondesktop}\Piveo"; Filename: "{app}\piveo.exe"; Tasks: desktopicon

[Tasks]
Name: "desktopicon"; Description: "Créer une icône sur le bureau"; GroupDescription: "Options supplémentaires"

[Run]
Filename: "{app}\piveo.exe"; Description: "Lancer Piveo"; Flags: nowait postinstall skipifsilent
```
