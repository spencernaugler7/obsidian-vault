## Downgrade newer packages to the official versions in the repo. 
```bash
sudo pacman -Syuu
```
(use this when there are warnings like: "pacman warning package local is newer than extra")

## add user
```bash
useradd -m -s /bin/bash roguetwo
```

## change pass for new user
```bash
sudo passwd roguetwo # new pass: clear01
```

## Remove package and all dependancies
```bash
pacman -Rns
```

## Show information for installed packages and system health.
```bash
yay -Ps
```

## Show available updates for packages installed from the AUR.
```bash
yay -Qau
```

## Update packages installed from the AUR.
```bash
yay -Sau
```

## Update all system and installed packages.
```bash
yay -Syu or yay
```

## Update a single package.
```bash
yay -Sy <package>
```