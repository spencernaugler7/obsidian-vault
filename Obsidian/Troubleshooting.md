## Linux 
___
#### Obsidian opens but only the file name is saved

It is likely that Obsidian cannot access your clipboard. Clipboard access is necessary to pass data from your browser to Obsidian. Your configuration can affect how apps are sandboxed, and clipboard permissions.

If you use Wayland, make sure that Obsidian has the permissions to read the clipboard when the app is not focused. This preference may be in your tiling window manager, e.g. Hyprland or Sway.

- If you use KDE go to to **System Settings** → **Window Management** → **Window Rules** and allow Obsidian to take focus
![[allow_obsian_to_take_focus.png]]