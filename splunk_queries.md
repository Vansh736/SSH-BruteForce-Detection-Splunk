# Splunk Queries for SSH Brute Force Detection

## Detect Failed SSH Logins

index=auth "Failed password"

## Extract Attacker IP and Target User

index=auth "Failed password"
| rex "Failed password for (invalid user )?(?<user>\w+)"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| table _time src_ip user host

## Investigate Attack Timeline

index=auth "Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| table _time src_ip user host