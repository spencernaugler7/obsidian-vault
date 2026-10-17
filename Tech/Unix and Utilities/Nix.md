Config for nix is located at `/etc/nixos/configuration.nix`.

## Rebuild system after config changes and switch to the new system immediately

```bash
sudo nixos-rebuild switch
```


### To keep just your current generation and the two older than it

```bash
nix-env --profile /nix/var/nix/profiles/system --delete-generations +3
```


### To remove all but your current generation

```bash
nix-env --profile /nix/var/nix/profiles/system --delete-generations old
```