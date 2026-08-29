remove all orphaned packages
```bash
pacman -Qtdq | pacman -Rns -
```