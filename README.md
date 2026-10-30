# Remote Touchpad

Control mouse and keyboard from the webbrowser of a smartphone
(or any other device with a touchscreen).
To take control open the displayed URL or scan the QR code.

Supports Flatpak's RemoteDesktop portal (for Wayland), X11, macOS and Windows.

## Installation

* [Flatpak](https://flathub.org/apps/details/com.github.unrud.RemoteTouchpad)
* [Snap](https://snapcraft.io/remote-touchpad)
* [macOS & Windows](https://github.com/Unrud/remote-touchpad/releases/latest)
* Golang:
  * Portal & uinput & X11:

    ```sh
    go install -tags portal,uinput,x11 github.com/unrud/remote-touchpad@latest
    ```
  * Windows:

    ```sh
    go install github.com/unrud/remote-touchpad@latest
    ```

### niri and other compositors without the RemoteDesktop portal

Control on Wayland normally goes through the `org.freedesktop.portal.RemoteDesktop`
portal, which only works if the compositor implements Mutter's remote desktop
interface. niri does not (yet), so the portal controller fails there.

This fork's Flatpak is built with the `uinput` controller and grants access to
`/dev/uinput` (`--device=all`), so it falls back to creating a virtual keyboard
and mouse that the compositor picks up like real hardware. `kbd`'s `loadkeys`
is bundled for keymap support.

Build the Flatpak locally with:

```sh
flatpak-builder --user --install --force-clean build-dir \
  flatpak/com.github.unrud.RemoteTouchpad.yaml
```

If you build with the sandboxed `org.flatpak.Builder` instead, export and install
from the host afterwards: the builder rewrites the exported `.desktop` file with
its own sandboxed `flatpak` path, which breaks launching from the app menu.

```sh
flatpak build-export host-repo .build-dir master
flatpak remote-add --user --no-gpg-verify local-repo "file://$PWD/host-repo"
flatpak install --user local-repo com.github.unrud.RemoteTouchpad
```

## Screenshots

![screenshot 1](https://raw.githubusercontent.com/Unrud/remote-touchpad/master/screenshots/1.png)

![screenshot 2](https://raw.githubusercontent.com/Unrud/remote-touchpad/master/screenshots/2.png)

![screenshot 3](https://raw.githubusercontent.com/Unrud/remote-touchpad/master/screenshots/3.png)

![screenshot 4](https://raw.githubusercontent.com/Unrud/remote-touchpad/master/screenshots/4.png)
