---
title: 'Change Bar Status indicators'
linkTitle: 'Change Bar Status indicators'
description: >
    Make changes to the status indicators in the bar.
---

# Adding or Removing status indicators

## Finding Status Indicators

```console
$ apt search i3xrocks-
```

## Installing a Status Indicator

```console
$ sudo apt install i3xrocks-memory
$ regolith-look refresh
```

# Customization of the i3 bar {#customize-bar}

Each status indicator on the bar is managed by a file. The name of the file maps to the position of the status indicator on the bar, e.g. a file's name starting with `10_` mean its corresponding indicator will be positioned before an indicator which has a configuration file starting with `20_`. Within each file there is some information that `i3xrocks` uses to execute a script that ultimately returns the data you see on the bar. Some of the status indicators have configuration parameters that can be adjusted to your liking. For example, if you would prefer that the battery status changes more frequently, the polling interval can be updated. The first thing to do in order to customize the bar is to copy the indicators you wish to see from `/usr/share/i3xrocks/conf.d/` to `~/.config/regolith3/i3xrocks/conf.d`. Each file in `~/.config/regolith3/i3xrocks/conf.d` can be modified as you see fit. To change the order of status indicators on the bar, simply change the name of the files to the sort order you prefer.

Once you've made your changes, refreshing the session should cause the bar to update based on your new configuration.

For example, to change the order of the battery and net traffic blocks on the bar and not display notifications, perform the following steps:

```console
$ ls /usr/share/i3xrocks/conf.d/
01_setup
30_net-traffic
80_battery
80_rofication
90_time
$ mkdir -p ~/.config/regolith3/i3xrocks/conf.d
$ cp /usr/share/i3xrocks/conf.d/01_setup ~/.config/regolith3/i3xrocks/conf.d/01_setup
$ cp /usr/share/i3xrocks/conf.d/80_battery ~/.config/regolith3/i3xrocks/conf.d/30_battery
$ cp /usr/share/i3xrocks/conf.d/30_net-traffic ~/.config/regolith3/i3xrocks/conf.d/80_net-traffic
$ regolith-look refresh
```

In the above steps the following actions are performed:

-   The current `i3xrocks` modules are listed that exist in the directory created by regolith
-   The directory where user configuration lives is created at `~/.config/regolith3/i3xrocks/conf.d`
-   Three files are copied from the application created directory to the user created directory. This will cause the order to change if the user change the `n_` number like described in the first paragraph of this article
-   The `regolith-look refresh` command is run to refresh the **Bar Status Indicators**

**Note**: If any block configuration exists in the user directory `~/.config/regolith3/i3xrocks/conf.d`, then the defaults in `/usr/share/i3xrocks/conf.d/` will be ignored.

# Further Reading

The [reference page for configurations]({{< ref "/docs/Reference/configurations.md" >}}) has more details about the configuration files used with Regolith Linux.
