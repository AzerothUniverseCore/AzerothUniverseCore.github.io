[← Back to Documentation](../)

# Requirements (Windows)

> Supported OS: Windows 10 (1903 or later) / Windows Server equivalent, fully updated.

## Required software

- [Git Extensions](https://gitextensions.github.io/) ≥ 2.51.2
- [MS Visual Studio Community](https://visualstudio.microsoft.com/) ≥ 17.0 (2022) — **Desktop development with C++** workload
- [MariaDB](https://mariadb.org/download/) ≥ 10.5.8
- [SQLyog](https://github.com/webyog/sqlyog-community/wiki/Downloads) ≥ 13.3.0 (or any MySQL/MariaDB-compatible client of your choice)
- [Boost](https://www.boost.org/releases/latest/) ≥ 1.78
- [CMake](https://cmake.org/download/) ≥ 3.29.8
- [OpenSSL](https://www.slproweb.com/products/Win32OpenSSL.html) ≥ v3.5.7 (64-bit, **not** the Light version)
- [Microsoft Visual C++ 2022 Redistributable Package](https://aka.ms/vc14/vc_redist.x64.exe)

The full list with exact versions is also kept up to date on the [UniverseSoftware release](https://github.com/AzerothUniverseCore/UniverseEmu/releases/tag/UniverseSoftware).

## Notes

- **Visual Studio**: when installing, select **Custom** → workload **Desktop development with C++**. The plain installer does not include the C++ compiler by default.
- **Boost**: download the prebuilt Windows binary matching your Visual Studio toolset (v143 for VS2022), install to the default location (e.g. `C:\local\boost_1_XX_0\`), then add a `BOOST_ROOT` environment variable pointing to that folder. Use `/` not `\` in the path.
- **OpenSSL**: during installation, choose to copy the DLLs to **The OpenSSL binaries (/bin) directory**, not the Windows system directory.
- **MariaDB**: remember the root password you set during installation — you'll need it both to import the SQL databases and to configure `worldserver.conf` / `authserver.conf` later.

[Continue to Core Installation →](core-installation)
