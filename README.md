# B1.Mod.Template

[中文文档](README.zh-CN.md)

Template for making Black Myth Wukong C# Mods

## Pre-requisites

* [Black Myth Wukong](https://store.steampowered.com/app/2358720/Black_Myth_Wukong/) with [B1CSharpModLoader](https://github.com/czastack/B1CSharpLoader)
* [.Net SDK 6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)
* Any C# IDE ([Visual Studio](https://visualstudio.microsoft.com), [Rider](https://www.jetbrains.com/rider), etc.)

## Getting Started

> [!NOTE]
> Currently due to some limitations on B1CSharpModLoader side, modders needs to download the `GameDll` folder and reference the dlls by themselves.
>
> Therefore, this template is not ready to publish to Nuget, now it's GitHub release only, which means you need to manually download the .nupkg file from [here](https://github.com/BlackMythWukongMods/B1.Mod.Template/releases/latest) and install it.

* If you are using .Net SDK 6, run

```shell
dotnet new --install B1.Mod.Template.{version}.nupkg
````

* If you are using of .Net SDK 7 or higher, run

```shell
dotnet new install B1.Mod.Template.{version}.nupkg
````

This will install the template on your computer.

### Current Limitations and Problem-Solving

B1.Mod.Template first check if your computer sets the environment variable named
`B1_DIRECTORY`, if the environment variable exists, it will use the value as the game folder to automatically copy the generated dll after build into Mods folder.

However, if no environment variable is found, modders need to set the path manually inside .csproj file, the line
`<GameFolder Condition="!Exists('$(B1_DIRECTORY)')">F:\SteamLibrary\steamapps\common\BlackMythWukong</GameFolder>`. Change the value inside into your own installation path.

Also, you might have many errors states that referenced dlls cannot be found. This is because as previously noted, ModLoader doesn't provide generating GameDlls functions right now.

If you don't want to change the path, simply download GameDll folder from [B1CSharpLoader](https://github.com/czastack/B1CSharpLoader) and put it inside previous level folder.

*You may also consider changing the referenced dll path directly by editing .csproj file.*

## Build From Source

* Clone the repository to your computer
* Open command prompt or powershell in that folder, run

```shell
dotnet build
````

* Or you can use your IDE to open the `B1.Mod.Template.sln` solution file and build the solution

> [!NOTE]
> If you saw errors during the build about `Error CS1031`, it's normal, and you can ignore it. The nuget package file should still be generated.

* Then you can find the nuget package in `bin/B1.Mod.Template.{version}.nupkg`
* Open command prompt or powershell in `bin` folder, run

```shell
dotnet new install B1.Mod.Template.{version}.nupkg
```