# Requirements

After a clean installation of `hyprland`, some dependencies are needed.

## Dependencies

- `wl-clipboard`
- `waybar` (see [dotfiles-waybar](https://github.com/mattdelupi/dotfiles-waybar) for my setup)
- `swaync`
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
- `hyprpolkitagent` (not included in the official repos, see [here](#installation-of-hyprpolkitagent) for installation)

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
