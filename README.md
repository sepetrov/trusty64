# Packer - Ubuntu Server 14.04.5 (Trusty Tahr) Vagrant Box


This Packer template builds [Ubuntu Server 14.04.5 (Trusty Tahr)](https://wiki.ubuntu.com/TrustyTahr/ReleaseNotes)
Vagrant box file.


## Prerequisites

 * [Packer](http://www.packer.io/)
 * [Vagrant](http://vagrantup.com/)
 * [VirtualBox](https://www.virtualbox.org/)

## Usage

1. Local build.

         $ packer build trusty64.json

   The above command will produce the file `trusty64.box`. You can now import
   the Vagrant box.

         $ vagrant box add --provider virtualbox trusty64 trusty64.box

   To create a virtul machine, you just need to create a `Vagrantfile` with box
   `trusty64` and use vagrant to build it for you.

         $ vagrant init trusty64
         $ vagrant up


2. Remote build using [HashiCorp](https://www.hashicorp.com/)'s
   [Atlas](https://atlas.hashicorp.com/).

   Use the [atlas](https://github.com/sepetrov/trusty64/tree/atlas) branch,
   which has support for remote builds.


## HOWTO

### Verify VirtualBox Guest Additions

    $ lsmod | grep -i vbox
    $ modinfo vboxguest

### Generate preconfiguration file

Information about preseeding can be found in the [Ubuntu Installation Guide](https://help.ubuntu.com/lts/installation-guide/armhf/apb.html).
To generate a preseed file, you need to complete an installation manually and
run the following commands.

    # apt-get install debconf-utils
    # debconf-get-selections --installer > /path/to/preseed.cfg
    # debconf-get-selections >> /path/to/preseed.cfg

## License

See [LICENSE](LICENSE).

## Author

[Stanislav Petrov](https://github.com/sepetrov)
