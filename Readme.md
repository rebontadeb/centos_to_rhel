# CentOS-TO-RHEL

* Install EPEL and Update packages.
```
yum install epel-release -y
yum  update  -y
```

* Install a Software . Example :- MariaDB
```
curl -LsS https://r.mariadb.com/downloads/mariadb_repo_setup | sudo bash -s -- --mariadb-server-version="mariadb-10.5"
yum install MariaDB-server-10.5.24 -y 
systemctl start mysqld
systemctl enable mysqld
```
* If Required install latest kernel
```
yum install kernel-3.10.0-1160.114.2.el7 -y
```
* Create Database to check Data integrity
```
CREATE DATABASE CENTOSTORHEL;
```
* Add Repo and GPG-Key
```
curl -o /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release https://www.redhat.com/security/data/fd431d51.txt
curl --create-dirs -o /etc/rhsm/ca/redhat-uep.pem https://ftp.redhat.com/redhat/convert2rhel/redhat-uep.pem
curl -o /etc/yum.repos.d/convert2rhel.repo https://ftp.redhat.com/redhat/convert2rhel/7/convert2rhel.repo
```
* Add repo for Convert-to-rhel
```
yum repoinfo convert2rhel-for-rhel-7-rpms
yum install -y convert2rhel
convert2rhel --auto-attach --username=username --password='password'
```
 ** The Above Steps Will convert CentOS to RHEL **
# RHEL-TO-RHEL Leapp Upgrade
* Once converted to RHEL Update Subscription Status.
```
subscription-manager status
subscription-manager list --installed
subscription-manager repos --enable rhel-7-server-rpms
subscription-manager repos --enable rhel-7-server-extras-rpms
```
* Update Packages
```
yum update -y
```
* Make sure Database is running and having data intact.
```
show databases;
```
* Add Target Mariadb REPO
```
curl -LsS https://r.mariadb.com/downloads/mariadb_repo_setup | sudo bash -s -- --mariadb-server-version="mariadb-10.5" --os-type="rhel" --os-version="8.9"
```
* Move the repo content to leapp utility.
```
cat /etc/yum.repos.d/mariadb.repo >> /etc/leapp/files/leapp_upgrade_repositories.repo
```
* Install Leapp Upgrade Utility
```
yum install leapp-upgrade -y
```
* If required execute below command
```
leapp answer --section remove_pam_pkcs11_module_check.confirm=True
```
* Run Leapp Pre-Upgrade [ Check the Repo Name according to the environment ]
```
leapp preupgrade --target 8.9 --enablerepo mariadb-el8-main --enablerepo mariadb-el8-maxscale --enablerepo mariadb-el8-tools
```
* Run Leapp Upgrade [ Check the Repo Name according to the environment ]
```
leapp upgrade --target 8.9 --enablerepo mariadb-el8-main --enablerepo mariadb-el8-maxscale --enablerepo mariadb-el8-tools
```
* After Upgrade Make sure Database is running and having data intact.
```
show databases;
```
