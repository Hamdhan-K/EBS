# WORKING WITH EBS
## NAME: HAMDHAN
## REG NO: 212225020013

## Aim

To create and configure an Amazon Elastic Block Store (EBS) volume, attach and mount it to an Amazon EC2 instance, create a snapshot backup, and restore the snapshot to a new EBS volume.

---

## Algorithm / Steps

1. Create a new Amazon EBS volume with a size of 1 GiB.
2. Select the same Availability Zone as the EC2 instance.
3. Attach the EBS volume to the EC2 instance using `/dev/sdb`.
4. Connect to the EC2 instance using AWS Systems Manager Session Manager.
5. Check the available storage using `df -h`.
6. Create an `ext3` file system on the EBS volume.
7. Create the `/mnt/data-store` directory.
8. Mount the EBS volume to `/mnt/data-store`.
9. Configure `/etc/fstab` for automatic mounting.
10. Verify that the EBS volume is successfully mounted.
11. Create `file.txt` inside the mounted EBS volume.
12. Verify the contents of the created file.
13. Create an EBS snapshot named `My Snapshot`.
14. Delete `file.txt` from the original EBS volume.
15. Create a new EBS volume from the snapshot.
16. Attach the restored volume to the EC2 instance using `/dev/sdc`.
17. Create the `/mnt/data-store2` directory.
18. Mount the restored volume to `/mnt/data-store2`.
19. Verify that `file.txt` has been successfully restored.

---

## Program

### 1. Check Available Storage

```bash
df -h
```

### 2. Create an ext3 File System

```bash
sudo mkfs -t ext3 /dev/sdb
```

### 3. Create a Mount Directory

```bash
sudo mkdir /mnt/data-store
```

### 4. Mount the EBS Volume

```bash
sudo mount /dev/sdb /mnt/data-store
```

### 5. Configure Automatic Mounting

```bash
echo "/dev/sdb   /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
```

### 6. View the File System Configuration

```bash
cat /etc/fstab
```

### 7. Verify the Mounted Volume

```bash
df -h
```

### 8. Create a File in the EBS Volume

```bash
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
```

### 9. Read the File

```bash
cat /mnt/data-store/file.txt
```

### 10. Delete the File

```bash
sudo rm /mnt/data-store/file.txt
```

### 11. Verify File Deletion

```bash
ls /mnt/data-store/
```

### 12. Create a Mount Directory for the Restored Volume

```bash
sudo mkdir /mnt/data-store2
```

### 13. Mount the Restored EBS Volume

```bash
sudo mount /dev/sdc /mnt/data-store2
```

### 14. Verify Snapshot Restoration

```bash
ls /mnt/data-store2/
```

Expected output:

```text
file.txt
```

---

## Outputs

<img width="1917" height="867" alt="Screenshot 2026-11-11 201156" src="https://github.com/user-attachments/assets/1123bafb-84da-4157-a7e0-9c732f4eca9b" />
<img width="1917" height="937" alt="Screenshot 2026-11-11 201346" src="https://github.com/user-attachments/assets/5b96206b-bdff-4f05-b5f7-7145ce9dc941" />
<img width="1916" height="898" alt="Screenshot 2026-11-11 202311" src="https://github.com/user-attachments/assets/739bfd47-4449-4566-8d0c-c66c8389acd4" />
<img width="1917" height="957" alt="Screenshot 2026-11-11 202642" src="https://github.com/user-attachments/assets/5d5bdfc3-159f-42ad-b41b-2797a9677c7f" />
<img width="1902" height="917" alt="Screenshot 2026-11-11 203011" src="https://github.com/user-attachments/assets/85069483-5e51-4b28-97fb-af58c3eff118" />
<img width="1917" height="992" alt="Screenshot 2026-11-11 203034" src="https://github.com/user-attachments/assets/3f24989f-46a5-4335-9b67-1bde645f9951" />
<img width="1916" height="941" alt="Screenshot 2026-11-11 203451" src="https://github.com/user-attachments/assets/412f2a00-1c6f-428d-be50-013d2c4597cb" />



## Result
Thus, an Amazon EBS volume was successfully created and attached to an Amazon EC2 instance. The volume was formatted with an ext3 file system, mounted, and used for storing data. An EBS snapshot was successfully created as a backup, and a new EBS volume was restored from the snapshot. The previously deleted file.txt was successfully recovered, demonstrating the backup and restore functionality of Amazon EBS.
