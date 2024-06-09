# Shell-Scripting 

Problem: You have multiple EC2 instances and want to automate the process of restarting a specific service (e.g., web server) on all of them.
Script Outline:

Bash

#!/bin/bash

# 1. Get list of EC2 instance IDs (modify based on your needs)
instance_ids=$(aws ec2 describe-instances | jq -r '.Reservations[].Instances[].InstanceId')

# 2. Loop through each instance ID
for instance_id in $instance_ids; do
  # 3. Connect to the instance (modify based on your SSH setup)
  ssh -i pem_key.pem ubuntu@$instance_id

  # 4. Restart the service (modify for your specific service)
  sudo systemctl restart apache2

  # 5. Disconnect from the instance
  exit
done

# 6. Script completes
echo "Service restarted on all EC2 instances."
