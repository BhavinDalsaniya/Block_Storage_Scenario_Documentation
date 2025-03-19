# Block_Storage_Scenario_Documentation

This repository documents the steps performed to create and manage block storage on AWS EC2 instances. The scenario includes creating a file on the first EC2 instance, creating a snapshot of the volume, creating a new volume from the snapshot, attaching it to a second EC2 instance, and verifying the data.

Steps Performed
On the First EC2 Instance
Create a Directory and File

- ```bash
  mkdir -p ~/mydir
  cd ~/mydir
  echo "Hello, this is my test file!" > hello.txt
  cat hello.txt
  ls -l hello.txt
mkdir -p ~/mydir: Creates a directory named mydir in the home directory.

cd ~/mydir: Navigates into the mydir directory.

echo "Hello, this is my test file!" > hello.txt: Creates a file named hello.txt with the specified content.

cat hello.txt: Displays the contents of the file.

ls -l hello.txt: Lists the file details.

Creating a Snapshot
Go to the AWS Management Console.

Navigate to EC2 > Volumes.

Select the volume attached to the first EC2 instance (e.g., /dev/xvdd1).

Click Actions > Create Snapshot.

Provide a description and name for the snapshot.

Click Create Snapshot.

Creating a Volume from the Snapshot
Go to EC2 > Snapshots.

Select the snapshot you just created.

Click Actions > Create Volume.

Specify the volume type, size, and availability zone (ensure it matches the region of your second EC2 instance).

Click Create Volume.

Attaching the Volume to the Second EC2 Instance
Go to EC2 > Volumes.

Select the newly created volume.

Click Actions > Attach Volume.

Select the second EC2 instance from the list.

Specify the device name (e.g., /dev/sdf).

Click Attach.

On the Second EC2 Instance (After Attaching the Volume)
Verify the Attached Volume

bash
Copy
lsblk
lsblk: Lists all block devices attached to the instance.

Check the File System and Repair if Necessary

bash
Copy
sudo file -s /dev/xvdf1
sudo fsck -y /dev/xvdf1
sudo file -s /dev/xvdf1: Checks the file system type of the attached volume.

sudo fsck -y /dev/xvdf1: Checks and repairs the file system if needed.

Mount the Volume

bash
Copy
sudo mkdir -p /mnt/mydata
sudo mount /dev/xvdf1 /mnt/mydata
sudo mkdir -p /mnt/mydata: Creates a directory for mounting the volume.

sudo mount /dev/xvdf1 /mnt/mydata: Mounts the volume to the directory.

Verify the Data

bash
Copy
ls -l /mnt/mydata/home/ubuntu/mydir/
cat /mnt/mydata/home/ubuntu/mydir/hello.txt
ls -l /mnt/mydata/home/ubuntu/mydir/: Lists the contents of the mounted directory.

cat /mnt/mydata/home/ubuntu/mydir/hello.txt: Displays the contents of the file to verify the data.

Summary
This scenario demonstrates how to:

Create and manage files on an EC2 instance.

Create a snapshot of a volume.

Create a new volume from the snapshot and attach it to a second EC2 instance.

Verify the data on the second EC2 instance.
