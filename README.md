# Ubuntu-Permission-Manager

# Step 1: Create a New User

You can create a new user using the adduser command.

```
sudo adduser <username>
```

Replace <username> with the desired username for the new user. Follow the prompts to set a password and other details.

# Step 2: Restrict Write Permissions

To ensure the user cannot write to any directories except their own, you can modify the user's permissions and set the filesystem to read-only for that user.

* create file `setup_readonly_user.sh`
* `chmod +x setup_readonly_user.sh`
* `./setup_readonly_user.sh`

```
#!/bin/bash

# Variables
USERNAME="<username>"
GROUP="readonlygroup"
APPLICATION="/usr/bin/firefox"
CONFIG_DIR="/home/$USERNAME/.mozilla"

# Create a New User
sudo adduser $USERNAME

# Create a Read-Only Group
sudo groupadd $GROUP

# Add the New User to the Read-Only Group
sudo usermod -aG $GROUP $USERNAME

# Create Necessary Directories
sudo mkdir -p /home/$USERNAME/Desktop

# Set Permissions for the Desktop Directory
sudo chown -R root:$GROUP /home/$USERNAME/Desktop
sudo chmod -R 755 /home/$USERNAME/Desktop

# Set More Permissive Permissions for the Home Directory
sudo chown -R $USERNAME:$USERNAME /home/$USERNAME
sudo chmod 755 /home/$USERNAME

# Optionally restrict other directories
# sudo chown -R root:$GROUP /home/$USERNAME/SpecificDirectory
# sudo chmod -R 755 /home/$USERNAME/SpecificDirectory

# Ensure the application binary is executable
sudo chmod +x $APPLICATION

# Set ownership and permissions on the application configuration directory
sudo mkdir -p $CONFIG_DIR
sudo chown -R $USERNAME:$USERNAME $CONFIG_DIR
sudo chmod -R 755 $CONFIG_DIR

# Verify Permissions
ls -l /home/$USERNAME
ls -l /home/$USERNAME/Desktop
ls -l $APPLICATION
ls -l $CONFIG_DIR
```
