This is an Arch Linux package for
[udp-obfuscat](https://github.com/vehlwn/udp-obfuscat) service.

## Build

```bash
makepkg -si
```

Now change options as needed in `/etc/udp-obfuscat/config.env` and start service:

```bash
sudo systemctl start udp-obfuscat.service
```
