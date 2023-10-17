# AMD SFH dkms driver for ASUS TM420 laptop
This repo contains an old version of the amd_sfh_hid driver that works for the ASUS TM420 laptop model.

The code is taken from this [commit](https://github.com/torvalds/linux/commit/a6e757e3a1c723341004fe55403970f9c7b83f4c) of the linux kernel, released with version 5.16, as it was the only working version of the driver for this laptop series.

## Installation

1. Install dkms using your package manager, here's an example for ubuntu
```bash
sudo apt install dkms
```

2. Clone the repo
```bash
mkdir /usr/src/amd_sfh-dkms-1.0
cd /usr/src/amd_sfh-dkms-1.0
git clone https://github.com/paolo-sofia/amd-sfh-hid-dkms-asus.git
```

3. Build the kernel module
```bash
sudo dkms add amd_sfh-dkms/1.0
sudo dkms build amd_sfh-dkms/1.0
```

4. If building was successfull, install the module
```bash
sudo dkms install amd_sfh-dkms/1.0
```

5. Unload official amd_sfh module
```bash
sudo modprobe -r amd_sfh
```

6. Update kernel boot parameter to block loading the original amd_sfh module.
Add this string to the kernel boot parameter string:
`modprobe.blacklist=amd_sfh` 
This step can be done in different ways depending on the distro, in ubuntu you need to edit the grub line GRUB_CMDLINE_LINUX_DEFAULT

For fedora use this command:
```bash
sudo grubby --update-kernel=ALL --args=modprobe.blacklist=amd_sfh
```

7. Reboot
After rebooting you should have the autorotation working

## Tested Environments
Hardware: ASUS TM420IA-EC065T
OS: Fedora 38
Kernel: 6.5.6
DE: GNOME 44.5
Window protocol: Wayland
CPU: AMD Ryzen 5 4500U (Renoir)
packages: 
- iio-sensor-proxy: 3.4-3 

## References
- https://github.com/torvalds/linux/tree/master/drivers/hid/amd-sfh-hid
- https://github.com/conqp/amd-sfh-hid-dkms


## Code Contributors

[[Contribute](CONTRIBUTING.md).
<a href="https://github.com/paolo-sofia/amd-sfh-hid-dkms-asus/graphs/contributors"><img src="https://opencollective.com/readme-md-generator/contributors.svg?width=890&button=false" /></a>

## Contributing

Contributions, issues and feature requests are welcome.<br />
Feel free to check [issues page](https://github.com/paolo-sofia/amd-sfh-hid-dkms-asus/issues) if you want to contribute.<br />
[Check the contributing guide](./CONTRIBUTING.md).<br />

## Author

**Paolo Sofia**

- Github: [@paolo-sofia](https://github.com/paolo-sofia)

## License

This project is [GPL-3.0](https://github.com/paolo-sofia/amd-sfh-hid-dkms-asus/blob/master/LICENSE) licensed.
