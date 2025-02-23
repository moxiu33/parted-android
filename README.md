 # parted-android

> [!WARNING]  
> - Do this at your own risk!  
> - This might brick your device. **Backup before proceeding.**  
> - Avoid PMing me if you have questions.

### **Preparation:**
1. **Extract Files:**  
   - Place the extracted files in `/sbin` and set permissions to `755`.

### **Using Terminal or ADB Shell:**
1. **Launch Parted:**
   ```bash
   parted /dev/block/mmcblk0  # or /dev/block/sda, depending on your device
   ```

2. **List Partitions:**
   ```bash
   p
   ```
   - *Take pictures of this list for reference.*

3. **Remove System Partition:**
   ```bash
   rm x  # replace x with the system partition number (e.g., rm 13)
   ```

4. **Remove Data Partition:**
   ```bash
   rm 67  # replace 67 with the actual data partition number
   ```

5. **List Partitions Again:**
   ```bash
   p
   ```
   - *Confirm that the partitions have been removed.*

6. **Create New System Partition:**
   ```bash
   mkpart system ext4 xMB yMB  
   # x: endpoint of last partition, y: desired size (nGB*1024+x)
   ```

7. **List Partitions Again:**
   ```bash
   p
   ```
   - *Check the endpoint of the new system partition.*

8. **Create New Userdata Partition:**
   ```bash
   mkpart userdata yMB zGB  
   # z: should match the size from the first list
   ```

9. **Final Partition List:**
   ```bash
   p
   ```

10. **Quit Parted:**
    ```bash
    q
    ```

### **Final Steps:**
1. **Reboot to Recovery.**
2. **Format the New Partitions:**
   - For **System:** Change Filesystem to **ext4**.
   - For **Data:** Select **Format Data**.

**If formatting fails, try restarting recovery.**
