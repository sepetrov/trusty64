# Packer - Ubuntu Server 14.04.3 (Trusty Tahr) Vagrant Box


This Packer template builds [Ubuntu Server 14.04.3 (Trusty Tahr)](https://wiki.ubuntu.com/TrustyTahr/ReleaseNotes) Vagrant box file for VirtualBox with Guest Additions 5.0.10.

    Local builds fail, because Packer does not have the option to exclude the
    post-processor "atlas" during a build. Use the branch "local" for local builds.

## Prerequisites

 * [Packer](http://www.packer.io/)
 * [Vagrant](http://vagrantup.com/)
 * [VirtualBox](https://www.virtualbox.org/)

## Usage

1. Local build.

   Use the [local](https://github.com/sepetrov/trusty64/tree/local) branch for local builds.

2. Remote build ([Atlas](https://atlas.hashicorp.com/)).

   Create a file with the Packer variables.

         $ cat <<EOF > variables.json
         {
            "atlas_username": "Your Atlas username",
            "atlas_name": "Your Atlas build name",
            "atlas_token": "Your Atlas build token"
         }
         EOF

   Push the configuration and trigger a new build.

         $ packer push -var-file=variables.json trusy64.json

   Create **Vagrantfile** using your {{atlas_username}}/{{atlas_name}} box, and build the virtual machine.

         $ vagrant init {{atlas_username}}/{{atlas_name}}
         $ vagrant up


## HOWTO

### Verify VirtualBox Guest Additions

    $ lsmod | grep -i vbox
    $ modinfo vboxguest

### Generate preconfiguration file

Information about preseeding can be found in the [Ubuntu Installation Guide](https://help.ubuntu.com/lts/installation-guide/armhf/apb.html). To generate a preseed file, you need to complete an installation manually and run the following commands.

    # apt-get install debconf-utils
    # debconf-get-selections --installer > /path/to/preseed.cfg
    # debconf-get-selections >> /path/to/preseed.cfg

## License

[MIT license](LICENCE.md).

## Author

[Stanislav Petrov](https://github.com/sepetrov)
