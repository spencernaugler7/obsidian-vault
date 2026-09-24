## User Management
### add user
```bash
useradd -m -s /bin/bash roguetwo
```

### change pass for new user
```bash
sudo passwd roguetwo # new pass: clear01
```

___
## Package management

### Downgrade newer packages to the official versions in the repo. 
```bash
sudo pacman -Syuu
```
(use this when there are warnings like: "pacman warning package local is newer than extra")

### See packages that you explicitly installed (excluding base devel)
```bash
pacman -Qei | awk '/^Name/ { name=$3 } /^Groups/ { if ( $3 != "base" && $3 != "base-devel" ) { print name } }'
```

### Remove package and all dependencies (unsafe and can result in breakage)
```bash
pacman -Rns
```

### Show information for installed packages and system health.
```bash
yay -Ps
```

### Show available updates.
```bash
pacman -Qau
```

### Update packages installed from the AUR.
```bash
yay -Sau
```

### Update all system and installed packages.
```bash
pacman -Syu
```

### Update a single package.
```bash
pacman -Sy <package>
```