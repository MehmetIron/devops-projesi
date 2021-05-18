# 1. case

# add 10 GB volume to centos 7 in VM Virtual Box by manuel

# update the installed packages and package cache
sudo yum update -y

# add a new user
sudo adduser mehmet.demir

# change user and assign password to user
su - mehmet.demir
sudo passwd mehmet.demir

# we can't do anything other than root privilege, we will give root privilege once
exit
sudo vim /etc/sudoers
mehmet.demir    ALL=(ALL=ALL)   ALL

# again change user
su - mehmet.demir

# root volume and secondary volume should be listed
lsblk
df -h

# show the current partitions
sudo fdisk -l

# check all available fdisk commands and using "m"
sudo fdisk /dev/sdb
    # n -> add new partition (with 1G size)
    # p -> primary
    # Partition number: 1
    # First sector: default - use Enter to select default
    # Last sector: +1g   (you can also type sector)
    # w -> write partition table

# show new partitions
lsblk

# format the new partitions
sudo mkfs -t ext4 /dev/sdb1

# create a mounting point path for new volume
cd /opt
sudo mkdir bootcamp
cd bootcamp
echo "Merhaba Trendyol" > bootcamp.txt

# mount the new volume to the mounting point path
sudo mount /dev/sdb1 /mnt/bootcamp

# list volumes to show current status, all volumes and partittions should be listed
lsblk

# show the used and available capacities related with volumes and partitions
df -h

# back up the /etc/fstab file.
sudo cp /etc/fstab /etc/fstab_backup

# open /etc/fstab file and add the following info to the existing
sudo vim /etc/fstab
/dev/sdb1   /mnt/bootcamp   ext4    defaults,nofail 0   0

# reboot and show that configuration exists
sudo reboot now

# list volumes to show current status, all volumes and partittions should be listed
lsblk

# show the used and available capacities related with volumes and partitions
df -h

# find and move bootcamp.txt file
sudo find / -name bootcamp.txt -type f -exec mv "{}" /mnt/bootcamp/ \;
# sudo find / -name bootcamp.txt -type f | mv $(sudo find / -name deneme.txt -type f) /mnt/bootcamp/
