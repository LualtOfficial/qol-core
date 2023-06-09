# Quality Of Life Core

### READ THIS IF YOU WANT YOUR MOD TO USE /UPDATE
if you make a release on github make sure the tag is like "0.0.1"
and also set that version in your .csproj, then make sure you put
in your github username+repo when registering your mod

Example.cs
```cs
using BepInEx;
using BepInEx.IL2CPP;
using HarmonyLib;
using System;
using System.Collections.Generic;
using qol_core;

namespace example
{
    [BepInPlugin(PluginInfo.PLUGIN_GUID, PluginInfo.PLUGIN_NAME, PluginInfo.PLUGIN_VERSION)]
    public class Plugin : BasePlugin
    {
        public static Mod modInstance;

        public override void Load()
        {
            Harmony.CreateAndPatchAll(typeof(Plugin));

            modInstance = Mods.RegisterMod(PluginInfo.PLUGIN_NAME, PluginInfo.PLUGIN_VERSION, "An example mod.", "LualtOfficial/Example");

            Commands.RegisterCommand("test", "test", "A test command.", modInstance, TestCommand);

            Log.LogInfo($"Plugin {PluginInfo.PLUGIN_GUID} is loaded!");
        }


        public static bool TestCommand(List<string> arguments)
        {
            qol_core.Plugin.SendMessage("Hello, world! " + string.Join(", ", arguments), modInstance);
        }
    }
}
```

Message
```cs
qol_core.Plugin.SendMessage("Hello, world!", modInstance);
```

Mods
```cs
// with updater
Mods.RegisterMod(PluginInfo.PLUGIN_NAME, PluginInfo.PLUGIN_VERSION, "Description", "UserName/RepoName");
// without updater
Mods.RegisterMod(PluginInfo.PLUGIN_NAME, PluginInfo.PLUGIN_VERSION, "Description");

Mods.UnregisterMod(PluginInfo.PLUGIN_NAME);
Mods.ModExists("mod-name");
Mods.GetMod("mod-name");
```

Commands
```cs
Commands.RegisterCommand("command-name", "/command-name (optional|optional2) [required|required2]", "description of the command", modInstance, Callback);
Commands.UnregisterCommand("mod-name:command-name");
Commands.CommandExists("mod-name:command-name");
Commands.GetCommand("mod-name:command-name");
Commands.FindName("command-name");
```