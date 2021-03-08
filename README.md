
# 🔥 FirewallSetup 🔥

## Basic setup

This script sets up iptables rules with basic hardening techniques including ssh tarpitting.

1. Download the rules to `/etc`:
  `git clone https://github.com/Exosunandnet/fw-ng.git /etc/`
2. Depending on your iptables version you may need to change to an older version:
   
   A. Legacy version: 
	```
	update-alternatives --set iptables /usr/sbin/iptables-legacy
	update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
	```
    B. NFT version:
	  ```
	update-alternatives --set iptables /usr/sbin/iptables-nft
	update-alternatives --set ip6tables /usr/sbin/ip6tables-nft
	```

## Additional steps

#### Define on `~/.bashrc` or `~/.zshrc`:
``
function fwclear(){bash /etc/fw-ng/fwclear}
``
``
function fwreload(){bash /etc/fw-ng/fwreload}
``
####  Make the rules persistent
* Debian-based Distributions
	```
	sudo apt install iptables-persistent
	sudo /etc/init.d/netfilter-persistent save
	```
* Arch Linux Distributions
	 ```
	sudo iptables-save > /etc/iptables/iptables.rules
	```
	>Using `iptable-save` which come preinstalled in Arch
* RHEL / CentOS Distributions 
	```
	sudo chkconfig iptables on
	sudo service iptables save
	```
	> It is a service so it only needs to be run once
