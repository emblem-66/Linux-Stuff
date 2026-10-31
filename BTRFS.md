# BTRFS

## RAID1

### create btrfs raid 1
'''
wipefs /dev/sdX /dev/sdY
mkfs.btrfs -L label -m raid1 -d raid1 /dev/sdX /dev/sdY
'''
### mount btrfs raid 1







## Subvolumes

### create subvolumes

wipefs /dev/sdX /dev/sdY
mkfs.btrfs -L label -m raid1 -d raid1 /dev/sdX /dev/sdY

### mount subvolumes



## Snapshots



sudo btrfs device stats /mnt/pool
btrfs device stats --check
btrfs device stats --check /mnt/pool/


### Automation with btrbk

❯ cat /etc/btrbk/btrbk.conf
# Keep every snapshot for at least 2 days, then thin out by age
snapshot_preserve_min   2d
snapshot_preserve       7d 4w 6m

# Only create a snapshot if the subvolume actually changed
snapshot_create         onchange

timestamp_format        long
lockfile                /var/lock/btrbk.lock

volume /mnt/pool
  snapshot_dir .snapshots
  subvolume movies
    snapshot_name movies
  subvolume documents
    snapshot_name documents

~
❯
