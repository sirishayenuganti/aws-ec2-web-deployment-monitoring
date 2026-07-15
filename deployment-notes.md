# Deployment & Monitoring SOP - Nginx Web Server on AWS EC2

## Setup Steps
1. Launched Ubuntu EC2 instance (t2.micro, free tier)
2. Configured Security Group: allowed SSH (22) from My IP, HTTP (80) from Anywhere
3. Connected via EC2 Instance Connect
4. Installed Nginx: sudo apt update && sudo apt install nginx -y
5. Verified service: sudo systemctl status nginx

## Monitoring
- CloudWatch alarm "high-cpu-alert" set at CPUUtilization > 70%

## Troubleshooting: Site Unreachable
1. Check service status: sudo systemctl status nginx
2. If inactive, restart: sudo systemctl start nginx
3. If still unreachable, check Security Group inbound rules for port 80
4. Verify public IP hasn't changed (restarts can change it unless Elastic IP is used)

## Common Issue Encountered
- Initial "Connection refused" error was caused by missing HTTP (port 80) inbound rule
- Fixed by adding HTTP rule with source 0.0.0.0/0 in Security Group
