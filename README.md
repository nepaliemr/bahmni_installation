### Features

- Prerequisite for the fresh installation of Bahmni
```
yum install -y https://kojipkgs.fedoraproject.org//packages/zlib/1.2.11/19.fc30/x86_64/zlib-1.2.11-19.fc30.x86_64.rpm
```
- Due to the non-availability of certain python distributions, the following steps needs to be executed to have a successful installation.
```
sudo yum install epel-release
```
```
sudo yum install python-pip
```
- Install the bahmni command line program (Choose the version you want)
```
yum install  https://repo.mybahmni.org/releases/bahmni-installer-0.92-155.noarch.rpm
```
- Confirm that the bahmni command is correctly installed (you should see a help message for the command)
```
bahmni –help
```
Note: if bahmni –help command doesn’t work there may be missing of package click and follow the following steps:
- Install Click Module
```
yum install wget
```
```
wget https://files.pythonhosted.org/packages/f8/5c/f60e9d8a1e77005f664b76ff8aeaee5bc05d0a91798afd7f53fc998dbc47/Click-7.0.tar.gz
``` 
```
tar -xvf Click-7.0.tar.gz (extract the file)
```
```
cd Click-7.0
```
```
python setup.py install
```
- Now setup a configuration file for bahmni command in /etc/bahmni-installer.
```
curl -L https://tinyurl.com/yyoj98df >> /etc/bahmni-installer/setup.yml
```
- Edit the setup.yml file and add the Bahmni Repo URL (for version 0.92 and earlier)
/etc/bahmni-installation/setup.yml (File Path)
```
bahmni_repo_url: https://repo.mybahmni.org/releases/
```
- Confirm the contents of the file. It should look like this file: (https://goo.gl/R8ekg5)
```
cat /etc/bahmni-installer/setup.yml
```
 The above setup.yml, has a timezone entry. You can change it to suit your timezone if you like. For valid options
please read this document: https://bahmni.atlassian.net/wiki/display/BAH/List+Of+Configurable+Installation+Variables
- Set the inventory file name to local in BAHMNI_INVENTORY environment variable. This way you won't need to use the '-i local' switch every time you use the 'bahmni' command
You can also configure custom inventory file instead of local.
```
echo "export BAHMNI_INVENTORY=local" >> ~/.bashrc
```
```
source ~/.bashrc
```
- Now fire the installer
For 0.92 or earlier
```
bahmni -aru https://repo.mybahmni.org/releases/ansible-2.4.6.0-1.el7.ans.noarch.rpm install
```
or for 0.93
```
bahmni  -I local install 
```
The installation should be done in about 15 - 30 minutes depending on your internet speed.
# Trouble shoot during Installation error:
- Postgres repo issue
https://talk.openmrs.org/t/installing-bahmni-0-92-failed-on-postgres-installation/27865/26?page=2
-  Postgres download package error during installation:
 Edit the below mention file:
/opt/bahmni-installer/bahmni-playbooks/group_vars/local 
```
postgrpostgres_repo_rpm_name:
postgres_repo_download_url:
```
Find the above mention line and replace with below line:
```
postgrpostgres_repo_rpm_name: pgdg-redhat-repo-latest.noarch.rpm
postgres_repo_download_url: https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
place the pgdg file inside /opt and re run the installation
- Install python-psycopg2 package if error during installation: 
```
yum install python-psycopg2
```
- Install the postgres package manually if error occur during installation:

	- (packages can be downloaded from the internet):
	- yum install  https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
	- a.	postgresql96-9.6.24-1PGDG.rhel7.x86_64.rpm
	- b.	postgresql96-contrib-9.6.24-1PGDG.rhel7.x86_64.rpm
	- c.	postgresql96-libs-9.6.24-1PGDG.rhel7.x86_64.rpm
	- d.	postgresql96-server-9.6.24-1PGDG.rhel7.x86_64.rpm
- Odoo service start error during installation and need to install following package manually:
Below command display the missing package on logs:
```
journalctl -xe
```
install required package using
```
wget https://raw.githubusercontent.com/odoo/odoo/10.0/requirements.txt
pip install -r requirements.txt
```
- Need to install to resolve the odoo UI display error after installation complete :
```
sudo npm install -g less@3.0.4 less-plugin-clean-css
```
- Verify installed components using the command:
```
yum list installed | grep bahmni
```
- Services:
```
service openmrs status/start/restart
service bahmni-lab status/start/restart
service odoo status/start/restart
service httpd status/start/stop/restart
service firewalld status/start/stop/restart
service bahmni-reports status/start/stop/restart
service bahmni-erp-connect status/start/stop/restart
service atomfeed-console status/start/stop/restart
service postgresql-9.6 status/start/stop/restart
service mysqld status/start/stop/restart
```
- Extra steps:
	- If error:
```
Yum install -y Bahmni-erp
```
And manually install the missing dependencies


