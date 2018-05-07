---
layout: post
title:  "dnf command usages."
date:   2018-05-07 18:35:29 +0200
categories: linux administration
---

* List enabled repositories `sudo dnf repolist`
* List all repositories `sudo dnf repolist all`
* Installing a package `sudo dnf install package_name`
* Removing a package:
* 	-  `sudo dnf erase package_name`
* 	-  `sudo dnf remove package_name`
* Update a package `sudo dnf update package_name`
* Check for full system update `sudo dnf check-update`
* Upgrade all package system `sudo dnf upgrade`
* List all group package `sudo dnf grouplist`
* Installing group package `sudo dnf groupinstall "Development Tools"`
* Removing group package `sudo dnf groupremove "Development Tools"`
* Search for package `sudo dnf search net-tools`
* Download without install a package `sudo dnf download package_name`
* Show all available packages `sudo dnf list available | more`
* Show only installed packages `dnf list installed`
* Show all available and installed `dnf list`
* Enable repository for installation `sudo dnf install --enable-repo=epel mysql`
* Check which package provides a required function `sudo dnf provides crontabl`
* View package information `sudo dnf info package_name`
* Building a cache `sudo time dnf makecache`
* Clean cache `sudo dnf clean all`
* Check the transaction history
* 	- `sudo dnf history`
* 	- `sudo dnf history info 5`
* Removing orphan packages `sudo dnf autoremove`
* Synchronize all the packages to latest stable releases `sudo dnf distro-sync`
* Reinstall a package `sudo dnf reinstall package_name`
* Upgrade to a particular version `sudo dnf upgrade-to package_name-x.x.x-x.fc28`
* Get dnf commands `dnf help`

