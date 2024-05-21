# mutter-xwayland-scaling

Mutter build with Xwayland native fractional scaling patch.

[gnome-settings-daemon-xwayland-scaling](https://github.com/HydroH/gnome-settings-daemon-xwayland-scaling) must also be installed to work.

---
To enable xwayland native fractional scaling after installation run:
- ```gsettings set org.gnome.mutter experimental-features "['scale-monitor-framebuffer', 'xwayland-native-scaling']"```
- Then open Settings > Displays to set the scale.

To disable fractional scaling run:
- ```gsettings reset org.gnome.mutter experimental-features```

---
