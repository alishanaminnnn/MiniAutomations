# minAutomation

Personal scripts and notes for automating everyday tasks on my Linux (Omarchy) setup.

## Automations

### Classroom launcher

Opens Google Classroom in my school Chrome profile with one command or keyboard shortcut.

**Files**

- `classroom` is the script, installed at `~/.local/bin/classroom`.

**Script**

```bash
#!/bin/bash
setsid google-chrome-stable --profile-directory="Profile 2" "https://classroom.google.com/u/0/h/st" >/dev/null 2>&1 &
```

**How it works**

- `--profile-directory` selects the Chrome profile by its folder name, not its display name. Replace `Profile 2` with your school profile's folder name.
- `setsid` detaches Chrome from the terminal, so Chrome stays open after the terminal closes.
- `>/dev/null 2>&1` hides Chrome's messages.
- `&` runs Chrome in the background.

**Setup steps**

## Setup

1. Created a `.sh` file and added the script.
2. Ran the permission command to make it executable:

   ```bash
   chmod +x classroom.sh
   ```

3. Reloaded Linux.

**Keyboard shortcut (Omarchy, Lua config)**

Added to `~/.config/hypr/binding.lua`:

```lua
o.bind("SUPER + C", "Classroom", "alacritty -e ~/.local/bin/classroom")
```

Then reload:

```bash
hyprctl reload
```

Press **Super + C** to launch. The Alacritty window closes when the script finishes, and Chrome stays open. If you use Ghostty, replace `alacritty` with `ghostty`.

**Troubleshooting**

- **A new empty Chrome profile appears:** The `--profile-directory` value is a display name instead of a folder name. Use the folder name from step 1.
- **Chrome closes when the terminal closes:** Make sure the script uses `setsid` and ends with `&`.
- **`classroom: command not found`:** Check that `~/.local/bin` is in your `PATH` with `echo $PATH`.

