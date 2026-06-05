# Project 1: EC2 Web Server

## 🎯 Objective

Launch and configure an Amazon EC2 instance to host a simple web server. This project demonstrates core EC2 concepts including instance types, security groups, elastic IPs, and basic Linux administration.

## 📚 Concepts Covered

- EC2 instance types and sizing
- Security Groups and inbound/outbound rules
- Key pairs and SSH access
- Elastic IPs
- Basic web server setup (Apache/Nginx)
- EC2 Instance Metadata Service

## 🛠️ Services Used

| Service | Purpose |
|---------|---------|
| **EC2** | Virtual compute instance |
| **Security Groups** | Network firewall rules |
| **Elastic IP** | Static public IP address |
| **Key Pairs** | SSH authentication |

## 💰 Cost Estimate

- **Instance Type**: t2.micro (Free Tier eligible)
- **Monthly Cost**: ~$0.01 (or FREE with AWS Free Tier)
- **Data Transfer**: Free (within free tier)
- **Elastic IP**: Free (while associated with running instance)

**Total**: FREE with AWS Free Tier

## ⏱️ Duration

Estimated time: **30-45 minutes**

## 📋 Prerequisites

- AWS Account with free tier access
- AWS Management Console access
- SSH client (built-in on Mac/Linux, PuTTY on Windows)
- Basic Linux command knowledge

## 🚀 Setup Instructions

### Step 1: Launch an EC2 Instance

1. Go to [AWS Management Console](https://console.aws.amazon.com)
2. Navigate to **EC2 Dashboard**
3. Click **Launch Instances**
4. **Name**: `my-web-server`
5. **AMI**: Select "Amazon Linux 2 AMI" (Free Tier eligible)
6. **Instance Type**: `t2.micro` (Free Tier eligible)
7. **Key Pair**: 
   - Create new: `my-ec2-key`
   - Download and save securely
8. **Security Group**: Create new
   - Name: `web-server-sg`
   - Add inbound rules:
     - HTTP (80) from 0.0.0.0/0
     - HTTPS (443) from 0.0.0.0/0
     - SSH (22) from YOUR_IP_ADDRESS only
9. **Storage**: Default (8 GB)
10. Click **Launch Instance**

### Step 2: Connect via SSH

```bash
# Change permissions on key file
chmod 400 my-ec2-key.pem

# Connect to instance
ssh -i my-ec2-key.pem ec2-user@YOUR_INSTANCE_PUBLIC_IP
```

### Step 3: Install Web Server

```bash
# Update system
sudo yum update -y

# Install Apache Web Server
sudo yum install httpd -y

# Start Apache service
sudo systemctl start httpd

# Enable Apache to start on reboot
sudo systemctl enable httpd

# Create a simple HTML page
echo "<h1>Welcome to my AWS Web Server!</h1>" | sudo tee /var/www/html/index.html
```

### Step 4: Assign Elastic IP (Optional)

1. In EC2 Dashboard, click **Elastic IPs**
2. Click **Allocate Elastic IP**
3. Select your instance
4. Click **Associate**

### Step 5: Test Web Server

Open browser and navigate to:
```
http://YOUR_INSTANCE_PUBLIC_IP
```

## 📸 Screenshots

Document the following:
- [ ] EC2 Dashboard showing running instance
- [ ] Security Group rules
- [ ] SSH connection to instance
- [ ] Web browser showing running web server
- [ ] Instance details page

## 🏗️ Architecture

```
Internet
    |
    | (HTTP/HTTPS on port 80/443)
    |
Security Group (Firewall)
    |
EC2 Instance (t2.micro)
    |
Apache Web Server
    |
index.html
```

## 🧹 Cleanup Instructions

**IMPORTANT**: Delete resources to avoid charges

```bash
# Stop the instance
1. Go to EC2 Dashboard
2. Right-click instance → Instance State → Stop

# (Optional) Release Elastic IP
1. Go to Elastic IPs
2. Select your IP → Release Address

# Terminate instance (delete permanently)
1. Right-click instance → Instance State → Terminate
```

## 📊 Monitoring

Check instance metrics:
1. Go to EC2 Dashboard
2. Click your instance
3. View **Monitoring** tab
4. Check CPU utilization, network activity

## 🔐 Security Best Practices

✅ **Did you do these?**
- [ ] Restricted SSH access to your IP only
- [ ] Used strong security group rules (not 0.0.0.0/0 for SSH)
- [ ] Kept key pair secure
- [ ] Used IAM roles (future project)
- [ ] Enabled detailed monitoring
- [ ] Cleaned up resources after testing

## 💡 Key Learnings

Write down what you learned:
- What is an EC2 instance?
- How do Security Groups work?
- What is an Elastic IP?
- SSH vs RDP for access
- Basic Linux commands

## 🚀 Next Steps

1. Add HTTPS/SSL certificate (using Let's Encrypt)
2. Install WordPress or other CMS
3. Set up auto-scaling
4. Add load balancer
5. Connect to RDS database

## 📚 Resources

- [EC2 User Guide](https://docs.aws.amazon.com/ec2/)
- [Security Groups Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)
- [Elastic IPs Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)
- [AWS Free Tier](https://aws.amazon.com/free/)

## 📝 Notes

Add your own notes, challenges faced, and how you solved them:

---

**Status**: 📝 Planned  
**Completion Date**: TBD  
**Last Updated**: June 2026
