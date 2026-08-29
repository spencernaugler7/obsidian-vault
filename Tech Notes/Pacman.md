remove all orphaned packages
```bash
sudo pacman -Qqd | sudo pacman -Rsu --print -
```