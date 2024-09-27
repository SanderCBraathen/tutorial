
### **Step 1: Download and Install Raspberry Pi Imager**
1. **Go to the Raspberry Pi website** and download the Raspberry Pi Imager:
   - [Download Raspberry Pi Imager](https://www.raspberrypi.org/software/)
2. **Install Raspberry Pi Imager** on your computer.

---

### **Step 2: Prepare the SD Card with Raspberry Pi OS**
1. **Open Raspberry Pi Imager**.
2. **Choose the Operating System**:
   - Select **Raspberry Pi OS (32-bit)** or **Raspberry Pi OS Lite** (if you want a minimal setup).
3. **Select Storage**:
   - Insert your SD card into your computer, and choose it as the target.
4. **Write the OS** to the SD card:
   - Click **Write** and wait for the process to finish.

---

### **Step 3: Boot the Raspberry Pi**
1. **Insert the SD card** into the Raspberry Pi.
2. **Connect the Raspberry Pi**:
   - Attach a monitor, keyboard, and mouse (if doing a headless setup, you can skip this step).
   - Connect to power, and the Raspberry Pi will boot.
3. **Follow the on-screen setup instructions**:
   - Set up country, language, and time zone.
   - Create a username and password (default is often `pi`/`raspberry` but you can change it).

---

### **Step 4: Connect Raspberry Pi to Wi-Fi or Ethernet**
1. **For Wi-Fi**:
   - If you are using a monitor and keyboard, you will be prompted to select a Wi-Fi network during setup.
   - Choose your Wi-Fi network and enter the password.
2. **For Ethernet**:
   - Simply plug in the Ethernet cable. It should automatically connect to the network.

---

### **Step 5: Update the Raspberry Pi**
It’s important to update the Raspberry Pi to ensure you have the latest security patches and software.

1. **Open the terminal** (or connect via SSH if headless):
   ```bash
   sudo apt update
   sudo apt upgrade -y
   ```
   
2. **Reboot** (optional, but recommended):
   ```bash
   sudo reboot
   ```

---

### **Step 6: Enable SSH (if using headless setup or remote access)**
SSH allows you to connect to your Raspberry Pi from another computer.

1. **Open terminal** and run:
   ```bash
   sudo raspi-config
   ```
2. **Navigate to Interface Options > SSH**, and enable it.
3. **Find your Raspberry Pi’s IP address**:
   ```bash
   hostname -I
   ```
4. **Connect via SSH** from another machine:
1. to find your IP address then **Open terminal** and type:
    ```bash
   ip a
   ```
   Then type:
   ```bash
   ssh pi@IP_ADDRESS
   ```
   Replace `IP_ADDRESS` with the actual IP address of the Raspberry Pi that we found earlier.

---

### **Step 7: Install Essential Software**
Here are some common software tools you might want to install on your Raspberry Pi:

#### **Install Git**
```bash
sudo apt install git
```

#### **Install Python 3 and Pip**
```bash
sudo apt install python3 python3-pip
```

#### **Install OpenSSH**
```bash
sudo apt install openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh
```

---

### **Step 8: Expand the File System (if necessary)**
If you are using a new SD card, you might want to expand the file system to utilize the full space.

1. **Open raspi-config**:
   ```bash
   sudo raspi-config
   ```
2. **Select Advanced Options > Expand Filesystem**.
3. **Reboot** for changes to take effect:
   ```bash
   sudo reboot
   ```

---

### **Step 9: Install Additional Software (Optional)**

#### **MariaDB (Database Server)**
1. **Install MariaDB**:
   ```bash
   sudo apt install mariadb-server
   sudo systemctl start mariadb
   sudo systemctl enable mariadb
   ```
2. **Secure MariaDB**:
   ```bash
   sudo mysql_secure_installation
   ```

#### **Install a Web Server (Apache)**
1. **Install Apache**:
   ```bash
   sudo apt install apache2
   ```
2. **Enable and start Apache**:
   ```bash
   sudo systemctl enable apache2
   sudo systemctl start apache2
   ```

#### **Install PHP**
1. **Install PHP**:
   ```bash
   sudo apt install php libapache2-mod-php
   ```

---

### **Step 10: Set Up Automatic Backups (Optional)**
1. **Install rsync** for automatic backups:
   ```bash
   sudo apt install rsync
   ```
2. **Set up cron jobs** to automate backups:
   ```bash
   crontab -e
   ```

---

### **Step 11: Access Your Raspberry Pi Remotely**
Once you have SSH enabled, you can easily connect to your Raspberry Pi from any computer on the same network.

1. **From a Linux/macOS machine**:
   ```bash
   ssh pi@IP_ADDRESS
   ```
2. **From a Windows machine**:
   - Use [PuTTY](https://www.putty.org/) to SSH into your Raspberry Pi.

---

### **Step 12: Access MariaDB**
1. **Log into MariaDB** using the following command:
   ```bash
   sudo mariadb
   ```
   - This opens the MariaDB shell as the root user.


2. **Create a new database**:
   ```sql
   CREATE DATABASE your_database_name;
   ```
   - Replace `your_database_name` with your desired database name.
   
3. **View the list of databases**:
   ```sql
   SHOW DATABASES;
   ```

4. **Create a new user** (replace `username` and `password`):
   ```sql
   CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
   ```

5. **Grant privileges to the new user** for your specific database:
   ```sql
   GRANT ALL PRIVILEGES ON your_database_name.* TO 'username'@'localhost';
   ```

6. **Apply the privilege changes**:
   ```sql
   FLUSH PRIVILEGES;
   ```

7. **Use a database** to work with it:
   ```sql
   USE your_database_name;
   ```

Tables are where data is stored. Each table contains rows (entries) and columns (attributes).

8. **Create a new table** (example for a `users` table):
   ```sql
   CREATE TABLE users (
      id INT AUTO_INCREMENT PRIMARY KEY,
      username VARCHAR(50),
      password VARCHAR(100),
      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

9. **View tables in the current database**:
   ```sql
   SHOW TABLES;
   ```

10. **Insert a record** into a table:
   ```sql
   INSERT INTO users (username, password) VALUES ('user1', 'password123');
   ```

11. **View the data** in a table:
   ```sql
   SELECT * FROM users;
   ```

12. **Update a record** in the table:
   ```sql
   UPDATE users SET password = 'newpassword' WHERE username = 'user1';
   ```

13. **Delete a record** from the table:
   ```sql
   DELETE FROM users WHERE username = 'user1';
   ```

---

## **Nice To Know Database Concepts**

### **Databases**
A **database** is an organized collection of structured data. Each database can contain multiple tables.

### **Tables**
A **table** is a collection of related data entries. It is made up of rows and columns:
- **Rows**: Each row represents a single record or entry.
- **Columns**: Each column represents an attribute or field of the record.

### **Primary Key**
The **primary key** is a column (or set of columns) that uniquely identifies each row in the table. In the `users` table, the `id` is the primary key.

### **SQL**
**SQL** (Structured Query Language) is the language used to manage and query databases. Commands like `CREATE`, `SELECT`, `INSERT`, and `DELETE` are SQL statements.

### **Data Types**
Each column in a table must have a **data type**, which defines the type of data stored in that column:
- **INT**: Integer (whole numbers).
- **VARCHAR(x)**: Variable-length string, where `x` is the maximum number of characters.
- **DATE/TIMESTAMP**: Date or date and time values.

### **Indexes**
An **index** helps speed up database queries. Indexes can be created on one or more columns in a table to make lookups faster.

### **Foreign Key**
A **foreign key** is a column that creates a relationship between two tables. It references the primary key of another table.

### **Backup and Restore**
- **Backup** a database:
   ```bash
   mysqldump -u root -p your_database_name > backup.sql
   ```
- **Restore** a database:
   ```bash
   mysql -u root -p your_database_name < backup.sql
   ```

---