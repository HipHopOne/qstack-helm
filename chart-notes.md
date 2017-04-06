##Notes about the featured charts##

Some of the charts do not have or disable by default their UI.
This includes Ingress controllers, OpenVPN and some of the databases, for example.
Some apps just need a single parameter to work or a command line copy paste that might not be obvious.
In this doc we keep some helpful notes on those types of apps.

###Traefik and other ingress controllers ###

You can easily use Ingress controllers to supply virtual named hosts routing for multiple apps using a single Load balanced IP address and in some cases to automate Let's Encrypt certificate usage for https. Ingress controllers use DNS names but for testing purposes you can just add the host name to your computers "/etc/hosts" file and point to the Ingress controllers Loadbalanced IP address.

After deploying an Ingress controller you can use "Create Application" from the UI or "kubectl" to add an Ingress definition for your URL. The Ingress will automatically activate as soon as the Controller finds it.

Traefik is a great Ingress controller. By default the Traefik dashboard with statistics and live connection information is disabled but you can enable the dashboard in custom install options. Note that you like to use Traefik to front a WordPress app you need to set "gzip.enabled" to false because the default Wordpress app already enables compression.

###ChaosKube###

ChaosKube randomly kills Pods from other apps on a time interval to test resilience. By default it only logs which pods it would kill. To allow chaoskube to kill real Pods change the custom install option "dryRun" to false.

###Headless databases, key-value stores###

This applies to MongoDB, Postgresql, MySQL, Redis among others when deployed standalone.

Assuming you already downloaded the cluster config from the Qstack UI and have kubectl working. To log into the database after deployment go to the app's action menu (where is says "Running") and select "Show Info". Copy paste the kubectl access command and password (if needed) and execute in a terminal and you will be logged into the DB shell. In most cases you can also fetch the password under Configurations (Secrets) in the Qstack UI e.g. for Redis.

###GitLab CE###

Gitlab "requires" a DNS name to use for its frontend UI. In the custom install options set "externalUrl" to your desired domain name e.g. "http://your-domain.com".

For testing purposed you can set this to any domain name and use the Loadbalanced IP address of the main http (port 80) service to start using GitLab Community Edition.

###OpenVPN###

OpenVPN app is a great way to VPN into the k8s cluster and your Qstack instance's private network at the same time. This also allows you to lookup services by their internal kubernetes dns names. After the app is running go to the app's action menu (where is says "Running") and select "Show Info". Follow the copy-paste instructions to autocreate an .ovpn file that is double clickable and ready to use with a VPN client like TunnelBlick.app. Assumes "kubectl" is pointing to the right cluster. Connecting for the first time can take a few moments (you can watch the logs of the OpenVPN pod from the Qstack UI).





