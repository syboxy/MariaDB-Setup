To set up **MariaDB** on **Fedora Linux**, follow these steps:

### 1. **Install MariaDB Server and Client**

MariaDB is included in the official Fedora repositories, so you can install it using `dnf`.

Open a terminal and run the following commands:

- **Install MariaDB Server**:
  ```bash
  sudo dnf install mariadb-server
  ```

- **Install MariaDB Client (Optional, for connecting to MariaDB from the command line)**:
  ```bash
  sudo dnf install mariadb
  ```

### 2. **Start and Enable MariaDB Service**

Once the installation is complete, you need to start the MariaDB service and enable it to start on boot:

- **Start MariaDB**:
  ```bash
  sudo systemctl start mariadb
  ```

- **Enable MariaDB to start on boot**:
  ```bash
  sudo systemctl enable mariadb
  ```

### 3. **Secure the MariaDB Installation**

After starting MariaDB, you should run the `mysql_secure_installation` script to secure your installation. This script will help you set a root password, remove insecure default settings, and improve the security of your installation.

- Run the script:
  ```bash
  sudo mysql_secure_installation
  ```

You will be prompted to configure the following:

- **Set a root password**: Choose a strong password.
- **Remove anonymous users**: This is recommended for security.
- **Disallow root login remotely**: This is recommended to secure your root user.
- **Remove test databases**: This is recommended for security.
- **Reload privilege tables**: Confirm to reload the privilege tables.

### 4. **Log in to MariaDB**

Once the installation and security setup are complete, you can log in to the MariaDB shell as the root user:

```bash
sudo mysql -u root -p
```

You’ll be prompted to enter the root password you set earlier.

### 5. **Create a Database and User (Optional)**

If you want to create a database and a user for your projects, follow these steps:

1. **Create a database**:
   ```sql
   CREATE DATABASE mydatabase;
   ```

2. **Create a user**:
   ```sql
   CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';
   ```

3. **Grant privileges**:
   ```sql
   GRANT ALL PRIVILEGES ON mydatabase.* TO 'myuser'@'localhost';
   ```

4. **Flush privileges** to apply the changes:
   ```sql
   FLUSH PRIVILEGES;
   ```

Now, you can exit the MariaDB shell:

```sql
EXIT;
```

### 6. **Test Your Setup**

To test that everything is working, you can log in with the new user you created:

```bash
mysql -u myuser -p
```

Enter the password for `myuser` when prompted, and you should be able to access the `mydatabase` database.

### 7. **Configure MariaDB to Listen on All Interfaces (Optional)**

If you want MariaDB to accept remote connections, you'll need to change its configuration.

1. Open the MariaDB configuration file:
   ```bash
   sudo nano /etc/my.cnf.d/server.cnf
   ```

2. Find the line with `bind-address` and change it to:
   ```ini
   bind-address = 0.0.0.0
   ```

3. Restart MariaDB:
   ```bash
   sudo systemctl restart mariadb
   ```

4. Open the firewall to allow traffic on port 3306 (MariaDB default port):
   ```bash
   sudo firewall-cmd --permanent --zone=public --add-port=3306/tcp
   sudo firewall-cmd --reload
   ```

### Conclusion

Now you have **MariaDB** installed and running on your Fedora Linux system. You can use it for local development, and it is ready to be connected to your **.NET API** or any other applications.
