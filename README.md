# packaging mollysocket for aur
- determine maintainer

## todo
- pgp keys

## Directories/packages
### mollysocket
- versioned package
- must increment `pkgver` in `PKGBUILD` for every release
- rerun `makepkg --printsrcinfo > .SRCINFO` after

### mollysocket-git
- pulls straight from the `HEAD` of the `main` branch of mollysocket
- no need to increment version
- if updating PKGBUILD, increment `pkgrel`

## Files
### Aur
#### `PKGBUILD`
- the main packaging file
- update file hashes in `sha256sums` section if updating auxiliary files in `source`

#### `.SRCINFO`
- is built from running `makepkg --printsrcinfo > .SRCINFO`
- needs an archlinux based distro because of makepkg
	- can be edited by hand otherwise

#### `config.toml`
- create an initial config file in `/etc/mollysocket`
- needed so unpriviledged users can run `sudo mollysocket connection add ...` while pointing to the correct db

### SystemD
#### `mollysocket.service`
- main systemd unit file

#### `sysuser.conf`
- systemd will create `mollysocket` user and group and set its home directory to `/var/lib/mollysocket`

#### `mollysocket.tmpfile.d`
- systemd will create `/var/lib/mollysocket/` directory as the `mollysocket` user

#### `mollysocket.install`
- when uninstalling, list the leftover directories so the user can manually remove them if desired