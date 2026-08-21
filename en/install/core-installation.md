[← Back to Documentation](../) · [← Requirements](requirements)

# Core Installation (Windows)

Make sure you've installed everything listed on the [Requirements](requirements) page first.

## 1. Pulling the source

1. Create a directory to clone the source into, e.g. `C:\UniverseEmu`.
2. Right-click the directory → **Git Extensions → Clone**.
3. Repository URL: `https://github.com/AzerothUniverseCore/UniverseEmu.git`
4. Click **Clone**. This pulls the full source into `C:\UniverseEmu`.

(You can also clone from the command line: `git clone https://github.com/AzerothUniverseCore/UniverseEmu.git`.)

## 2. Configuring with CMake

1. Create an empty build directory, e.g. `C:\Build`.
2. Open CMake (cmake-gui).
3. **Browse Source...** → select `C:\UniverseEmu`.
4. **Browse Build...** → select `C:\Build`.
5. Click **Configure**.
6. Choose the Visual Studio 2022 generator, **x64** platform.
7. Make sure **TOOLS** is checked (needed for the map extractors used later).
8. Click **Configure** again until there are no more errors in red.
9. Click **Generate**.

**Common CMake errors:**

- *MySQL/MariaDB not found*: set `MYSQL_INCLUDE_DIR` to your MariaDB `include` folder and `MYSQL_LIBRARY` to `libmysql.lib` inside your MariaDB `lib` folder (tick **Advanced** if you don't see these fields).
- *OpenSSL not found*: tick **Advanced**, then set `OPENSSL_ROOT_DIR` (e.g. `C:/Program Files/OpenSSL-Win64`) and `OPENSSL_INCLUDE_DIR` (the `include` subfolder inside it).
- *Boost not found*: double-check the `BOOST_ROOT` environment variable from the [Requirements](requirements) step.

## 3. Compiling

1. Open `C:\Build\UniverseEmu.sln` (or the equivalent `.sln`) in Visual Studio — or click **Open Project** directly from CMake.
2. In the top menu: **Build → Configuration Manager**, set **Active Solution Configuration** to `RelWithDebInfo`.
3. Right-click **ALL_BUILD** in the Solution Explorer → **Build** (or **Build → Rebuild Solution**, `Ctrl+Alt+F7`).
4. This can take anywhere from 5 to 30+ minutes depending on your machine.
5. On success you'll see something like: `Build: X succeeded, 0 failed`.

Your compiled binaries will be in `C:\Build\bin\RelWithDebInfo`.

## 4. Files needed to run the server

Alongside `authserver.exe` / `worldserver.exe`, you'll need these DLLs copied into the same folder:

- `libmysql.dll` → from your MariaDB `lib` folder
- `libcrypto-3-x64.dll` / `libssl-3-x64.dll` / `legacy.dll` → from your OpenSSL `bin` folder

Rename `authserver.conf.dist` → `authserver.conf` and `worldserver.conf.dist` → `worldserver.conf` (unless you already have configured ones from a previous build).

## 5. Keeping the source up to date

1. In Git Extensions, click **Pull** to fetch the latest commits.
2. Re-run CMake **Configure** and **Generate**.
3. Rebuild the solution.
4. Start `worldserver.exe` — it will automatically apply any new SQL updates on launch (you'll see this in the console).

[Continue to Server Setup →](server-setup)
