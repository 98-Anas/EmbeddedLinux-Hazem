# Fifth Session

- # Steps to create a filesystem on a sd card
    1. Connect sd card and make sure it is available in devices `lsblk`
    2. Mount and Format
    3. Use `Gparted` to create Primary Partitions
    4. Write the new partitions to the sd card
    5. Verify the new partitions with `lsblk`
    6. Create Filesystems on the partitions
    7. Verify the new partitions with `Gparted`
    8. Mount each filesystem to a mountpoint using `mount -t {{filesystem_type}} {{path/to/device_file}}
{{path/to/target_directory}}`
>⚠️ ***Becareful while mounting that you have to mount each filesystem into a certain directory***
---
- # Usecase of filesystems
    - ## Task A:
        -   ***Overlay*** : It is a union filesystem in the kernel that allows us to use a Read/Only directory as a Read/Write directory without "" for only the current power cycle..
        -   `mount -t overlay overlay -o lowerdir=/lower,upperdir=/upper,workdir=/work /merged`
            -  The lower directory can be read-only or could be an overlay itself.
            -  The upper directory is normally writable.
            -  The workdir is used to prepare files as they are switched between the layers.   
    - ## Task B:
        -   New mounting point will hide the first mounting point, the files that was in the mounting point at first still exist but they will be unaccessable (and unharmed) until you remove the new mounting point and go back to the old mounting point.
---
- ## Extras
    - Linux Adminstration (Great Material for learning general linux stuff)--> http://linux-training.be/
    - Overlays --> https://wiki.archlinux.org/title/Overlay_filesystem
