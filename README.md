## THIS IS A GUIDE TO INSTALL OMARCHY ON DISK PARTITION

since we dont have an official way to install omarchy on partition disk. I am writing this guide to help myself to follow and install without any issue

First thing I understood is we need to create a seperate partition with enough space. 
    - from windows, we need to go the "Create and Partition tool" or Disk Management tool 
    - Create some free space which we are going to use for our installation.
        - If you dont have free space, we can create a new volume, which can be selected from shrink the existing drive space and free up space for new volume

Once we have the space required, we are good to go.

2. Install omarchy ISO from official website. (https://omarchy.org/)
 - Flash the ISO on a pendrive. balenaEtcher or Rufus is recommended

3. Installing the Omarchy  

- connect to Wifi 
        - iwctl
        - device list
        - station wlan0 scan
        - station wlan0 get-networks
        - station wlan0 connect <wifi_name>
        - exit post that
        - check : ping -c 5 archlinux.org

- We need to start with creating the partitioning of the disk
    - use lsblk for seeing the partitions 
    - cfdisk <replace with your disk name in the above command>
    - After that, delete the parition, and delete it for free space
    - Create 2 paritions 
        - 1 GB for boot : EFI file system 
        - rest for our disk : btrfs
    - Check lsblk to see if we partitioned it correctly
    
- Coverting the partitions to correct file systems 
    - convert the boot (1GB) to fat32 format
        - mkfs.fat -F32 <disk name>
    - Convert the other to 
        - mkfs.btrfs <disk name>

- Do the mounting as required 
    - mount <btsfs disk name>  /mnt
    - btrfs su cr /mnt/@
    - btrfs su cr /mnt/@home
    - btrfs su cr /mnt/@pkg
    - btrfs su cr /mnt/@log

- Mount the sub volumnes
    - umount /mnt
    - mount -o noatime,compress=zstd,discard=async,space_cache=v2,subvol=@ <btrfs_disk_name> /mnt 
    - mkdir -p /mnt/home
    - mkdir -p /mnt/var/cache/pacman/pkg
    - mkdir -p /mnt/var/log

    - mount -o noatime,compress=zstd,discard=async,space_cache=v2,subvol=@home /dev/nvme0n1p5 /mnt/home
    - mount -o noatime,compress=zstd,discard=async,space_cache=v2,subvol=@pkg /dev/nvme0n1p5 /mnt/var/cache/pacman/pkg
    - mount -o noatime,compress=zstd,discard=async,space_cache=v2,subvol=@log /dev/nvme0n1p5 /mnt/var/log

    - mkdir -p /mnt/boot
    - mount /dev/nvme0n1p4 /mnt/boot

--Disk configuration -> Pre-Mounted configuration -> /mnt






references : 
- https://github.com/basecamp/omarchy/discussions/900
- https://github.com/basecamp/omarchy/discussions/1651
- https://learn.omacom.io/2/the-omarchy-manual/96/manual-installation

- https://www.youtube.com/watch?v=WaWB3F-ffcI

