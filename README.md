# guixify-pharo-vm

Shell script to get the Pharo VM and fix paths and libraries in order to work with GNU Guix distro.

The `guixify-pharo` script first`` downloads the Pharo VMs and images using the Pharo Zeroconf tool (you can read info about the Pharo Zeroconf at http://get.pharo.org/),
then it proceeds to apply some fixes and patches in order to make the VM usable in GNU Guix.

## Fixes for GNU Guix

GNU Guix does not conform to the Filesystem Hierarchy Standard (FHS). In practical terms, this means there is no global 
`/lib` containing libraries, `/`bin` containing binaries, and so on. This is very much at the core of how Guix works and some of the 
convenient features, like per-user installation of programs (different versions, for instance) and a declarative system configuration 
where the system is determined from a configuration file.

As some Linux command paths are hardcoded in the Pharo shell scripts following the FHS convention, the `guixify-pharo` script patches 
Pharo scripts to refer to absolute paths in the Guix store, like `/gnu/store/yr39rh6wihd1wv6gzf7w4w687dwzf3vb-coreutils-9.1/bin/dirname`
instead of `/usr/bin/dirname`.

