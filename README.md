SET UP ABSOLUTE ORANGE WEBSITE FOR DEV:  
Install Vagrant  
Install Virtual Machine  
Install Ansible  

Add Group Vars for ansible

In terminal:  
$ cp [your path to vagrant]/group_vars/_all.yml  [your path to vagrant]/group_vars/all.yml

In terminal:  
$ cd [your path to vagrant]/vagrant/  
$ vagrant up  

When the vagrant machine is up and running:  
$ cd [your path to vagrant]/vagrant/  
$ vagrant ssh  
$ sudo su  
$ source ~/.bash_aliases [initialise .bash_alisaes for command shortcuts]  
$ cdw [alias cd /vagrant/www]  
$ npm install  
$ grunt build  

On host machine browser http://localhost:8888/ to view site

CREATE AN ABSOUTE ORANGE WEBSITE INSTANCE  
Add keys to ~/.bash_profile:  
export AWS_KEY=[key]  
export AWS_SECRET=[key]  
export AWS_KEYNAME=[key]  
export AWS_KEYPATH=[key]  

$ source ~/.bash_profile  
$ mkdir AOL-AWS  
$ cd AOL-AWS  
$ git clone https://github.com/absoluteorange/Vagrant-for-AOL.git  

Set up your machine (only needs to be done once):  
1.  Install vagrant plugin  
    $ vagrant plugin install vagrant-aws  
  
2.  Add dummy box  
    $ vagrant box add dummy https://github.com/mitchellh/vagrant-aws/raw/$ master/dummy.box  
  
3.  Create ansible config (long AWS host names)  
    $ cd ~/  
    $ vim .ansible.cfg  
      [ssh_connection]  
      control_path = /tmp/%%h-%%p-%%r  
      :w  
  
$ vagrant up --provider=aws  
  
UPDATE ABSOLUTE ORANGE ON AWS  
Add aol-aws.pem to ~/  
$ ssh -i "aol-aws.pem" ubuntu@[Amazon instance Public DNS]  
$ cd /vagrant/www  
$ sudo git pull  
$ sudo make install  
  
COMMITTING DATA FROM ABSOLUTE ORANGE AWS TO GIT REPO  
$ ssh -i "aol-aws.pem" ubuntu@[Amazon instance Public DNS]  
$ sudo su  
$ cd /vagrant/www/
$ mysqldump -u amyvarga -p0range amyvarga > database/prod/aol-prod.sql   
$ sudo git status  
$ sudo git add -A  
$ sudo git commit -m [message]  
$ sudo git push  
