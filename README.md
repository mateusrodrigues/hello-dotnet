# hello-dotnet

## Without plugin

```yaml
name: hello-dotnet
base: core24
version: '0.1'
summary: Hello World in desktop with .NET
description: |
  This is a simple Hello World desktop application built with .NET.
  It demonstrates how to create a snap package for a .NET application.
  The application displays a window with a "Hello, World!" message.

grade: devel
confinement: strict

parts:
  hello-dotnet:
    plugin: nil
    source-type: git
    source: https://github.com/mateusrodrigues/hello-dotnet
    build-packages:
      - dotnet8
    stage-packages:
      - libicu74
      - libfontconfig1
      - libx11-6
      - libice6
      - libsm6
    override-build: |
      dotnet publish -c Release -o $CRAFT_PART_INSTALL --self-contained -r linux-x64

apps:
  hello-dotnet:
    command: HelloDotnet
    plugs:
      - desktop
      - desktop-legacy
      - wayland
      - unity7

```

## With plugin

```yaml
name: hello-dotnet
base: core24
version: '0.1'
summary: Hello World in desktop with .NET
description: |
  This is a simple Hello World desktop application built with .NET.
  It demonstrates how to create a snap package for a .NET application.
  The application displays a window with a "Hello, World!" message.

grade: devel
confinement: strict

parts:
  hello-dotnet:
    plugin: dotnet
    source-type: git
    source: https://github.com/mateusrodrigues/hello-dotnet
    stage-packages:
      - libicu74
      - libfontconfig1
      - libx11-6
      - libice6
      - libsm6
    dotnet-version: "8.0"
    dotnet-self-contained: true

apps:
  hello-dotnet:
    command: HelloDotnet
    plugs:
      - desktop
      - desktop-legacy
      - wayland
      - unity7

```