# Stack notifications in Oxide Pixel

This optional patch uses the notification service shipped with Omarchy 4.5.0. The front card shows the latest alert. Older cards peek out behind it and the stack expands on hover.

1. Install Oxide Pixel. If you already have a local clone of the notifications plugin, use that clone and skip the next command. Otherwise run:

   ```sh
   omarchy plugin clone omarchy.notifications
   ```

2. Check the patch against your installed version, then apply it. The default clone path is shown below. The second command runs only if the dry run succeeds.

   ```sh
   plugin_dir="$HOME/.config/omarchy/plugins/$(id -un).notifications"
   stack_patch="$HOME/.config/omarchy/themes/oxide-pixel/extras/notification-stack.patch"
   patch --dry-run --forward -d "$plugin_dir" -p1 < "$stack_patch" &&
     patch --forward -d "$plugin_dir" -p1 < "$stack_patch"
   ```

3. Run `omarchy restart shell` while the desktop is unlocked. The layout follows the theme's `notifications.grouping` setting in `shell.toml`.

To restore the original clone, use the same two path variables and run:

```sh
patch --dry-run -R -d "$plugin_dir" -p1 < "$stack_patch" &&
  patch -R -d "$plugin_dir" -p1 < "$stack_patch"
omarchy restart shell
```

This changes how cards are displayed. Each application controls how often it sends a notification.
