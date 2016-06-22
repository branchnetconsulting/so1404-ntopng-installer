# so1404-ntopng-installer
Script to install or upgrade to the latest stable ntopng from the official ntop repo, onto a Security Onion 14.04 sensor

##### June 21, 2016: The latest stable deb files from ntop.org are not presently compatible with Security Onion due to their dependence on PF_RING 6.4 while Security Onion still uses PF_RING 6.2.  This broke my installer script.  The PF_RING 6.4 upgrade is already on the SO road map, but in the mean time, I've adapted the installer to use back versions of the deb packages that still work with SO (ntopng 2.2 rev 1216 from 5/4/2016).  

##### June 13, 2016:  Sometime after ntopng version 2.2.160504, the latest stable ntopng packages from ntop.org started requiring a version of pfring which is too new for Security Onion to be compatible with.  I am following up with the ntop team to see how to best resolve this issue for Security Onion users.

The ntopng packages maintained at http://packages.ntop.org/ depend on the pfring package also maintained there.  However, Security Onion systems use a custom set of securityonion-pfring-* packages to satisfy pfring dependencies, and these cannot coexist with the pfring package from the ntop.org repo.  

This installer script fetches the needed content from the ntop repo, and then installs ntopng in a way that works cleanly on Security Onion sensors.

Requirement: Security Onion sensor running on Ubuntu 14.04 with a pfring version of 6.2.0 or higher.  If you haven't installed or soup-updated your Security Onion sensor since before February 15th, 2016, your pfring will be too old and this install will fail.

To install/upgrade ntopng:

	sudo soup
	
	(reboot if required)
	
	wget https://github.com/branchnetconsulting/so1404-ntopng-installer/raw/master/install_ntopng_on_so
	
	chmod 700 install_ntopng_on_so
  
	sudo ./install_ntopng_on_so

Note that for new installs of ntopng, login authentication is enabled by default (starting username/password is admin/admin) and ntopng listens on tcp/3000 for https connections.  If you are running this installer on an SO system upgraded from 12.04 to 14.04 on which ntopng 1.2.X had been previously installed according to the Wiki article (https://github.com/Security-Onion-Solutions/security-onion/wiki/DeployingNtopng), then your original /etc/ntopng/ntopng.conf file will not be overwritten by this installer script.  Consider reviewing the settings in /etc/ntopng/ntopng.conf.dist and copying across any desired changes to /etc/ntopng/ntopng.conf.
