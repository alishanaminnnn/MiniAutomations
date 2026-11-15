# Classroom launcher

Opens Google Classroom in my school Chrome profile. I can run it by typing `classroom` in the terminal or by pressing **Super + C**.

## Files

- `classroom.sh`: the script. The package installs it as the command `classroom` in `/usr/bin/`.
- `PKGBUILD`: the recipe that builds and installs the package.

## Script

```bash
#!/bin/bash
setsid google-chrome-stable --profile-directory="Profile 2" "https://classroom.google.com/u/0/h/st" >/dev/null 2>&1 &
```

Replace `Profile 2` with the folder name of your school profile.

**What each part does**

- `--profile-directory` picks the Chrome profile by its folder name, not its display name.
- `setsid` keeps Chrome open after the terminal closes.
- `>/dev/null 2>&1` hides Chrome's messages.
- `&` runs Chrome in the background.

## Install from GitHub (Omarchy / Arch)

1. Download the repo:

   ```bash
   git clone https://github.com/alishanaminnnn/MiniAutomations.git
   ```

2. Go to the folder that contains the recipe:

   ```bash
   cd MiniAutomations/classroom
   ```

3. Build and install the package:

   ```bash
   makepkg -si
   ```

   Type your password when asked, then type `Y` if it asks to proceed.

4. Test it:

   ```bash
   classroom
   ```

Chrome should open Google Classroom in the profile named in the script.

## Keyboard shortcut

Add this line to `~/.config/hypr/binding.lua`:

```lua
o.bind("SUPER + C", "Classroom", "alacritty -e classroom")
```

Then reload Hyprland:

```bash
hyprctl reload
```

If you use Ghostty instead of Alacritty, replace `alacritty` with `ghostty`.

## Updating

When you change `classroom.sh`:

1. Increase `pkgver` in `PKGBUILD` (for example, `1.0` to `1.1`).
2. Commit and push the changes.
3. Run `makepkg -si` again.

## Troubleshooting

- **A new empty Chrome profile opens:** The profile name is wrong. Use the folder name, not the display name.
- **Chrome closes with the terminal:** Check that the script has `setsid` and ends with `&`.
- **`classroom: command not found`:** Run `echo $PATH` and check that `/usr/bin` is listed. If you installed the package, run `pacman -Q classroom-launcher` to confirm it's installed.
- **An old copy runs instead of the package:** Delete it with `rm ~/.local/bin/classroom`, then run `hash -r` or open a new terminal.
