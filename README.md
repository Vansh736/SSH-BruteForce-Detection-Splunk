# SSH-BruteForce-Detection-Splunk
Detecting SSH brute-force attacks using Splunk by analyzing Linux auth.log and identifying attacker IP addresses.

This project demonstrates detection of SSH brute-force attacks using Splunk SIEM by analyzing Linux authentication logs.

## Tools Used
- Kali Linux (Attacker Machine)
- Ubuntu Server (Target System)
- Splunk Enterprise (SIEM)
- Hydra (Brute-force tool)

## Lab Setup
1. Kali Linux used to simulate brute-force attack using Hydra.
2. Ubuntu server configured with SSH service.
3. Linux auth.log forwarded to Splunk.
4. Splunk queries used to detect multiple failed login attempts.

## Attack Simulation

Hydra command used:

hydra -t 4 -V -f -l raj -P passlist.txt ssh://<TARGET_IP>

This generates multiple failed login attempts in:

/var/log/auth.log

## Detection in Splunk

Example SPL Query:

index=auth "Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
| sort -count

This identifies attacker IP performing brute-force attempts.

## Investigation

Using Splunk:

| Field | Meaning |
|------|--------|
src_ip | Attacker IP |
user | Target username |
host | Target system |

## Response

Attacker IP blocked using firewall:

sudo ufw deny from <attacker_ip> to any port 22

## Conclusion

This project demonstrates how SIEM tools like Splunk can detect brute-force attacks by analyzing authentication logs and identifying malicious login attempts.
