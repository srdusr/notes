### Create/Resize partitions using LVM (Logical Volume Manager)
  Useful if we want a flexible disk storage that we either need to create separate partitions on, be able to resize them on the fly or create snapshots.  
  NOTE: LVM is exclusive to linux, no offical support in most other OS's (Windows,FreeBSD..) and is redundent on filesystems like BTRFS since it has it's own Subvolume feature.
#### LVM Concepts:  
  LVM is a Linux's native paritition type, other partition types are PC (MBR or GPT) that are considered standard and don't have the cool features of LVM.
  - Device Mapper or dev/mapper (not exclusive to LVM) is a framework for mapping physical block devices onto higher-level virtual block devices
  - Physical Volumes occupy the "whole of" or a partition of the actual disks/drives that are phyically present.  
  - Volume Groups are the overall collection of one or more physical volumes that encompass/split logical volumes.  
  - Logical Volumes are the divided partitions of a volume group between potentially more than one disk/drive.  
  ```bash  
   ┌───────────────────────┐┌─────────────────────────────┐
   │  Physical Hard Drive  ││    Physical Hard Drive      │
   └───────────────────────┘└─────────────────────────────┘
                            ┌───────────────────────┐
                            │       Partition       │
                            └───────────────────────┘
   ┌───────────────────────┐┌───────────────────────┐
   │    Physical Volume    ││    Physical Volume    │
   └───────────────────────┘└───────────────────────┘
   ┌────────────────────────────────────────────────┐
   │                 Volume Group                   │
   └────────────────────────────────────────────────┘
   ┌───────────────────┐ ┌──────────────────────────┐
   │  Logical Volume   │ │      Logical Volume      │
   └───────────────────┘ └──────────────────────────┘
   ┌───────────────────┐ ┌──────────────────────────┐
   │    Filesystem     │ │        Filesystem        │
   └───────────────────┘ └──────────────────────────┘
  ```
#### Create/Extend/Reduce:
  1. First list/find out information about the partitions  
  `$ fdisk -l` # Needs root privileges,  
  `$ df -h` # Displays amount of disk space on filesystems, "-h" in human readable form  
  `$ lsblk` # List/find information about avaliable block devices/partitions
  - Find info about VG(Volume Groups), PV(Physical Volumes) and LV(Logical Volumes):  
      - hello  
      `$ vgs` # Needs root privileges,  
      - hello  
      `$ lvs`
      - Report information about Physical Volumes  
      `$ pvs` # Needs root privileges,

  2. Unmount the partition/filesystem making sure we are not on it:  
  NOTE: It is best not to be on the filesystem currently being managed although it's possible on EXT3 and EXT4 but BTRFS and ZFS need the use of a program called grow (still safe to gather/list information on them though).  
  - Change to a different user and kill any processes of the target filesystem's user.  
  `$ su root` # If going to change (extend/reduce) a user's filesystem  
  `$ pkill <user>` # Make sure user's processes aren't running  
  or  
  `$ su <user>` # If going to change (extend/reduce) the root's filesystem  
  then  
  `umount /dev/path/<home_or_root>`  

  3. Create/resize partitions  
  - Create:  
    - Create the Logical Volume from existing free space within the Volume Group. The command below creates a LV with a size of 60GB from the VG called "vg1" and LV name is Stuff  
    NOTE: Always make meaningful volume and volume group names.  
    `$ lvcreate -L +60G --name Stuff vg1`  
    - Create a filesystem, creating the Logical Volume does not create the filesystem. The command below creates an EXT4 filesystem that fits the newly created Logical Volume.  
    `$ mkfs -t ext4 /dev/vg1/Stuff`  
Add a filesystem label  

Adding a filesystem label makes it easy to identify the filesystem later in case of a crash or other disk related problems.  

e2label /dev/MyVG01/Stuff Stuff  
  - Resize:  
    - Reduce the Logical Volume:  
    - Extend the Logical Volume:  

Extend the Logical Volume (LV) from existing free space within the Volume Group. The command below expands the LV by 50GB. The Volume Group name is MyVG01 and the Logical Volume Name is Stuff.  

lvextend -L +50G /dev/MyVG01/Stuff  
  sudo lvextend -l 100%VG -r /dev/mapper/vg1-root  
  4. Mount the partition  


    ```
    umount /dev/mapper/vg1-root
    umount /dev/mapper/vg1-home
    lvresize --resizefs -L -20G /dev/mapper/vg1-home
    mount /dev/mapper/vg1-home
    ```

