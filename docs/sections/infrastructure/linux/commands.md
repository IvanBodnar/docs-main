# Commands
<hr>
<br>

#### Make bootable usb

- List devices

```
$ lsbk
```

- Unmount usb

```
$ sudo umount /dev/sdbX
```

- Create usb

```
$ sudo dd if=~/opt/ubuntu-19.04-desktop-amd64.iso of=/dev/sdb bs=4M && sync
```