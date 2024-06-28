# Installation and Setup

## First Steps

Before launching your Homestead environment, you must install Vagrant and VirtualBox.

-   [Install Vargrant](https://developer.hashicorp.com/vagrant/install).
-   [Install VirtualBox7.0.18](https://www.virtualbox.org/wiki/Downloads).

All of these software packages provide easy-to-use visual installers for all popular operating systems.

## Installing Homestead

You may install Homestead by cloning the Homestead repository onto your host machine. Consider cloning the repository into a Homestead folder within your "home" directory, as the Homestead virtual machine will serve as the host to all of your Laravel applications. Throughout this documentation, we will refer to this directory as your "Homestead directory":

```
git clone https://github.com/laravel/homestead.git Homestead
```

After cloning the Laravel Homestead repository, you should checkout the release branch. This branch always contains the latest stable release of Homestead:

```
cd Homestead
git checkout release
```

Next, execute the bash init.sh command from the Homestead directory to create the Homestead.yaml configuration file. The Homestead.yaml file is where you will configure all of the settings for your Homestead installation. This file will be placed in the Homestead directory:

```
# macOS / Linux...
bash init.sh

# Windows...
init.bat
```

# Configuring Homestead

```
---
ip: "192.168.56.101"
memory: 2048
cpus: 2
provider: virtualbox

authorize: ~/.ssh/id_rsa.pub

keys:
  - ~/.ssh/id_rsa

folders:
  - map: D:/Work/Contact/Vue/Laravel/Homestead/Code/hello-world
    to: /home/vagrant/code/hello
    # type: "smb"

  - map: D:/Work/Contact/Vue/Laravel/Homestead/Code/myapp
    to: /home/vagrant/code/app
    # type: "smb"
sites:
  - map: hello.com
    to: /home/vagrant/code/hello/public

  - map: app.com
    to: /home/vagrant/code/app/public
databases:
  - hello_db
  - app_db

mysql:
  user: root
  password: 123456789

features:
  - mariadb: false
  - postgresql: false
  - ohmyzsh: false
  - webdriver: false

services:
  - enabled:
      - "mysql"
#   - disabled:
#       - "postgresql@11-main"

# ports:
#   - send: 33060 # MySQL/MariaDB
#     to: 3306
#   - send: 4040
#     to: 4040
#   - send: 54320 # PostgreSQL
#     to: 5432
#   - send: 8025 # Mailpit
#     to: 8025
#   - send: 9600
#     to: 9600
#   - send: 27017
#     to: 27017
```

Please review (https://laravel.com/docs/11.x/homestead#configuring-homestead) for more details.

# Generate a New SSH Key (if necessary):

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

When prompted to "Enter file in which to save the key", you can press Enter to accept the default location (C:\Users\admin/.ssh/id_rsa):
Enter file in which to save the key (C:\Users\admin/.ssh/id_rsa): [Press Enter]
Complete the Key Generation Process:

You'll be prompted to enter a passphrase. You can choose to enter a passphrase for added security or press Enter twice to leave it empty:

# Project Installation

```
composer create-project --prefer-dist laravel/laravel hello-world

```

# Hostname Resolution

Homestead publishes hostnames using mDNS for automatic host resolution. If you set hostname: homestead in your Homestead.yaml file, the host will be available at homestead.local. macOS, iOS, and Linux desktop distributions include mDNS support by default. If you are using Windows, you must install Bonjour Print Services for Windows.

Using automatic hostnames works best for per project installations of Homestead. If you host multiple sites on a single Homestead instance, you may add the "domains" for your web sites to the hosts file on your machine. The hosts file will redirect requests for your Homestead sites into your Homestead virtual machine. On macOS and Linux, this file is located at /etc/hosts. On Windows, it is located at C:\Windows\System32\drivers\etc\hosts. The lines you add to this file will look like the following:

```
192.168.56.101 hello.com
192.168.56.101 app.com
```

# Connecting via SSH

```
vagrant up
vagrant ssh
cd code/hello
php artisan migrate
npm install vue
npm run dev
```

# Updating Homestead

```
vagrant destroy
vagrant reload --provision
```

# Check Folder Permissions

Ensure that the permissions for the shared folder are correct. You can do this by SSH'ing into the VM and checking the permissions:

```
vagrant ssh
cd /home/vagrant/code
ls -l
```

# Error ENOTSUP: operation not supported on socket

```
vagrant plugin install vagrant-vbguest
vagrant vbguest --do install
```
