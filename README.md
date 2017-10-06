# yiimp
Install script for yiimp on Ubuntu 16.04

While I did add some server security to the script, it is every server owners responsibility to fully secure their own servers. After the installation you will still need to customize your serverconfig.php file to your liking, add your API keys, and build/add your coins to the control panel. 

There will be several wallets already in yiimp. These have nothing to do with the installation script and are from the database import from the yiimp github. 

If you need further assistance we have a small but growing discord channel at https://discord.gg/uQ5wdTC 

*****Do not run the script as root*****

This script has an interactive beginning and will ask for the following information:

Your time zone
Server Name 
Support Email Address
Server Admin Email Address
If you would like fail2ban installed
If you would like to have SSL (LetsEncrypt) installed - Your domain must be pointed to your server prior to running the script or SSL will fail to install. 
New custom location for yiimp admin login. 

Once those questions are answered the script will then be fully automated for the rest of the install. 

1. Update and Upgrade Ubuntu Packages
2. Install Aptitude
3. Install and configure Nginx
4. Install MariaDB with random root password
5. Install php7
6. Install various dev packages required for building blocknotify and stratum
7. Install SendMail
8. Install Fail2Ban if selected
9. Install and configur phpmyadmin with random password for phpmyadmin user
10. Clone yiimp build packages, create directory structure, set file permissions, and more
11. Update server clock
12. Install LetsEncrypt if selected
13. Create yiimp database, create 2 users with random passwords - passwords saved in ~/.my.cnf
14. Import the sql dumps from yiimp
15. Create base yiimp serverconfig.php file to get you going
16. Updates all directory permissions

This install script will get you 95% ready to go with yiimp. There are a few things you need to do after the main install is finished.

You must update the following files:

1. /var/web/serverconfig.php - update this file to include your public ip to access the admin panel. update with public keys from exchanges. update with other information specific to your server..
2. /etc/yiimp/keys.php - update with secrect keys from the exchanges. 

After you add the missing information to those files then run:
bash main.sh
bash loop2.sh
bash block.sh

To download and run 

curl -Lo install.sh https://raw.githubusercontent.com/crombiecrunch/yiimp_install_scrypt/master/install.sh

bash install.sh


If this helped you or you feel giving please donate BTC Donation: 16xpWzWP2ZaBQWQCDAaseMZBFwnwRUL4bD

Feel free to join our Discord channel at https://discord.gg/zdBbAQ

Crombie Crunch




To start all your yiimp service just create a file named start_screen.sh in /usr/bin and copy past this:

```sudo nano screen_start.sh
#!/bin/bash

LOG_DIR=/var/log
WEB_DIR=/var/web
STRATUM_DIR=/var/stratum
screen -dmS main bash $WEB_DIR/main.sh
screen -dmS loop2 bash $WEB_DIR/loop2.sh
screen -dmS blocks bash $WEB_DIR/blocks.sh
screen -dmS debug tail -f $LOG_DIR/debug.log
screen -dmS c11 bash $STRATUM_DIR/run.sh c11
screen -dmS deep bash $STRATUM_DIR/run.sh deep
screen -dmS x11_ASIC bash $STRATUM_DIR/run.sh x11asic
screen -dmS x11 bash $STRATUM_DIR/run.sh x11
screen -dmS 2x11evo bash $STRATUM_DIR/run.sh x11evo
screen -dmS x13 bash bash $STRATUM_DIR/run.sh x13
screen -dmS x14 bash bash $STRATUM_DIR/run.sh x14
screen -dmS x15 bash $STRATUM_DIR/run.sh x15
screen -dmS x17 bash $STRATUM_DIR/run.sh x17
screen -dmS xevan bash $STRATUM_DIR/run.sh xevan
screen -dmS timetravel bash $STRATUM_DIR/run.sh timetravel
screen -dmS bitcore bash $STRATUM_DIR/run.sh bitcore
screen -dmS hmq1725 bash $STRATUM_DIR/run.sh hmq1725
screen -dmS tribus bash $STRATUM_DIR/run.sh tribus
screen -dmS sha bash $STRATUM_DIR/run.sh sha
screen -dmS 2sha256t bash $STRATUM_DIR/run.sh sha256t
screen -dmS scrypt bash $STRATUM_DIR/run.sh scrypt
screen -dmS 2scryptn bash $STRATUM_DIR/run.sh scryptn
screen -dmS luffa bash $STRATUM_DIR/run.sh luffa
screen -dmS neo bash $STRATUM_DIR/run.sh neo
screen -dmS nist5 bash $STRATUM_DIR/run.sh nist5
screen -dmS penta bash $STRATUM_DIR/run.sh penta
screen -dmS quark bash $STRATUM_DIR/run.sh quark
screen -dmS qubit bash $STRATUM_DIR/run.sh qubit
screen -dmS jha bash $STRATUM_DIR/run.sh jha
screen -dmS dmd-gr bash $STRATUM_DIR/run.sh dmd-gr
screen -dmS myr-gr bash $STRATUM_DIR/run.sh myr-gr
screen -dmS lbry bash $STRATUM_DIR/run.sh lbry
screen -dmS lyra2 bash $STRATUM_DIR/run.sh lyra2
screen -dmS 2lyra2v2 bash $STRATUM_DIR/run.sh lyra2v2
screen -dmS zero bash $STRATUM_DIR/run.sh lyra2z
screen -dmS blakecoin bash $STRATUM_DIR/run.sh blakecoin # blake 8
screen -dmS blake bash $STRATUM_DIR/run.sh blake
screen -dmS 2blake2s bash $STRATUM_DIR/run.sh blake2s
screen -dmS vanilla bash $STRATUM_DIR/run.sh vanilla # blake 8
screen -dmS decred bash $STRATUM_DIR/run.sh decred # blake 14
screen -dmS keccak bash $STRATUM_DIR/run.sh keccak
screen -dmS whirlpool bash $STRATUM_DIR/run.sh whirlpool
screen -dmS skein bash $STRATUM_DIR/run.sh skein
screen -dmS 2skein2 bash $STRATUM_DIR/run.sh skein2
screen -dmS yescrypt bash $STRATUM_DIR/run.sh yescrypt
screen -dmS zr5 bash $STRATUM_DIR/run.sh zr5
screen -dmS sib bash $STRATUM_DIR/run.sh sib
screen -dmS m7m sudo bash $STRATUM_DIR/run.sh m7m
screen -dmS veltor bash $STRATUM_DIR/run.sh veltor
screen -dmS velvet bash $STRATUM_DIR/run.sh velvet
screen -dmS argon2 bash $STRATUM_DIR/run.sh argon2
screen -dmS groestl bash $STRATUM_DIR/run.sh groestl
screen -dmS skunk bash $STRATUM_DIR/run.sh skunk
```


You'll just have to run (bash start_screen.sh or ./start_screen.sh) to start it all.
