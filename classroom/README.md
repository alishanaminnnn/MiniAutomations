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

## Install (Omarchy / Arch)

## Install (Omarchy / Arch)

```bash
git clone https://github.com/alishanaminnnn/MiniAutomations.git
cd MiniAutomations/classroom
makepkg -si
```

After this finishes, the script is installed as `/usr/bin/classroom`, and you can run `classroom` from any terminal.

## Run

Type this in the terminal:

```bash
classroom
```

## Change the Chrome profile

The script uses `Profile 2`, my school profile. To use your own profile, edit `classroom.sh` and replace `Profile 2` with your profile's folder name.
