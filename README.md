# limine-timeshift-sync

Boot Timeshift btrfs snapshots from the Limine menu, and restore them with the
kernel they were taken with.

- Lists the newest Timeshift snapshots under a "Timeshift snapshots" entry in
  `limine.conf`, each booting the kernel and initramfs it was taken with. Those
  are copied to the ESP before an upgrade replaces them.
- When booted into a snapshot, shows a "Snapshot detected!" notification
  offering to restore it.
- After Timeshift restores a snapshot, puts that snapshot's kernels back into
  the `limine.conf` entries they came from, so the restored system does not
  boot a kernel whose modules it lacks.

It keeps itself up to date through pacman hooks and a systemd timer, and
re-enrols the config when the loader has a config hash enrolled.

## Installing

On Arch Linux, install `limine-timeshift-sync` from the
[malik05](https://github.com/malik05051/malik05-repo) repository. It is built
from the [PKGBUILD](https://github.com/malik05051/malik05-repo/tree/main/limine-timeshift-sync)
there.

## Usage

```
limine-timeshift-sync [--dry-run] [--remove]
limine-timeshift-sync --restore-kernels <snapshot>
limine-timeshift-restore [<snapshot>]
```

`limine-timeshift-restore` restores the snapshot the system was booted into, or
one picked from a list. It is also in the application menu as "Restore Timeshift
snapshot".

Settings are in `/etc/limine-timeshift-sync.conf`.
