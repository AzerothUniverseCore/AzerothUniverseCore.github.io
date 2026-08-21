[← Retour à la documentation](../)

# Prérequis (Windows)

> OS supporté : Windows 10 (1903 ou supérieur) / équivalent Windows Server, entièrement à jour.

## Logiciels requis

- [Git Extensions](https://gitextensions.github.io/) ≥ 2.51.2
- [MS Visual Studio Community](https://visualstudio.microsoft.com/) ≥ 17.0 (2022) — module **Développement Desktop en C++**
- [MariaDB](https://mariadb.org/download/) ≥ 10.5.8
- [SQLyog](https://github.com/webyog/sqlyog-community/wiki/Downloads) ≥ 13.3.0 (ou tout autre client compatible MySQL/MariaDB)
- [Boost](https://www.boost.org/releases/latest/) ≥ 1.78
- [CMake](https://cmake.org/download/) ≥ 3.29.8
- [OpenSSL](https://www.slproweb.com/products/Win32OpenSSL.html) ≥ v3.5.7 (64-bit, **pas** la version Light)
- [Microsoft Visual C++ 2022 Redistributable Package](https://aka.ms/vc14/vc_redist.x64.exe)

La liste complète avec les versions exactes est aussi tenue à jour sur la [release UniverseSoftware](https://github.com/AzerothUniverseCore/UniverseEmu/releases/tag/UniverseSoftware).

## Remarques

- **Visual Studio** : à l'installation, choisis **Personnalisé** → module **Développement Desktop en C++**. L'installeur de base n'inclut pas le compilateur C++ par défaut.
- **Boost** : télécharge le binaire Windows précompilé correspondant à ton toolset Visual Studio (v143 pour VS2022), installe-le à l'emplacement par défaut (ex : `C:\local\boost_1_XX_0\`), puis ajoute une variable d'environnement `BOOST_ROOT` pointant vers ce dossier. Utilise `/` et non `\` dans le chemin.
- **OpenSSL** : à l'installation, choisis de copier les DLL dans **The OpenSSL binaries (/bin) directory**, pas dans le dossier système Windows.
- **MariaDB** : garde bien en tête le mot de passe root défini à l'installation — tu en auras besoin pour importer les bases SQL et configurer `worldserver.conf` / `authserver.conf` plus tard.

[Continuer vers l'installation du core →](core-installation)
