# Installing-Suricata-on-Ubuntu-24.04.1
Follow this guide to install and configure Suricata IDS on an Ubuntu system. The steps have been tested with Suricata version 6.0.8 and should work seamlessly on Ubuntu 24.04.1.


Step 1: Install Suricata
Begin by adding the Suricata stable repository to your system, updating your package lists, and installing Suricata.

bash
Copy code
sudo add-apt-repository ppa:oisf/suricata-stable
sudo apt-get update
sudo apt-get install suricata -y
Step 2: Add Emerging Threats Rules
Download the latest Suricata rules from Emerging Threats and place them in the appropriate directory.

bash
Copy code
cd /tmp/
curl -LO https://rules.emergingthreats.net/open/suricata-6.0.8/emerging.rules.tar.gz
sudo tar -xvzf emerging.rules.tar.gz
sudo mv rules/*.rules /etc/suricata/rules/
sudo chmod 640 /etc/suricata/rules/*.rules
Step 3: Configure Suricata
Modify the Suricata configuration file to define your network settings and load rules. Open the file:

bash
Copy code
sudo nano /etc/suricata/suricata.yaml
Update the following parameters in the configuration file:

Set the internal and external networks:

yaml
Copy code
HOME_NET: "<YOUR_UBUNTU_IP>"
EXTERNAL_NET: "any"
Define the rules directory and include all rule files:

yaml
Copy code
default-rule-path: /etc/suricata/rules
rule-files:
  - "*.rules"
Enable global statistics:

yaml
Copy code
stats:
  enabled: yes
Configure the interface for high-speed packet capture (replace eth0 with your active interface):

yaml
Copy code
af-packet:
  - interface: eth0
Save and close the file.

Step 4: Restart Suricata
Finally, restart the Suricata service to apply the new configuration.

bash
Copy code
sudo systemctl restart suricata
