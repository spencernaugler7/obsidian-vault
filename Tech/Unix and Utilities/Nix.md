Config for nix is located at `/etc/nixos/configuration.nix`.
Hardware config is located at `/etc/nixos/hardware-configuration.nix`

## Nix commands

##### Rebuild system after config changes and switch to the new system immediately

```bash
sudo nixos-rebuild switch
```

##### To keep just your current generation and the two older than it

```bash
nix-env --profile /nix/var/nix/profiles/system --delete-generations +3
```

##### To remove all but your current generation

```bash
nix-env --profile /nix/var/nix/profiles/system --delete-generations old
```

##### Upgrade packages.

```bash
sudo nixos-rebuild switch --upgrade-all
```

## Config options

