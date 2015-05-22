PHPVM
==================
Your next PHP stack using HHVM, Nginx, Mysql, Redis & Supervisord - build on top of Vagrant.


## You Will Have
A fresh setuped Ubuntu virtual machine, running:

    • Base Packages:
        Base Items (Curl, Git and more!)
    • Languages:
        PHP (php/hhvm)
    • Web Servers:
        HHVM
        Nginx
    • Databases Servers:
        MySQL
        PostgreSQL
    • In-Memory Stores:
        Redis
    • Utilities:
        Vim
        Composer (with PHPUnit)
        Supervisord

## Dependencies
    • Vagrant 1.5.0+
        Use vagrant -v to check your version
    • Vitualbox or VMWare Fusion


## Instructions
1. After installing Vagrant, you might need a virtual machine. I have used precise32, which can be downloaded first but running command: "vagrant box add precise32 http://files.vagrantup.com/precise32.box"
2. Clone/ copy this project in your application working copy.
3. Run command "vagrant up" from your faverout terminal.
4. In few mintes your machine will be ready and all project files will be synced.
5. Open browser and type: 192.168.22.10:4567 (your newly created host)


## Screenshots
![vagrant up](https://raw.github.com/waqar-alamgir/PHPVM/master/screenshots/vagrant-up.png)
![vagrant running](https://raw.github.com/waqar-alamgir/PHPVM/master/screenshots/vagrant-running.png)
![vagrant destroy](https://raw.github.com/waqar-alamgir/PHPVM/master/screenshots/vagrant-destroy.png)


## Developer Resources
Check out the URLs bellow to find out how its done:<br/>
[Vagrant Documentation](https://docs.vagrantup.com/)<br/>
[Checkout my tutorial to setup yii project on vagrant](http://waqaralamgir.wordpress.com/2014/09/30/setting-vagrant-with-yii-php/)<br/>


## The Vagrantfile
Its simple and easy to modify, meet your requirements by adding, removing and modifying shell scripts in /PHPVM/scripts/ directory.


## Interested in contributing?
If you wanna add more features and user options then just fork this repo from the link bellow:
https://github.com/waqar-alamgir/PHPVM/fork


## Credits
Shell scripts are compiled version, taken by googling.<br/><br/>
PHPVM by [Waqar Alamgir](http://waqaralamgir.tk)<br/>
[Web](http://waqaralamgir.tk)<br/>
[Twitter](http://www.twitter.com/wajrcs)
