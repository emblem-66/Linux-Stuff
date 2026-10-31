# BTRFS

Work in progress

```
https://btrfs.readthedocs.io/en/latest
```

## RAID1

### create btrfs raid 1

List drives
```
lsblk -f
```
Create raid1
```
wipefs /dev/sdX /dev/sdY
mkfs.btrfs -L label -m raid1 -d raid1 /dev/sdX /dev/sdY
```
Check raid1
```
lsblk -f
```
Same UUID for 2 drives

### mount btrfs raid 1

Check raid1 UUID
```
lsblk -f
```

Add to `/etc/fstab`

```
UUID=<raid1-uuid> /mnt/raid      btrfs   defaults,noatime,compress=zstd:3,nofail,x-systemd.device-timeout=10 0 0
```

Options:
- defaults
- noatime



Check
Should show stats for both /dev/sdX and /dev/sdY
```
sudo btrfs filesystem show /mnt/raid
sudo btrfs filesystem usage /mnt/raid
sudo btrfs scrub start -Bd /mnt/raid
sudo btrfs device stats /mnt/raid
```

## Subvolumes

### create subvolumes

```
btrfs subvolume create 
```

### mount subvolumes


UUID=<> /srv/movies    btrfs   subvol=movies,ro,noatime,nodev,nosuid,noexec,compress=zstd:3,nofail,x-systemd.device-timeout=10 0 0


## Snapshots



sudo btrfs device stats /mnt/pool
btrfs device stats --check
btrfs device stats --check /mnt/pool/


### Automation with btrbk

```
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
```


#### Note: these are just my personal notes on how I setup btrfs raid1. Claude/Gemini/ChatGPT heavily involved. DO NOT USE, you may risk your data.
