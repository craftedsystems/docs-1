# Developing using Nitro and WSL2

Tips for working with Nitro on Windows.

## Filesystem and Project Layout

The Windows filesystem can be accessed through your WSL2 distro via the `/mnt` folder.\
Put your Nitro projects _outside_ that folder (i.e. `~/dev/mysite.nitro`) for vastly better performance directly from the Linux filesystem instead of the shared `/mnt` folder.

You can access the Linux filesystem from Windows by accessing the `\\wsl$` share. If you use PhpStorm, you can load your project, for example, via `\\wsl$\Ubuntu-20.04\home\me\dev\mysite.nitro`. Performance is not as fast as the native filesystem, but faster than going through `/mnt`.

We recommend using [Visual Studio Code](https://code.visualstudio.com/) and installing the [Remote - WSL](https://code.visualstudio.com/docs/remote/wsl) plugin, which will mount the Linux filesystem on Windows inside of Visual Studio Code for the best performance.

## Permissions and Manual Setup Steps

When adding a new site, you’ll need to manually set permissions from the root of the Craft project from within the WSL2 distro:

- `chmod 777 ./.env`
- `chmod 777 ./composer.lock`
- `chmod 777 ./composer.json`
- `chmod -R 777 ./config`
- `chmod -R 777 ./storage`
- `chmod -R 777 ./vendor`
- `chmod -R 777 ./web`

The first time you add a Craft site, you’ll need to manually run a command on the Windows host machine to import a certificate file so SSL will work. You can follow the terminal output for exact instructions.

Nitro will not be able to edit the hosts file on the Windows machine at `C:\Windows\system32\drivers\etc\hosts`. Nitro commands that want to edit that file will give you the steps so you can manually perform the edit.