# Yabai

## Scripting Addition

[Source](https://github.com/koekeishiya/yabai/wiki/Installing-yabai-(latest-release)#configure-scripting-addition)

Did cmd + m stop working for you?

> Configure scripting addition
> yabai uses the macOS Mach APIs to inject code into Dock.app; this requires elevated (root) privileges. You can configure your user to execute yabai --load-sa as the root user without having to enter a password. To do this, we add a new configuration entry that is loaded by /etc/sudoers.
> ```
> # create a new file for writing - visudo uses the vim editor by default.
> # go read about this if you have no idea what is going on.
> 
> sudo visudo -f /private/etc/sudoers.d/yabai
> ```
>
> ```
> # input the line below into the file you are editing.
> #  replace <yabai> with the path to the yabai binary (output of: which yabai).
> #  replace <user> with your username (output of: whoami). 
> #  replace <hash> with the sha256 hash of the yabai binary (output of: shasum -a 256 $(which yabai)).
> #   this hash must be updated manually after upgrading yabai.
>
> <user> ALL=(root) NOPASSWD: sha256:<hash> <yabai> --load-sa
> ```
> If you know what you are doing, the following one-liner can be used to update the sudoers file correctly:
> ```
> echo "$(whoami) ALL=(root) NOPASSWD: sha256:$(shasum -a 256 $(which yabai) | cut -d " " -f 1) $(which yabai) --load-sa" | sudo tee /private/etc/sudoers.d/yabai
> ```
