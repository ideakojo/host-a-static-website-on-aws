


# Static Website Hosting on AWS

This project demonstrates how to host a static HTML web application on AWS using various AWS services to ensure high availability, scalability, and security.

## Project Architecture



### Resources Utilized
1. **Virtual Private Cloud (VPC)**: Configured with both public and private subnets across two availability zones for network isolation and reliability.
2. **Internet Gateway**: Facilitates connectivity between VPC instances and the Internet.
3. **Security Groups**: Acts as a virtual firewall to control inbound and outbound traffic.
4. **Availability Zones**: Leveraged two zones for enhanced system reliability and fault tolerance.
5. **Public Subnets**: Utilized for infrastructure components like the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect Endpoint**: Ensures secure connections to assets within both public and private subnets.
7. **Private Subnets**: Hosts web servers (EC2 instances) for enhanced security.
8. **NAT Gateway**: Enables instances in private subnets to access the Internet.
9. **EC2 Instances**: Hosts the website.
10. **Application Load Balancer (ALB)**: Evenly distributes web traffic to an Auto Scaling Group of EC2 instances across multiple Availability Zones.
11. **Auto Scaling Group (ASG)**: Automatically manages EC2 instances to ensure website availability, scalability, fault tolerance, and elasticity.
12. **GitHub**: Used for storing web files for version control and collaboration.
13. **AWS Certificate Manager**: Secures application communications.
14. **Simple Notification Service (SNS)**: Configured to alert about activities within the Auto Scaling Group.
15. **Route 53**: Registered the domain name and set up DNS records.

## Prerequisites

- AWS account with necessary permissions.
- Git installed on your local machine.
- Domain name registered (if using Route 53 for DNS).

## Deployment Steps

### Step 1: VPC Configuration
1. **Create a VPC**: Configure with public and private subnets across two availability zones.
2. **Set Up an Internet Gateway**: Attach it to the VPC.
3. **Create Security Groups**: Define inbound and outbound rules for your EC2 instances.

### Step 2: EC2 Instance Setup
1. **Launch EC2 Instances**: Place them in the private subnets for enhanced security.
2. **Create an EC2 Instance Connect Endpoint**: For secure access to your instances.

### Step 3: Install and Configure Apache on EC2
1. SSH into your EC2 instance.
2. Run the following script to install and configure Apache:

    ```bash
    #!/bin/bash
    sudo su
    yum update -y
    yum install -y httpd
    cd /var/www/html
    yum install git -y
    git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
    cp -R host-a-static-website-on-aws/. /var/www/html/
    rm -rf host-a-static-website-on-aws
    systemctl enable httpd
    systemctl start httpd
    ```

### Step 4: Configure Load Balancer and Auto Scaling
1. **Set Up an Application Load Balancer (ALB)**: To distribute incoming traffic.
2. **Create an Auto Scaling Group (ASG)**: Attach EC2 instances to the ASG.

### Step 5: Configure DNS
1. **Register a Domain Name**: Use AWS Route 53.
2. **Set Up DNS Records**: Point your domain to the ALB.

### Step 6: Secure Communications
1. **Request an SSL Certificate**: Use AWS Certificate Manager.
2. **Attach the Certificate**: To your ALB for HTTPS support.

## Testing and Validation
1. Access your website via the domain name.
2. Ensure that the load balancer and auto-scaling mechanisms work as expected.
3. Verify SSL/TLS encryption by checking the HTTPS connection.

## Repository Structure

- **/scripts**: Deployment and configuration scripts.
- **/docs**: Documentation and diagrams.

## Useful Links

- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)
- [AWS Load Balancer Documentation](https://docs.aws.amazon.com/elasticloadbalancing/)
- [GitHub Repository](https://github.com/aosnotes77/host-a-static-website-on-aws)

## Contributing

Feel free to submit issues or pull requests for any improvements or fixes.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

