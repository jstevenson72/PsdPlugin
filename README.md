# Photoshop PSD FileType Plugin for Paint.NET

Load and save Adobe Photoshop `.PSD` files in [Paint.NET](https://www.getpaint.net/).

This is a maintained continuation of the original [PsdPlugin](https://github.com/PsdPlugin/PsdPlugin)
project, retargeted to run on current Paint.NET. The upstream repository has seen no
commits since July 2024, so fixes and updates happen here.

## Download

Grab `PSDPlugin.zip` from the [latest release](../../releases/latest), then:

1. Exit all instances of Paint.NET.
2. Copy `PhotoShop.dll` into the `FileTypes` folder of your Paint.NET install,
   typically `C:\Program Files\Paint.NET\FileTypes\`.
3. Restart Paint.NET, which will detect the plugin automatically.

## Requirements

| | |
|---|---|
| Paint.NET | **5.2 or newer** |
| .NET | 11 (bundled with Paint.NET 5.2) |

> **Upgrading from 2.x?** Releases up to 2.5.0 were built for Paint.NET 4.x and
> will not load in Paint.NET 5.2. Delete the old `PhotoShop.dll` from
> `FileTypes` before installing this one. That compatibility break is why the
> version moved to 3.0.0.

## What is supported

Perfect round-trip compatibility is possible for features common to both
Paint.NET and Photoshop. Other features are preserved with varying levels of
visual fidelity. Please report anything that does not survive a round-trip
through [the issue tracker](../../issues).

## Building from source

The plugin compiles against the assemblies of an installed Paint.NET, so you
need Paint.NET 5.2 and a matching .NET 11 SDK. `global.json` pins the SDK band
so `dotnet build` and Visual Studio agree on the toolset.

```sh
dotnet build PSDPlugin.sln
dotnet test Tests\Tests.csproj
```

The Paint.NET install directory defaults to `C:\Program Files\Paint.NET`;
override it if yours lives elsewhere:

```sh
dotnet build PSDPlugin.sln /p:PaintDotNetDir="D:\Paint.NET"
```

The output is `PhotoShopFileType\bin\Release\PhotoShop.dll`.
`Build\build-package.cmd` produces the `PSDPlugin.zip` release archive.

## Continuous integration

[`.github/workflows/ci.yml`](.github/workflows/ci.yml) builds and tests every
push and pull request. Paint.NET is not redistributable, so CI downloads the
matching portable build from the official release page, caches it, and points
the build at it with `PaintDotNetDir`. The version used is set by
`PAINTNET_VERSION` and `PAINTNET_TAG` at the top of the workflow.

Pushing a `v*` tag runs [`release.yml`](.github/workflows/release.yml), which
rebuilds, retests, and publishes a GitHub release with `PSDPlugin.zip`
attached.

## Licence

MIT, with portions of the PSD parsing code under BSD 3-Clause. See
[LICENSE.txt](LICENSE.txt) for the MIT terms, and
[THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt) for the BSD terms and the
attribution they require. Original work by Frank Blumenberg and Tao Yue; the
BSD portions derive from Jonas Beckeman's Yet Another PSD Parser.
