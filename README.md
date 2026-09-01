# org.openttd.OpenTTD Flatpak

Flatpak packaging for [OpenTTD](https://www.openttd.org), an open source
transport simulation game based on Transport Tycoon Deluxe.

## Requirements

- [Flatpak](https://flatpak.org/setup/)
- [org.flatpak.Builder](https://flathub.org/apps/org.flatpak.Builder)

The sandboxed builder is recommended because it matches the Flathub build
environment.

## Build and install locally

```bash
flatpak remote-add --if-not-exists --user flathub \
  https://dl.flathub.org/repo/flathub.flatpakrepo
flatpak install --user flathub org.flatpak.Builder
flatpak install --user flathub org.freedesktop.Platform//25.08
flatpak install --user flathub org.freedesktop.Sdk//25.08
flatpak run org.flatpak.Builder --user --install --force-clean \
  builddir org.openttd.OpenTTD.yaml
flatpak run org.openttd.OpenTTD
```

OpenTTD needs network access for multiplayer and its online content features.
The package includes the OpenGFX graphics set and OpenMSX/OpenSFX media sets.
The package grants access to the user's home directory because OpenTTD supports
user-managed savegames, scenarios, NewGRFs, AIs, GameScripts and downloaded
content in arbitrary user-selected locations. This permission requires a
Flathub linter exception.

## Lint

```bash
flatpak run --command=flatpak-builder-lint org.flatpak.Builder \
  manifest org.openttd.OpenTTD.yaml
flatpak run --command=flatpak-builder-lint org.flatpak.Builder repo repo
```

## Update

1. Update the OpenTTD source archive URL and checksum in
   `org.openttd.OpenTTD.yaml`.
2. Update the version and date in `org.openttd.OpenTTD.metainfo.xml`.
3. Check the OpenGFX, OpenMSX and OpenSFX sources for newer stable releases.
4. Build and lint the package before submitting the update.
