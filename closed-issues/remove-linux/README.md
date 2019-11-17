# Removing Ubuntu

Removing Ubuntu is a two part process:

1. Remove the Ubuntu partition along with all of its files.
2. Remove the GRUB boot-loader.



## Removing Ubuntu Partition

1. From Windows, open the start menu and search and open `diskmgmt.msc`.
2. Identify your Ubuntu partition. This can be done by looking for the partition that is in the `ext4` format and recalling the amount of space you assigned to Ubuntu during installation. You can also do this by eliminating the drives that are clearly being used by Windows by the labels being assigned to them.
3. Once Ubuntu partition has been identified, right click the partition and delete the partition. Needless to say, this will delete all your files in your Ubuntu partition.
4. (Optional) You may optionally have to also delete your swap space assigned to the Ubuntu.
5. Right click your Windows partition and click extend partition to reclaim the space forfeited by Ubuntu.
6. DO NOT RESTART PC UNTIL YOU HAVE REMOVED GRUB BOOT-LOADER.



## Removing Grub Boot Loader

These steps are based on this [post](https://askubuntu.com/questions/429610/uninstall-grub-and-use-windows-bootloader). (armadadrive's answer). The steps are outlined here if something happens to that post in the future.

1. Run a `cmd.exe` process with administrator privileges
2. Run `diskpart`
3. Type: `list disk` then `sel disk X` where `X` is the drive your boot files reside on.
4. Type `list vol` to see all partitions (volumes) on the disk (the EFI volume will be formatted in FAT, others will be NTFS)
5. Select the EFI volume by typing: `sel vol Y` where Y is the `SYSTEM` volume (this is almost always the EFI partition)
6. For convenience, assign a drive letter by typing: `assign letter=Z:` where Z is a free (unused) drive letter
7. Type `exit` to leave disk part
8. While still in the `cmd` prompt, type: `Z:` and hit enter, where Z was the drive letter you just created.
9. Type `dir` to list directories on this mounted EFI partition
10. If you are in the right place, you should see a directory called `EFI`
11. Type `cd EFI` and then `dir` to list the child directories inside `EFI`
12. Type `rmdir /S ubuntu` to delete the Ubuntu boot directory.



You have successfully deleted Ubuntu and GRUB Boot-loader and you can now restart your PC and boot into windows safely.

If GRUB is still giving problems, check if the BIOS has any mentions of Ubuntu and change them to windows.