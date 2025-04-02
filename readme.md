# Notes

## Troubleshooting 

### Make sure all dependencies are installed

```
sudo apt-get install autoconf automake bzip2 cmake flex g++ gawk gcc gettext git gperf help2man libncurses5-dev libstdc++6 libtool libtool-bin make patch python3-dev rsync texinfo unzip wget xz-utils zstd lz4
```

```
sudo apt install e2fsprogs genext2fs mtd-utils squashfs-tools util-linux
```

### Resolving ERROR: Nothing RPROVIDES 'linux-firmware-rpidistro-bcm43455'

add the line below to your `conf/local.conf` file

```
LICENSE_FLAGS_ACCEPTED = "synaptics-killswitch"
```

### To deal with "user namespaces are not usable by Bitbake, possibly due to AppArmor", do the following:

Create this file
```
sudo touch /etc/apparmor.d/bitbake
```

Edit the file, using any editor or just use nano
```
sudo nano /etc/apparmor.d/bitbake
```

Copy-paste or rewrite the lines below into the file

```
abi <abi/4.0>,
include <tunables/global>
profile bitbake /**/bitbake/bin/bitbake flags=(unconfined) {
userns,
}
```
then, run
```
sudo apparmor_parser -r /etc/apparmor.d/bitbake
```

if you're still having issues, disable AppArmour entirely as follows:

```
echo 0 | sudo tee /proc/sys/kernel/apparmor_restrict_unprivileged_userns
```

### Mender troubleshooting

To set up the docker demo for Mender server, follow the instructions on this webpage: https://docs.mender.io/server-installation/evaluation-with-docker-compose
