install android studio

download zip and extract

``` 
sudo mv ~/Downloads/android-studio /usr/local/ 
```
Desktop shortcut: 
```
nano ~/.local/share/applications/androidstudio.desktop
```

paste following
```

[Desktop Entry]
Version=1.0
Type=Application
Name=Android Studio
Exec="/usr/local/android-studio/bin/studio.sh" %f
Icon=/usr/local/android-studio/bin/studio.png
Categories=Development;IDE;
Terminal=false
StartupNotify=true
StartupWMClass=android-studio

```