# Ubuntu-Permission-Manager

# Step 1: Create a New User

You can create a new user using the adduser command.

```
sudo adduser <username>
```

Replace <username> with the desired username for the new user. Follow the prompts to set a password and other details.

# Step 2: Restrict Write Permissions

To ensure the user cannot write to any directories except their own, you can modify the user's permissions and set the filesystem to read-only for that user.

2.1. Change Ownership of Home Directory
Change the ownership of the home directory to root so the user can't write to their home directory.

```
sudo chown root:root /home/<username>
sudo chmod 755 /home/<username>
```

# 2.2. Create a Read-Only Group

Create a new group and add the user to this group. This group will have read-only permissions on the system.

```
sudo groupadd readonly
sudo usermod -aG readonly <username>
```

# 2.3. Set Permissions on Key Directories

Set the appropriate permissions for the new group on key directories.

```
sudo chown root:readonly /usr /bin /etc /lib /sbin /var /opt
sudo chmod 755 /usr /bin /etc /lib /sbin /var /opt
```

# Step 3: Ensure Desktop Environment Functions


```
sudo chown root:root /home/<username>
sudo chmod 755 /home/<username>
```

# Step 4: Restrict Sudo Access

```
sudo deluser <username> sudo
```


