[← Retour à la documentation](../) · [← Prérequis](requirements)

# Installation du core (Windows)

Assure-toi d'avoir installé tout ce qui est listé sur la page [Prérequis](requirements) avant de commencer.

## 1. Récupérer les sources

1. Crée un dossier pour cloner les sources, par exemple `C:\UniverseEmu`.
2. Clic droit sur le dossier → **Git Extensions → Clone**.
3. URL du repository : `https://github.com/AzerothUniverseCore/UniverseEmu.git`
4. Clique sur **Clone**. Toutes les sources sont récupérées dans `C:\UniverseEmu`.

(Tu peux aussi cloner en ligne de commande : `git clone https://github.com/AzerothUniverseCore/UniverseEmu.git`.)

## 2. Configuration avec CMake

1. Crée un dossier de build vide, par exemple `C:\Build`.
2. Ouvre CMake (cmake-gui).
3. **Browse Source...** → sélectionne `C:\UniverseEmu`.
4. **Browse Build...** → sélectionne `C:\Build`.
5. Clique sur **Configure**.
6. Choisis le générateur Visual Studio 2022, plateforme **x64**.
7. Vérifie que **TOOLS** est bien coché (nécessaire pour les extracteurs de maps utilisés plus tard).
8. Clique de nouveau sur **Configure** jusqu'à ce qu'il n'y ait plus d'erreurs en rouge.
9. Clique sur **Generate**.

**Erreurs CMake courantes :**

- *MySQL/MariaDB introuvable* : renseigne `MYSQL_INCLUDE_DIR` avec le dossier `include` de ton installation MariaDB, et `MYSQL_LIBRARY` avec `libmysql.lib` dans le dossier `lib` correspondant (coche **Advanced** si les champs ne sont pas visibles).
- *OpenSSL introuvable* : coche **Advanced**, puis renseigne `OPENSSL_ROOT_DIR` (ex : `C:/Program Files/OpenSSL-Win64`) et `OPENSSL_INCLUDE_DIR` (le sous-dossier `include` correspondant).
- *Boost introuvable* : vérifie la variable d'environnement `BOOST_ROOT` définie à l'étape [Prérequis](requirements).

## 3. Compilation

1. Ouvre `C:\Build\UniverseEmu.sln` (ou l'équivalent `.sln`) dans Visual Studio — ou clique sur **Open Project** directement depuis CMake.
2. Dans le menu du haut : **Build → Configuration Manager**, mets **Active Solution Configuration** sur `RelWithDebInfo`.
3. Clic droit sur **ALL_BUILD** dans le Solution Explorer → **Build** (ou **Build → Rebuild Solution**, `Ctrl+Alt+F7`).
4. Ça peut prendre de 5 à 30+ minutes selon ta machine.
5. En cas de succès tu verras un message du type : `Build: X succeeded, 0 failed`.

Tes binaires compilés se trouvent dans `C:\Build\bin\RelWithDebInfo`.

## 4. Fichiers nécessaires pour lancer le serveur

À côté de `authserver.exe` / `worldserver.exe`, il faut copier ces DLL :

- `libmysql.dll` → depuis le dossier `lib` de MariaDB
- `libcrypto-3-x64.dll` / `libssl-3-x64.dll` / `legacy.dll` → depuis le dossier `bin` d'OpenSSL

Renomme `authserver.conf.dist` → `authserver.conf` et `worldserver.conf.dist` → `worldserver.conf` (sauf si tu as déjà des fichiers configurés d'une compilation précédente).

## 5. Garder les sources à jour

1. Dans Git Extensions, clique sur **Pull** pour récupérer les derniers commits.
2. Relance **Configure** puis **Generate** dans CMake.
3. Recompile la solution.
4. Lance `worldserver.exe` — il appliquera automatiquement les nouvelles mises à jour SQL au démarrage (visible dans la console).

[Continuer vers la configuration du serveur →](server-setup)
