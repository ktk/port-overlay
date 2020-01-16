# port-overlay
Overlay for some FreeBSD ports

## Config

`netlabs` in `/usr/local/etc/portshaker.d`

```sh
#!/bin/sh
. /usr/local/share/portshaker/portshaker.subr
method="git"
git_clone_uri="https://github.com/ktk/port-overlay.git"
git_branch="master"
run_portshaker_command $*
```
