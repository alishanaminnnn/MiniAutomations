## Automations

### Classroom launcher

Opens Google Classroom in my school Chrome profile. I can run it by typing `classroom` in terminal or by pressing **Super + C**.

**Files**

- `classroom`: the script. It lives at `~/.local/bin/classroom`.

**Script**

```bash
#!/bin/bash
setsid google-chrome-stable --profile-directory="Profile 2" "https://classroom.google.com/u/0/h/st" >/dev/null 2>&1 &
```

Replace `Profile 2` with the folder name of my school profile.

**What each part does**

- `--profile-directory` picks the Chrome profile by its folder name, not its display name.
- `setsid` keeps Chrome open after the terminal closes.
- `>/dev/null 2>&1` hides Chrome's messages.
- `&` runs Chrome in the background.

**Setup**

1. Created a `.sh` file and add the script given above.
2. Made it executable:

   ```bash
   chmod +x classroom.sh
   ```

3. Reload Linux.

**How to trigger it through Keyboard shortcut ?**

Added this line to `~/.config/hypr/binding.lua` if you are using arch(omarchy):

```lua
o.bind("SUPER + C", "Classroom", "alacritty -e ~/.local/bin/classroom")
```

Then ran:

```bash
hyprctl reload
```

If you use Ghostty instead of Alacritty, replace `alacritty` with `ghostty`.

**Troubleshooting**

- **A new empty Chrome profile opens:** The profile name is wrong. Use the folder name, not the display name.
- **Chrome closes with the terminal:** Check that the script has `setsid` and ends with `&`.
- **`classroom: command not found`:** Run `echo $PATH` and check that `~/.local/bin` is listed.
