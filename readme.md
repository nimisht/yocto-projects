# Notes

## Troubleshooting 

### Make sure all dependencies are installed

```
sudo apt-get install autoconf automake bzip2 cmake flex g++ gawk gcc gettext git gperf help2man libncurses5-dev libstdc++6 libtool libtool-bin make patch python3-dev rsync texinfo unzip wget xz-utils zstd lz4
```

### Resolving ERROR: Nothing RPROVIDES 'linux-firmware-rpidistro-bcm43455'

add the line below to your `conf/local.conf` file

```
LICENSE_FLAGS_ACCEPTED = "synaptics-killswitch"
```

### To deal with "user namespaces are not usable by Bitbake, possibly due to AppArmor", do the following

```
sudo touch /etc/apparmor.d/bitbake
sudo nano /etc/apparmor.d/bitbake
abi <abi/4.0>,
include <tunables/global>
profile bitbake /**/bitbake/bin/bitbake flags=(unconfined) {
userns,
}
then, run :
sudo apparmor_parser -r /etc/apparmor.d/bitbake
```
