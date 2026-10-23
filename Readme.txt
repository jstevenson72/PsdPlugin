Photoshop PSD FileType Plugin for Paint.NET


Description
------------

This plugin allows Paint.NET to load and save Photoshop .PSD files.

Perfect round-trip compatibility is possible for features that are
common to both Paint.NET and Adobe Photoshop.  Other features are
preserved with varying levels of visual fidelity.

For more details, or to report bugs, please refer to the website:
  https://www.psdplugin.com/


Installation
-------------

1. Exit all instances of Paint.NET.
2. Copy PhotoShop.dll into the C:\Program Files\Paint.NET\FileTypes
   directory.
3. Restart Paint.NET, which will automatically detect the plugin.

A copy of Paint.NET can be obtained from the official website:
  http://www.getpaint.net/


Building
---------

The plugin is built against the assemblies of an installed Paint.NET 5.x,
which targets .NET 11, so a matching .NET SDK is required.  global.json
pins the solution to the .NET 11 SDK band so that both "dotnet build" and
the Visual Studio build use the same toolset.

  dotnet build PSDPlugin.sln

The Paint.NET installation directory defaults to C:\Program Files\Paint.NET.
Override it on the command line if Paint.NET is installed elsewhere:

  dotnet build PSDPlugin.sln /p:PaintDotNetDir="D:\Paint.NET"

The build output is PhotoShopFileType\bin\Debug\PhotoShop.dll (or
...\bin\Release\PhotoShop.dll for a release build).  Run the unit tests with:

  dotnet test Tests\Tests.csproj


Licensing
----------

This software is open-source, under the MIT and BSD licenses.  Please see
LICENSE.TXT for complete licensing and attribution information.
