# B1.Mod.Template

[English](README.md)

黑神话悟空 C# Mod 模板

## 前提条件

* 已下载 [黑神话悟空](https://store.steampowered.com/app/2358720/Black_Myth_Wukong/) 以及 [B1CSharpModLoader](https://github.com/czastack/B1CSharpLoader)
* [.Net SDK 6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)
* C# IDE，比如 [Visual Studio](https://visualstudio.microsoft.com), [Rider](https://www.jetbrains.com/rider) 等

## 使用方法

> [!NOTE]
> 目前因为B1CSharpLoader方面的一些限制，Mod 作者需要下载 `GameDll` 文件夹并且自己引用dll
>
> 因此，这个模板还没准备好发布到 Nuget 上，目前只有 GitHub 的 release，所以你需要手动从[这里](https://github.com/BlackMythWukongMods/B1.Mod.Template/releases/latest)下载 .nupkg文件然后安装模板

* 如果你在使用 .Net SDK 6, 使用以下命令：

```shell
dotnet new --install B1.Mod.Template.{version}.nupkg
````

* 如果你在使用 .Net SDK 7 或者更高, 使用以下命令：

```shell
dotnet new install B1.Mod.Template.{version}.nupkg
````

### 目前的限制以及一些问题的解决方案

B1.Mod.Template 首先检查你的电脑上有没有名为 `B1_DIRECTORY` 的环境变量, 如果存在这个环境变量，它就会使用这个值当作游戏目录来自动复制生成的 dll 到 Mods 文件夹

但是，如果没有这个环境变量，Mod 作者需要手动编辑 .csproj 文件来设置路径。修改
`<GameFolder Condition="!Exists('$(B1_DIRECTORY)')">F:\SteamLibrary\steamapps\common\BlackMythWukong</GameFolder>` 里的值为你自己的游戏安装路径即可。

并且，你可能碰到一些错误说找不到引用的 dll，因为就像之前所说，ModLoader 目前并没有生成 GameDll 的功能。

因此，如果你不想要修改引用的路径，直接从 [B1CSharpLoader](https://github.com/czastack/B1CSharpLoader) 下载 GameDll 文件夹并且放在上一级目录

*你也可以考虑直接修改 .csproj 文件中的 dll 引用路径*

## 从源代码构建

* 克隆这个仓库到你的电脑上
* 在当前文件夹打开命令行或者 PowerShell，运行以下命令：

```shell
dotnet build
````

* 或者你可以使用你的 IDE 来打开 `B1.Mod.Template.sln` 文件然后构建解决方案

> [!NOTE]
> 如果你在构建期间看到有关于 `Error CS1031` 的错误, 你可以直接无视。Nuget 包文件仍然会被生成

* 接着你就可以在此文件夹内找到 Nuget 包文件 `bin/B1.Mod.Template.{version}.nupkg`
* 在 `bin` 文件夹打开命令行或者 PowerShell, 运行以下命令

```shell
dotnet new install B1.Mod.Template.{version}.nupkg
```

## 卸载

```shell
dotnet new uninstall B1.Mod.Template
````