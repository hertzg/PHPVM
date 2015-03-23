# -*- mode: ruby -*-
# vi: set ft=ruby :

##
# Server Configuration
##

server_cpus           = "1"   # Cores
server_memory         = "384" # MB
server_swap           = "768" # Options: false | int (MB) - Guideline: Between one or two times the server_memory

# Set a local private network IP address.
# See http://en.wikipedia.org/wiki/Private_network for explanation
# You can use the following IP ranges:
#   10.0.0.1    - 10.255.255.254
#   172.16.0.1  - 172.31.255.254
#   192.168.0.1 - 192.168.255.254
server_ip             = "192.168.22.10"
server_port           = "4567"

# Server Timezone
# UTC        for Universal Coordinated Time
# EST        for Eastern Standard Time
# US/Central for American Central
# US/Eastern for American Eastern
server_timezone       = "UTC"

##
# Language Configuration
##
php_timezone          = "UTC"    # http://php.net/manual/en/timezones.php
php_version           = "5.6"    # Options: 5.5 | 5.6
# To install HHVM instead of PHP, set this to "true"
hhvm                  = "false"
# Composer Options
# List any global Composer packages that you want to install
composer_packages     = [  
  "phpunit/phpunit:4.0.*",
  # "codeception/codeception=*",
  # "phpspec/phpspec:2.0.*@dev",
  # "squizlabs/php_codesniffer:1.5.*",
]
# Default web server document root
public_folder         = "/vagrant"

##
# Database Configuration
##
# MySQL
mysql_root_password   = ""   # We'll assume user "root"
mysql_version         = "5.5"    # Options: 5.5 | 5.6
mysql_enable_remote   = "false"  # remote access enabled when true
# PgSQL
pgsql_root_password   = ""   # We'll assume user "root"

Vagrant.configure("2") do |config|

  config.vm.box = "precise32" # "ubuntu/trusty64" for Ubuntu 14.04 LTS
  config.vm.network :forwarded_port, host: server_port, guest: 80
  
  ##
  # Base Items
  ##
  # Provision Base Packages
  # Installs curl and git
  config.vm.provision "shell", path: "./scripts/base.sh", args: [server_timezone , server_swap]
  # Optimize base box
  config.vm.provision "shell", path: "./scripts/base_box_optimizations.sh", privileged: true

  ##
  # Language Provision
  ##
  # PHP
  config.vm.provision "shell", path: "./scripts/php.sh", args: [php_timezone, hhvm, php_version]

  ##
  # Web Servers
  ##
  # Nginx
  config.vm.provision "shell", path: "./scripts/nginx.sh", args: [server_ip, public_folder]

  ##
  # Database Servers
  ##
  # MySQL
  config.vm.provision "shell", path: "./scripts/mysql.sh", args: [mysql_root_password, mysql_version, mysql_enable_remote]
  # PostgreSQL
  config.vm.provision "shell", path: "./scripts/pgsql.sh", args: pgsql_root_password

  ##
  # In-Memory Stores
  ##
  # Redis (without journaling and persistence)
  config.vm.provision "shell", path: "./scripts/redis.sh"

  ##
  # Utility
  ##
  # Vim
  config.vm.provision "shell", path: "./scripts/vim.sh"
  # Composer
  config.vm.provision "shell", path: "./scripts/composer.sh", privileged: false, args: composer_packages.join(" ")
  # Supervisord
  config.vm.provision "shell", path: "./scripts/supervisord.sh"

  # VM settings
  # If using VirtualBox
  config.vm.provider :virtualbox do |vb|

    vb.name = "Vaprobash"

    # Set server cpus
    vb.customize ["modifyvm", :id, "--cpus", server_cpus]

    # Set server memory
    vb.customize ["modifyvm", :id, "--memory", server_memory]

    # Set the timesync threshold to 10 seconds, instead of the default 20 minutes.
    # If the clock gets more than 15 minutes out of sync (due to your laptop going
    # to sleep for instance, then some 3rd party services will reject requests.
    vb.customize ["guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000]

    # Prevent VMs running on Ubuntu to lose internet connection
    # vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    # vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]

  end

  # If using VMWare Fusion
  config.vm.provider "vmware_fusion" do |vb, override|
    override.vm.box_url = "http://files.vagrantup.com/precise64_vmware.box"

    # Set server memory
    vb.vmx["memsize"] = server_memory

  end

  # If using Vagrant-Cachier
  # http://fgrehm.viewdocs.io/vagrant-cachier
  if Vagrant.has_plugin?("vagrant-cachier")
    # Configure cached packages to be shared between instances of the same base box.
    # Usage docs: http://fgrehm.viewdocs.io/vagrant-cachier/usage
    config.cache.scope = :box

    config.cache.synced_folder_opts = {
        type: :nfs,
        mount_options: ['rw', 'vers=3', 'tcp', 'nolock']
    }
  end

  # Adding vagrant-digitalocean provider - https://github.com/smdahlen/vagrant-digitalocean
  # Needs to ensure that the vagrant plugin is installed
  config.vm.provider :digital_ocean do |provider, override|
    override.ssh.private_key_path = '~/.ssh/id_rsa'
    override.ssh.username = 'vagrant'
    override.vm.box = 'digital_ocean'
    override.vm.box_url = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    provider.token = 'YOUR TOKEN'
    provider.image = 'ubuntu-14-04-x64'
    provider.region = 'nyc2'
    provider.size = '512mb'
  end

end
