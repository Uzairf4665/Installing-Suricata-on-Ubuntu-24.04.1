# Installing Suricata IDS on Ubuntu 24.04.1

This guide provides step-by-step instructions for installing and configuring Suricata IDS on an Ubuntu system. The process has been tested with Suricata version 6.0.8 on Ubuntu 24.04.1.

---
## Step 1: Install Suricata

Add the Suricata stable repository to your system, update the package list, and install Suricata:

```bash
sudo add-apt-repository ppa:oisf/suricata-stable
sudo apt-get update
sudo apt-get install suricata -y
```

## Step 2: Add Emerging Threats Rules
Download and extract the latest Suricata rules from Emerging Threats:
```bash
cd /tmp/
curl -LO https://rules.emergingthreats.net/open/suricata-6.0.8/emerging.rules.tar.gz
sudo tar -xvzf emerging.rules.tar.gz
sudo mv rules/*.rules /etc/suricata/rules/
sudo chmod 640 /etc/suricata/rules/*.rules
```

## Step 3:  Configure Suricata
Modify the Suricata configuration file to define network settings and load rules. 
Open the configuration file:
```bash
sudo nano /etc/suricata/suricata.yaml
```
Make the following changes:
Set Network Variables:
```
HOME_NET: "<YOUR_UBUNTU_IP>"
EXTERNAL_NET: "any"
```
Specify Rule Path:
default-rule-path: /etc/suricata/rules
```
default-rule-path: /etc/suricata/rules
rule-files:
  - "*.rules"
```
Enable Statistics:
```
stats:
  enabled: yes

```
Configure Interface:
```
af-packet:
  - interface: eth0
```

Save and close the file.

# Step 4: Restart Suricata
Restart the Suricata service to apply the changes:
```
sudo systemctl restart suricata
```
## Conclusion
Suricata is now installed and configured on your Ubuntu machine. You can start monitoring network traffic and analyzing data using the configured ruleset. For further customization, refer to the Suricata documentation.



