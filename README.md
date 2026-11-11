# AWS Application Load Balancer – High Availability Project

## Project Overview
This project demonstrates how to configure an AWS Application Load Balancer (ALB) to distribute incoming HTTP traffic across two Amazon EC2 web servers.

Both EC2 instances run Amazon Linux 2023 with Apache HTTP Server installed. The ALB uses a target group with health checks to monitor the availability of the registered instances.

A failure test was performed by stopping Apache on one server. The target group detected the unhealthy instance while the other server remained healthy. After restarting Apache, the target returned to a healthy state.

## Architecture

```text
                 Internet
                    |
                    v
       Application Load Balancer
               (HTTP : 80)
                    |
                    v
             Target Group
                    |
             +------+------+
             |             |
             v             v
       ALB-Server-1   ALB-Server-2
         Apache          Apache
          Port 80        Port 80
```

## AWS Services and Technologies Used

- Amazon EC2
- Application Load Balancer (ALB)
- Target Groups
- Health Checks
- Amazon VPC
- Public Subnets
- Internet Gateway
- Security Groups
- Amazon Linux 2023
- Apache HTTP Server
- AWS Management Console

## Project Implementation

1. Created two EC2 instances using Amazon Linux 2023.
2. Installed Apache HTTP Server on both instances.
3. Started and enabled the Apache service.
4. Created a target group named `ALB-Target-Group`.
5. Registered both EC2 instances with the target group on HTTP port 80.
6. Created an internet-facing Application Load Balancer named `ALB-Project`.
7. Configured the listener to forward HTTP traffic to the target group.
8. Verified target health using health checks.

## Testing and Validation

### Test 1 – Both Servers Healthy
Verified that both registered EC2 instances showed Healthy status in the target group.

### Test 2 – Server Failure
Stopped the Apache service on ALB-Server-1 using:

```bash
sudo systemctl stop httpd
```

The target group health check detected Server 1 as Unhealthy, while Server 2 remained Healthy.

### Test 3 – Server Recovery
Restarted Apache on Server 1:

```bash
sudo systemctl start httpd
sudo systemctl status httpd
```

After the health check recovered, both registered targets showed Healthy status again.

## Repository Structure

```text
AWS-Application-Load-Balancer-Project/
│
├── AWS_ALB_High_Availability_Project_Documentation_With_Screenshots.docx
├── AWS_ALB_High_Availability_Project_Documentation_With_Screenshots.pdf
├── screenshots/
└── README.md
```

## Key Learning Outcomes

- Understanding Application Load Balancer configuration.
- Registering EC2 instances with a target group.
- Configuring and monitoring health checks.
- Understanding Healthy and Unhealthy target states.
- Performing application failure and recovery testing.
- Managing Apache HTTP Server on Amazon Linux.

## Project Documentation

- [Download Word Documentation](AWS_ALB_High_Availability_Project_Documentation_With_Screenshots.docx)
- [View PDF Documentation](AWS_ALB_High_Availability_Project_Documentation_With_Screenshots.pdf)

## Project Scope

This project focuses on Application Load Balancer configuration, EC2 web servers, target group health checks, and failure-recovery testing. Auto Scaling is not included in this project.

---

**Author:** Deepika Vijayakumar  
**GitHub:** https://github.com/deepikacloud-learner
