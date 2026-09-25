---
title: I'm getting the permissions request window again and again
description: An explanation of why NOMM shows you the permissions request window, and what you can do about it.
weight: 2
---

# Context

If you're here, it's likely because you keep getting the permissions request window on NOMM over and over.

If you have copied the command, executed it in your preferred terminal, and restarted NOMM and still see the missing permission screen, then this page is for you.

First we'll explain _why_ this happens, and then we'll go into _what_ you can do about it.

## A brief explanation of what's happening

NOMM is built with privacy and security first.

It is distributed as a **Flatpak**, which is a sandboxed environment.
Think of it as if the app was running on a different computer, and there is a layer in charge of isolating the app and managing what it can or can not access on your own computer.

In our instance, NOMM actually has very little access to your files.

How it finds libraries is simple: it reads a specific file from your Steam configuration called `libraryfolders.vdf`, and from there it gets a list of all the Steam libraries registered on your system.

It then generates a command that will alow you to give NOMM access to those libraries.

Only, the problem is **Steam remembers all your libraries, even those that no longer exist**. This can be due to you changing drives, or even having a library on a USB stick or the like.

But Steam doesn't make a record of this removal, all it knows is that this library existed.

Therefore, NOMM has no way of knowing which libraries are active either.
In fact, we assume that all libraries in the `libraryfolders.vdf` file are currently active, and that NOMM should normally have access to all of them.

**What happens when one of those libraries is inaccessible is that NOMM thinks that you simply haven't given it the rights to access it yet.**

So we now have a simple explanation of why this happens, let's move on to solutions!

# Solutions!

## The Continue & Ignore button

The easy solution is to simply press the "Continue & Ignore" button.
This will add the libraries that are inaccessible to a list of ignored libraries, that will not be checked when you launch NOMM.

This is not a permanent process however, and launching a manual scan of libraries from the main dashboard UI will remove all libraries from the ignored list.

## Manually editing the Steam library file

If you want to make sure that this will never happen again, and you are sure that this library does not exist and will never be reconnected, **you can manually edit the Steam library file**.

You may follow the steps described here to do so:

### 1. Close Steam

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

### 2. Create a backup of the file

Make a copy of the configuration file before editing it.

```bash
cp ~/.steam/steam/config/libraryfolders.vdf ~/.steam/steam/config/libraryfolders.vdf.bak
```

### 3. Open the file for editing

Open the file in a text editor:

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

### 4. Remove the target library block

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

### 5. Save the file and relaunch Steam

Save your changes:

- In Nano: press `Ctrl + O`, then `Enter`
- Then exit with `Ctrl + X`

You may now launch Steam and/or NOMM again.

You should see that NOMM is no longer asking for permisions for that Steam Library.

## Troubleshooting

If NOMM still asks for permisions for the removed library:

- Make sure Steam was fully closed before editing the file.
- Recheck that the library block was removed cleanly.
- Restore your backup and try again.

## Notes

This method is intended for removing a stale or extra Steam library entry. If the library contains games you still want to access, do not delete it from the config file unless you are sure you no longer need it.

You can always restore the file from the backup if something goes wrong:

```bash
cp ~/.steam/steam/config/libraryfolders.vdf.bak ~/.steam/steam/config/libraryfolders.vdf
```
