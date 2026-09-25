---
title: Fix an extra Steam library folder
description: Safely remove a stale Steam library entry by editing the Steam libraryfolders.vdf file on Linux.
weight: 2
---

If Nomm still asks permisions for a steam library folder you no longer use, you can remove it by editing the Steam configuration file `libraryfolders.vdf`. This is a safe process, but it should be done carefully because Steam can overwrite manual edits if it is still running.

## Before you begin

- Close Steam completely before editing any config files.
- Make a backup of the file before changing anything.
- Only remove the unwanted library block. Do not delete the default Steam library unless you know exactly what you are doing.

## 1. Close Steam first

Always fully shut down Steam before editing `libraryfolders.vdf`. If Steam is still running, it may rewrite your changes when it exits.

To close Steam from the terminal:

```bash
pkill steam
```

To verify that it has stopped:

```bash
pgrep steam
```

If this command returns no output, Steam is no longer running.

## 2. Create a backup

Make a copy of the configuration file before editing it.

```bash
cp ~/.steam/steam/config/libraryfolders.vdf ~/.steam/steam/config/libraryfolders.vdf.bak
```

Verify that the backup was created:

```bash
ls ~/.steam/steam/config/libraryfolders.vdf.bak
```

If the file exists, the backup is ready.

## 3. Open the file for editing

Open the file in a text editor such as Nano or Gedit:

```bash
nano ~/.steam/steam/config/libraryfolders.vdf
```

You should see a file structure similar to this:

```vdf
"libraryfolders"
{
    "0"
    {
        "path"        "/home/your-user/.local/share/Steam"
        ...
    }
    "1"
    {
        "path"        "/media/your-user/Games/SteamLibrary"
        "label"       ""
        "contentid"   "123456789"
        "totalsize"   "0"
        "enabled"     "1"
        "apps"
        {
            ...
        }
    }
}
```

Each library entry is a numbered block such as `"0"`, `"1"`, and so on.

## 4. Remove the target library block

Find the block whose `"path"` matches the library folder you want to remove.

Delete the entire block for that library, including the numbered key and the matching braces:

```vdf
"1"
{
    "path"        "/media/your-user/Games/SteamLibrary"
    "label"       ""
    "contentid"   "123456789"
    "totalsize"   "0"
    "enabled"     "1"
    "apps"
    {
        ...
    }
}
```

Important: keep the remaining library definitions valid. Make sure the file still has matching opening and closing braces after the edit.

## 5. Save the file and relaunch Steam

Save your changes:

- In Nano: press `Ctrl + O`, then `Enter`
- Then exit with `Ctrl + X`

Now start Steam again.

Open Nomm and see if it's asking for permisions to that Steam Library again.

You should see that Nomm is no longer asking for permisions for that Steam Library.

## Troubleshooting

If Nomm still asks for permisions for the removed library:

- Make sure Steam was fully closed before editing the file.
- Recheck that the library block was removed cleanly.
- Restore your backup and try again more carefully.

## Notes

This method is intended for removing a stale or extra Steam library entry. If the library contains games you still want to access, do not delete it from the config file unless you are sure you no longer need it.

You can always restore the file from the backup if something goes wrong:

```bash
cp ~/.steam/steam/config/libraryfolders.vdf.bak ~/.steam/steam/config/libraryfolders.vdf
```
