[← Back to Documentation](../) · [← Core Installation](core-installation)

# Server Setup

## 1. Create the databases

Using SQLyog (or the `mysql`/`mariadb` CLI), connect to your local MariaDB instance and create three empty databases:

```sql
CREATE DATABASE auth;
CREATE DATABASE characters;
CREATE DATABASE world;
```

## 2. Import the base structure

Import, in order:

1. The base TrinityCore/UniverseEmu structure from [`sql/base`](https://github.com/AzerothUniverseCore/UniverseEmu/tree/main/sql/base) into the matching `auth` / `characters` / `world` databases.
2. The full Azeroth Universe content from the [UniverseSql](https://github.com/AzerothUniverseCore/UniverseEmu/releases/tag/UniverseSoftware) release into `world` (and `characters` if it ships character-side tables — check the release notes).

## 3. Client data (maps, vmaps, mmaps, dbc)

Download [UniverseData](https://github.com/AzerothUniverseCore/UniverseEmu/releases/tag/UniverseData) and extract the `dbc`, `maps`, `vmaps`, `mmaps` folders directly next to `worldserver.exe` (in `C:\Build\bin\RelWithDebInfo`).

## 4. Lua scripts

Download [UniverseLua](https://github.com/AzerothUniverseCore/UniverseEmu/releases/tag/UniverseLua) and extract it into the `lua_scripts` folder next to `worldserver.exe` (create the folder if it doesn't exist).

## 5. Configure the server

Open `authserver.conf` and `worldserver.conf` (renamed from the `.dist` files during [Core Installation](core-installation)) and set your database connection strings, e.g.:

```
LoginDatabaseInfo     = "127.0.0.1;3306;root;YOUR_PASSWORD;auth"
WorldDatabaseInfo     = "127.0.0.1;3306;root;YOUR_PASSWORD;world"
CharacterDatabaseInfo = "127.0.0.1;3306;root;YOUR_PASSWORD;characters"
```

Adjust the port if your MariaDB instance doesn't use the default `3306`.

## 6. Realmlist

In the `auth` database, update the `realmlist` table with your server's address:

```sql
UPDATE realmlist SET address = '127.0.0.1' WHERE id = 1;
```

Use `127.0.0.1` for a local-only server, or your machine's LAN/public IP if other people need to connect.

## 7. Start the server

Run `authserver.exe`, then `worldserver.exe`, both from the same folder. On first launch, `worldserver.exe` will apply any pending SQL updates automatically — watch the console for errors.

Create your first GM account from the `authserver` console:

```
account create MyAccount MyPassword
account set gmlevel MyAccount 3 -1
```

[Continue to Client Setup →](client-setup)
