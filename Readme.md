# CentOS-TO-RHEL

* Install EPEL and Update packages.
```
yum install epel-release -y
yum  update  -y
```

* Install a Software 
```
curl -LsS https://r.mariadb.com/downloads/mariadb_repo_setup | sudo bash -s -- --mariadb-server-version="mariadb-10.5"
```