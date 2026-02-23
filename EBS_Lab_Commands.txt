EBS LAB EXPERIMENT COMMANDS (Complete Flow)

  ---------------------------------------------
  PART 1: Partition, Format, Mount, Permanent
  ---------------------------------------------

lsblk sudo fdisk /dev/nvme1n1

Inside fdisk:

n p Enter Enter Enter w

sudo partprobe
 lsblk 
sudo mkfs -t ext4 /dev/nvme1n1p1 
sudo mkdir -p /mnt/lucky 
sudo mount /dev/nvme1n1p1 /mnt/lucky 
df -h 
sudo blkid /dev/nvme1n1p1

-----Add UUID entry to /etc/fstab

sudo nano /etc/fstab

Add line (replace UUID):

UUID=your-uuid-value /mnt/lucky ext4 defaults,nofail 0 2

sudo systemctl daemon-reload 
sudo mount -a 
df -h 
sudo reboot
df -h(reconnect)
  ------------------------------
  PART 2: Detach Volume (AWS
  Console)
  ------------------------------
  EC2 → Volumes → Select Volume
  → Actions → Detach Volume

  ------------------------------

PART 3: Attach to New EC2 Instance

EC2 → Volumes → Select Volume → Actions → Attach Volume → Select new
instance

  -------------------------------
  PART 4: Mount in New Instance
  -------------------------------

ssh -i key.pem ubuntu@ 
lsblk 
sudo mkdir -p /mnt/lucky 
sudo mount /dev/nvme1n1p1 /mnt/lucky df -h

NOTE: Do NOT run mkfs again after reattaching, otherwise data will be
erased.
