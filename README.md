# Installing Suricata IDS on Ubuntu 24.04.1

This guide provides step-by-step instructions for installing and configuring Suricata IDS on an Ubuntu system. The process has been tested with Suricata version 6.0.8 on Ubuntu 24.04.1.

---

## Step 1: Install Suricata

Add the Suricata stable repository to your system, update the package list, and install Suricata:

```bash
sudo add-apt-repository ppa:oisf/suricata-stable
sudo apt-get update
sudo apt-get install suricata -y




