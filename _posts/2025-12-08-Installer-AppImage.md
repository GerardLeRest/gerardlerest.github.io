---
title: Installer une Appimage
author: Gérard LE REST
date: 2025-12-08 20:00:00 +0800
categories: [Linux, Tutoriel]
tags: [AppImage]

---

# 1 Installation  (ex: PyCDCover)

- créer le dossier "PyCdCover-AppImage. Y enclure:

- ### **Dossiers à inclure dans AppDir**
  
  | Dossier         | Pourquoi ?                                          |
  | --------------- | --------------------------------------------------- |
  | **Controleur/** | Contient le contrôleur du programme.                |
  | **locales/**    | locales (langues)                                   |
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
  
  | Fichier        | Utilité                                        |
  | -------------- |:---------------------------------------------- |
  | **install.sh** | script maison qui pilote toute la construction |
  
  REMARQUE - Important: pour Piveo, il ne faut pas intégrer les dossiers *.JSON, les .db, le dossier "fichiers.
  
  - Rendre exécutable "install.sh":
    
    ```bash
    chmod +x install.sh
    ```

- exécuter "install.sh":
  
  ```bash
  ./install.sh
  ```
  
  l'AppImage est construite. La rendre exécutable:
  
  ```bash
  chmod +x PyCDCover-x86_64.AppImage
  ```
  
  et puis l'exécuter:
  
  ```bash
  ./PyCDCover-x86_64.AppImage
  ```
  
  # 2 intégration dans Ubuntu
  
  ```bash
  sudo mkdir -p /opt/PyCDCover
  ```
  
  ```bash
  sudo cp PyCDCover-x86_64.AppImage /opt/PyCDCover/
  ```
  
  ```bash
  sudo chmod +x /opt/PyCDCover/PyCDCover-x86_64.AppImage
  ```

# Alacarte

Alacarte permet de créer un exécutable sur les bureaux GNU/Linux

# 4 Effacement

- Effacer l'appimage:
  
  ```bash
  sudo rm /opt/PyCDCover/PyCDCover-x86_64.AppImage
  ```

- (Optionnel) Nettoyer le cache d’icônes
  
  ```bash
  update-desktop-database ~/.local/share/applications/
  ```

# 5 Scripts "Install.sh

## 5.1  Script "Install.sh - PyCDCover

```bash
#!/bin/bash
set -e

APP=PyCDCover
ARCH=x86_64
APPDIR=AppDir
PYTHON=python3

echo "== PyCDCover AppImage builder =="

# 1) Nettoyage
rm -rf "$APPDIR"
rm -f "$APP-$ARCH.AppImage"

# 2) Arborescence AppDir
mkdir -p "$APPDIR/usr/bin"
mkdir -p "$APPDIR/usr/lib/python3/site-packages"

# 3) Copie du projet
cp -r \
    Controleur \
    Modele \
    Vue \
    locales \
    ressources \
    pycdcover.py \
    pycdcover.png \
    "$APPDIR/"

# 4) Exécutable principal (point d’entrée unique)
cat > "$APPDIR/usr/bin/pycdcover" <<'EOF'
#!/bin/bash
HERE="$(dirname "$(readlink -f "$0")")"
export PYTHONPATH="$HERE/../lib/python3/site-packages:$HERE/../.."
exec python3 "$HERE/../../pycdcover.py"
EOF
chmod +x "$APPDIR/usr/bin/pycdcover"

# 5) AppRun
cat > "$APPDIR/AppRun" <<'EOF'
#!/bin/bash
HERE="$(dirname "$(readlink -f "$0")")"
exec "$HERE/usr/bin/pycdcover"
EOF
chmod +x "$APPDIR/AppRun"

# 6) Fichier .desktop
cat > "$APPDIR/PyCDCover.desktop" <<EOF
[Desktop Entry]
Type=Application
Name=PyCDCover
Exec=pycdcover
Icon=pycdcover
Categories=Audio;Utility;
Terminal=false
EOF

# 7) Icône
cp pycdcover.png "$APPDIR/"

# 8) Dépendances Python
$PYTHON -m pip install -r requirements.txt \
  --target "$APPDIR/usr/lib/python3/site-packages" \
  --break-system-packages \
  --disable-pip-version-check

# 9) appimagetool
if [ ! -f appimagetool-x86_64.AppImage ]; then
  wget https://github.com/AppImage/AppImageKit/releases/download/continuous/appimagetool-x86_64.AppImage
  chmod +x appimagetool-x86_64.AppImage
fi

# 10) Création AppImage
ARCH=$ARCH ./appimagetool-x86_64.AppImage "$APPDIR"

echo "✅ AppImage générée : $APP-$ARCH.AppImage"
```

## 5.2  Script "Install.sh - PyCDCover

```bash
#!/bin/bash
set -e

APP=Piveo
ARCH=x86_64
APPDIR=AppDir
PYTHON=python3

echo "== Piveo AppImage builder =="

# 1) Nettoyage
rm -rf "$APPDIR"
rm -f "$APP-$ARCH.AppImage"

# 2) Arborescence AppDir
mkdir -p "$APPDIR/usr/bin"
mkdir -p "$APPDIR/usr/lib/python3/site-packages"

# 3) Copie du projet
cp \
    Piveo.pyw \
    FenetrePrincipale.py \
    ChoixOrganisme.py \
    FrameGauche.py \
    FrameDroiteHaute.py \
    FrameDroiteBasse.py \
    GestionLangue.py \
    ModifierBDD.py \
    utils.py \
    utils_i18n.py \
    "$APPDIR/"

cp -r locales "$APPDIR/"

# 4) Exécutable principal (POINT D’ENTRÉE UNIQUE)
cat > "$APPDIR/usr/bin/piveo" <<'EOF'
#!/bin/bash
HERE="$(dirname "$(readlink -f "$0")")"

export PYTHONPATH="$HERE/../lib/python3/site-packages:$HERE/../.."

exec python3 "$HERE/../../Piveo.pyw"
EOF
chmod +x "$APPDIR/usr/bin/piveo"

# 5) AppRun
cat > "$APPDIR/AppRun" <<'EOF'
#!/bin/bash
HERE="$(dirname "$(readlink -f "$0")")"
exec "$HERE/usr/bin/piveo"
EOF
chmod +x "$APPDIR/AppRun"

# 6) Desktop
cat > "$APPDIR/Piveo.desktop" <<EOF
[Desktop Entry]
Type=Application
Name=Piveo
Exec=piveo
Icon=piveo
Categories=Education;Utility;
Terminal=false
EOF

# 7) Icône
cp piveo.png "$APPDIR/"

# 8) Dépendances Python
$PYTHON -m pip install PySide6 \
  --target "$APPDIR/usr/lib/python3/site-packages" \
  --break-system-packages \
  --disable-pip-version-check

# 9) appimagetool
if [ ! -f appimagetool-x86_64.AppImage ]; then
  wget https://github.com/AppImage/AppImageKit/releases/download/continuous/appimagetool-x86_64.AppImage
  chmod +x appimagetool-x86_64.AppImage
fi

# 10) Création AppImage
ARCH=$ARCH ./appimagetool-x86_64.AppImage "$APPDIR"

echo "✅ AppImage générée : $APP-$ARCH.AppImage"
```
