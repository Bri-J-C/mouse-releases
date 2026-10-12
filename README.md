# Mouse

Use your phone as a secure Wi-Fi touchpad and keyboard for your Windows and
Linux computers.

**[Download the latest release](https://github.com/Bri-J-C/mouse-releases/releases/latest)**

## Install

### Windows 10/11

1. Download **Mouse-Setup.exe** (or **Mouse-Setup-arm64.exe** for ARM PCs).
2. Run it and accept the administrator prompt. If Windows shows "Windows
   protected your PC", choose *More info* → *Run anyway*.
3. It installs Mouse, allows it through the firewall for your local network,
   starts it, and shows a **6-digit PIN**. Mouse then starts by itself whenever
   you log in.

The PIN is also in `%APPDATA%\mouse\mouse.log`. Uninstall from
*Settings → Apps → Mouse*.

### Linux (X11 or Wayland)

```sh
sudo install -m644 70-mouse-uinput.rules /etc/udev/rules.d/
sudo udevadm control --reload && sudo udevadm trigger --name-match=uinput
chmod +x mouse-linux-amd64 && ./mouse-linux-amd64    # prints the PIN
```

Use `mouse-linux-arm64` on ARM (e.g. Raspberry Pi). Allow UDP port 47474 if a
firewall is enabled. Typing on Linux uses a US keyboard layout.

### Android phone

Install the app (Google Play listing coming, or **Mouse.apk** from the
release), open it, tap your computer and enter its PIN once. After that the
phone connects by itself.

## Security

- All traffic between phone and computer is **encrypted and authenticated**
  (AES-256-GCM) with a fresh **ECDH key exchange** for every connection.
- The PIN is used once to pair; after that each phone has its own random key.
  Recorded traffic can't be used to guess the PIN or decrypt sessions later.
- Forged, replayed or tampered packets are rejected.
- Mouse talks only to devices on your local network. No accounts, cloud
  relay, ads or analytics; nothing is sent to the internet.
- The computer program **never updates itself** and makes no internet
  connections. When a newer version is out, the phone app marks that computer
  "update available"; you update it by running the new Mouse-Setup.exe there.
  (Computers on 1.5.7 or earlier make one last automatic update, to 1.5.8.)
- Each release's `manifest.json` lists every file's SHA-256 and is signed
  (`manifest.sig`, Ed25519) with the project's release key.

Pair on a network you trust: someone actively impersonating your computer at
the exact moment you pair could still attack the PIN.

## Privacy

See [PRIVACY.md](PRIVACY.md). In short: Mouse collects nothing.

## Support

Questions and bug reports: [open an issue](https://github.com/Bri-J-C/mouse-releases/issues).
