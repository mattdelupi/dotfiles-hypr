# Requirements

After a clean installation of `hyprland`, some dependencies are needed.

## Dependencies

- `wl-clipboard`
- `waybar` (see [dotfiles-waybar](https://github.com/mattdelupi/dotfiles-waybar) repo for my setup)
- `swaync` (see [related section](#swaync-autostart-conflict) for for troubleshooting systemd autostart conflicts)
- `hyprpaper`
- `hyprpicker`
- `hyprlauncher`
- `hypridle`
- `hyprlock`
- `xdg-desktop-portal-hyprland`
- `xdg-desktop-portal-gtk`
- `hyprsunset`
- `hyprland-qt-support`
- `hyprshutdown`
- `hyprland-guiutils`
- `hyprpolkitagent` (not included in the official repos, see [related section](#installation-of-hyprpolkitagent) for installation)

### Swaync autostart conflict

After booting with systemd you could get errors due to multiple instances of swaync trying to be run. This can happen because inside the `hyprland.lua` file there is a line that makes your system execute `swaync` command immediately after booting up and, if systemd tries to do the same, errors occur. To check whether this happens you can simply look at the output of the following command after booting up:

```
systemctl --failed
```

And you can fix it by disabling the service entirely from systemd:

```
systemctl --user disable swaync
systemctl --user reset-failed swaync
```

and rebooting the system.

If the errors still persists, try masking the service:

```
systemctl --user mask swaync
systemctl --user reset-failed swaync
```

### Installation of hyprpolkitagent

For official documentation please refer to the [hyprpolkitagent section on the hyprland wiki](https://wiki.hypr.land/Hypr-Ecosystem/hyprpolkitagent/) and to the [hyprpolkitagent repository](https://github.com/hyprwm/hyprpolkitagent).

You can easily install it by running the following commands:

```
mkdir hyprpolkitagent_src_folder
cd hyprpolkitagent_src_folder
git clone https://github.com/hyprwm/hyprpolkitagent
cd hyprpolkitagent
cmake --no-warn-unused-cli -DCMAKE_BUILD_TYPE:STRING=Release -DCMAKE_INSTALL_PREFIX:PATH=/usr -S . -B ./build
cmake --build ./build --config Release --target all -j`nproc 2>/dev/null || getconf NPROCESSORS_CONF`
sudo cmake --install ./build
cd ../..
rm -r hyprpolkitagent_src_folder
```

Then, start it by running:

```
systemctl --user start hyprpolkitagent
```
