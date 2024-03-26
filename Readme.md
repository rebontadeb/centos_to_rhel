# CentOS-TO-RHEL
---
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

