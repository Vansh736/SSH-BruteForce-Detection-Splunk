# SSH Brute Force Detection using Splunk

## Objective
Simulate SSH brute force attack using Hydra and detect it using Splunk SIEM.

## Tools Used
- Kali Linux
- Ubuntu Server
- Splunk Enterprise
- Hydra
- UFW Firewall

## Attack Simulation
Hydra was used to perform brute force attack on SSH.

hydra -t 4 -V -f -l raj -P /tmp/passlist.txt ssh://10.42.232.156

## Detection in Splunk
Splunk query used to detect brute force attack:

index=auth "Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip

## Result
Attacker IP detected successfully and blocked using firewall.

## Prevention
sudo ufw deny from ATTACKER_IP to any port 22