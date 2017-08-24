# Spin up RHEL 7.4 VM
# Install updates
yum -y update

# Install xauth-tools
yum -y install xorg-x11-xauth

Edit /etc/ssh/sshd_config to allow X11 forwarding (uncomment these lines in the file):
# X11Forwarding yes
# X11DisplayOffset 10
# X11UseLocalhost yes

systemctl restart sshd

# Install Firefox
yum install -y firefox

# Allow Firefox plugins to function with SELinux enabled (it is enabled by default in RHEL)
setsebool -P unconfined_mozilla_plugin_transition 0

# Installed epel repo (probably not actually needed):
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-10.noarch.rpm
rpm -ivh epel-release-7-10.noarch.rpm

# Install node.js 6.x repo:
curl --silent --location https://rpm.nodesource.com/setup_6.x | sudo bash -

Install node.js:
yum install -y nodejs

# Verify node.js version:
# node --version
# v6.11.2

npm install -g @sanity/cli

sanity init

# This utility walks you through creating a Sanity installation.
# Press ^C at any time to quit.

# Looks like you already have a Sanity-account. Sweet!

# ? Select project to use Create new project
# ? Informal name for your project Vega Dev
# ? Name of your first data set: dev
# ? Project description: Vega Development Testing
# ? Git repository URL: https://github.com/sanity-io/sanity.git
# ? Author: Steve Giessler
# ? License: UNLICENSED
# ? Output path: /root/vegadev
# ✔ Bootstrapping files from template
# ✔ Resolving latest module versions
# ✔ Fetching packages      ▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪ 100% (12.21s)
# ✔ Linking dependencies   ▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪ 100% (7.70s)
# ● Linking dependencies   ▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫ 0% (0.00s)
# ● Linking dependencies   ▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫▫ 0% (0.00s)
# ✔ Linking dependencies   ▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪▪ 100% (0.10s)
# ✔ Saved lockfile

# Success! You can now change to directory "/root/vegadev" and run "sanity start"

#  Note: If you want to import some sample data to your new project, run:

#  cd vegadev
#  sanity dataset import https://storage.googleapis.com/sanity/docsite-assets/moviedb.ndjson dev


# When prompted for login type chose Google since Github gave me a 500 error in browser window
# Had to CTRL-C and do this twice for reasons unknown before it authenticated.

sanity start
# webpack building...
# ✔ Checking configuration files...
# ⠧ Compiling...webpack built f8eddacaec020fba7ae7 in 13616ms
# ✔ Compiling...
# Compiled successfully! Server listening on http://localhost:3333

# Create ssh tunnel from my local iMac terminal to view locally on port 3333
# ssh -L 3333:localhost:3333 root@157.182.147.46

# Open a browser on my iMac and point to:
# localhost:3333
