[← Retour à la documentation](../) · [← Installation du core](core-installation)

# Configuration du serveur

## 1. Créer les bases de données

Avec SQLyog (ou le CLI `mysql`/`mariadb`), connecte-toi à ton instance MariaDB locale et crée trois bases vides :

```sql
CREATE DATABASE auth;
CREATE DATABASE characters;
CREATE DATABASE world;
```

## 2. Importer la structure de base

Importe, dans l'ordre :

1. La structure de base TrinityCore/UniverseEmu depuis [`sql/base`](https://github.com/AzerothUniverseCore/UniverseEmu/tree/main/sql/base) dans les bases `auth` / `characters` / `world` correspondantes.
2. Le contenu complet d'Azeroth Universe depuis la release [UniverseSql](https://github.com/AzerothUniverseCore/UniverseEmu/releases/tag/UniverseSoftware) dans `world` (et `characters` si elle contient des tables côté personnage — vérifie les notes de la release).

## 3. Données client (maps, vmaps, mmaps, dbc)

Télécharge [UniverseData](https://github.com/AzerothUniverseCore/UniverseEmu/releases/tag/UniverseData) et extrais les dossiers `dbc`, `maps`, `vmaps`, `mmaps` directement à côté de `worldserver.exe` (dans `C:\Build\bin\RelWithDebInfo`).

## 4. Scripts Lua

Télécharge [UniverseLua](https://github.com/AzerothUniverseCore/UniverseEmu/releases/tag/UniverseLua) et extrais-le dans le dossier `lua_scripts` à côté de `worldserver.exe` (crée le dossier s'il n'existe pas).

## 5. Configurer le serveur

Ouvre `authserver.conf` et `worldserver.conf` (renommés depuis les fichiers `.dist` lors de l'[installation du core](core-installation)) et renseigne tes chaînes de connexion à la base de données, par exemple :

```
LoginDatabaseInfo     = "127.0.0.1;3306;root;TON_MOT_DE_PASSE;auth"
WorldDatabaseInfo     = "127.0.0.1;3306;root;TON_MOT_DE_PASSE;world"
CharacterDatabaseInfo = "127.0.0.1;3306;root;TON_MOT_DE_PASSE;characters"
```

Adapte le port si ton instance MariaDB n'utilise pas le port par défaut `3306`.

## 6. Realmlist

Dans la base `auth`, mets à jour la table `realmlist` avec l'adresse de ton serveur :

```sql
UPDATE realmlist SET address = '127.0.0.1' WHERE id = 1;
```

Utilise `127.0.0.1` pour un serveur local uniquement, ou l'IP LAN/publique de ta machine si d'autres personnes doivent se connecter.

## 7. Démarrer le serveur

Lance `authserver.exe`, puis `worldserver.exe`, tous les deux depuis le même dossier. Au premier lancement, `worldserver.exe` applique automatiquement les mises à jour SQL en attente — surveille la console en cas d'erreur.

Crée ton premier compte GM depuis la console `authserver` :

```
account create MonCompte MonMotDePasse
account set gmlevel MonCompte 3 -1
```

[Continuer vers la configuration du client →](client-setup)
