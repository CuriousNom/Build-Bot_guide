# Custom ROM Building Environment Setup

This guide will walk you through setting up the necessary packages for building a Custom ROM. Make sure you follow each step carefully.

## Prerequisites

- Ubuntu or Debian-based Linux distribution.
- Internet connection.

## Installation Steps

Open a terminal and run the following command:
```bash
sudo su
add-apt-repository ppa:openjdk-r/ppa
apt-get update

# Install more packages.
apt install openssh-server screen python git openjdk-8-jdk android-tools-adb bc bison \
build-essential curl flex g++-multilib gcc-multilib gnupg gperf imagemagick lib32ncurses-dev \
lib32readline-dev lib32z1-dev  liblz4-tool libncurses5-dev libsdl1.2-dev libssl-dev \
libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc yasm zip zlib1g-dev \
libtinfo5 libncurses5

# Exit su mode.
exit

# Creating a bin folder.
mkdir ~/bin
PATH=~/bin:$PATH
cd ~/bin
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
git clone https://github.com/akhilnarang/scripts.git scripts
cd scripts
bash setup/android_build_env.sh
