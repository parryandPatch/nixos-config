# parryandPatch NixOS Config — ASUS FX506HE

NixOS configuration for my ASUS TUF Gaming
FX506HE laptop.

> **Important:** This is a personal configuration. It currently uses a the FX506HM nixos-hardware setup and has not been modified.
> The DGPU: RTX 3050 Ti may not work as intended in this current state. 

## System overview

| Component | Configuration |
| --- | --- |
| NixOS version | 26.05 |
| Device | ASUS FX506HE |
| Desktop environment | KDE Plasma 6.6.6 |
| Window Manager | KWin(Wayland) |
| Audio | PipeWire with PulseAudio compatibility |
| Bootloader | systemd-boot |
| Hardware profile | `nixos-hardware` ASUS FX506HM module |

## Included software

- Firefox
- Kate
- Neovim
- lf
- Git
- fastfetch
- cava
- htop

## Repository layout

```text
.
├── configuration.nix
├── hardware-configuration.nix
├── flake.nix
├── flake.lock
└── wallpapers/
    └── wallpaper.jpg
```

| File or directory | Purpose |
| --- | --- |
| `configuration.nix` | Main system configuration: packages, services, users, locale, desktop, and boot settings. |
| `hardware-configuration.nix` | Hardware and filesystem configuration generated for this laptop. |
| `flake.nix` | Defines the Nix inputs and the `nixos` system configuration. |
| `flake.lock` | Pins the exact input versions used by the flake. |
| `wallpapers/` | Optional desktop wallpaper assets. |

## Flake inputs

This configuration uses:

- `nixpkgs` on the `nixos-26.05` branch.
- `nixos-hardware` for the ASUS FX506HM hardware module.

The hardware module is imported through the flake:

```nix
nixos-hardware.nixosModules.asus-fx506hm
```
## Apply the configuration

```bash
cd ~/nixos-config

# Edit the configuration.
nano configuration.nix

# Test before applying it. If there are any issues, reboot.
sudo nixos-rebuild test --flake .#nixos

#The wallpaper may not load. use the command
systemctl --user restart set-wallpaper.service

#If you face no issues, to make changes permanent use;
sudo nixos-rebuild switch --flake .#nixos

