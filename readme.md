# To deal with "user namespaces are not usable by Bitbake, possibly due to AppArmor", do the following:

`
sudo touch /etc/apparmor.d/bitbake
sudo nano /etc/apparmor.d/bitbake
abi <abi/4.0>,
include <tunables/global>
profile bitbake /**/bitbake/bin/bitbake flags=(unconfined) {
userns,
}
then, run :
sudo apparmor_parser -r /etc/apparmor.d/bitbake
`
