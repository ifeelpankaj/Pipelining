# CI/CD Pipeline for Node.js Application using Jenkins, GitHub, AWS and Docker

Welcome to the comprehensive guide on creating a CI/CD pipeline for your Node.js application using Jenkins, GitHub, and Docker. This README provides detailed step-by-step instructions to ensure a seamless setup process.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Setting Up](#setting-up)
   1. [Creating an EC2 Instance](#creating-an-ec2-instance)
   2. [Installing Jenkins](#installing-jenkins)
   3. [Jenkins Setup](#jenkins-setup)
   4. [Generating SSH Keys](#generating-ssh-keys)
   5. [Integrating GitHub and Jenkins](#integrating-github-and-jenkins)
   6. [Automating Docker Build and Run](#automating-docker-build-and-run)
3. [Conclusion](#conclusion)

## Prerequisites

- AWS account for creating an EC2 instance.
- Basic familiarity with the command line interface.
- Basic familiarity with GitHub
- An GitHub account

## Setting Up

### Creating an EC2 Instance

1. Launch an EC2 instance using the AWS Management Console.

   ![Screenshot: Instance](./ScreenShot/creating_instance.png)
   
3. Add a key pair for secure SSH access during instance creation.

   ![Screenshot:Key Pair](./ScreenShot/keypair.png) 
  
5. Connect to the instance using SSH

 ![Screenshot:Key Pair](./ScreenShot/keypair.png) 
  

### Installing Jenkins

1. Update packages and install Java:

   ```bash
   sudo apt-get update
   sudo apt-get install openjdk-11-jdk

   ![Screenshot: Installing Java](./ScreenShot/install_java.png)

   - Because Jenkins is made up of Java, we need to install Java on our Ubuntu machine.
  
2. Set up the location for Jenkins installation:

   ```bash
   curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
   echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

3. Install Jenkins:

   ```bash
   sudo apt-get install jenkins
   sudo apt-get update
   ![Screenshot: Installed Jenkins](./ScreenShot/startjenkins.png)

### Jenkins Setup

1. Open the Jenkins port in your security group:

   - Go to your EC2 instance details in the AWS Management Console.
   - Under the "Security groups" section, click on the security group associated with your instance.
   - In the "Inbound rules" tab, add a custom TCP rule for port 8080.
      ![Screenshot: Inbound Rule](./ScreenShot/Security_port.png)

2. Access Jenkins in your browser:

   ```bash
   http://your-instance-ip:8080
      ![Screenshot: Access Jenkins](./ScreenShot/jenkinsScreen.png)

3. Retrieve the initial admin password:

   ```bash
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword

4. Install the suggested plugins and create an admin user.

   ![Screenshot: Plugins](./ScreenShot/InstallPluginsd.png)

5. Create a admin user for jenkins

 ![Screenshot: UserJenkins](./ScreenShot/Create an Admin User.png)
 
6. Start using Jenkins and configure any additional settings as needed.

   ![Screenshot: Welcome Screen](./ScreenShot/Welcome Jenkins Screen.png)

### Generating SSH Keys

1. Generate SSH keys on your EC2 instance:

   ```bash
   ssh-keygen
   cd .ssh
   ls
   cat id_rsa
   cat id_rsa.pub

   # After this, you will get a Public and Private Key.


## Integrating GitHub and Jenkins

1. Clone the [MERN Stack Project Code](https://github.com/ifeelpankaj/locker) repository from GitHub.

 ![Screenshot: Repo](Git Repo.png)
2. Go to your GitHub settings:

   - Click on your profile picture in the top right corner and select "Settings".
   - Navigate to "SSH and GPG keys" in the left sidebar.


3. Add a new SSH key:

   - Click on "New SSH key".
   - In your terminal, open the public key file (usually `~/.ssh/id_rsa.pub`) and copy its content (starts with `ssh-rsa`).
   - Paste the public key into the "Key" field.
   - Give your key a meaningful title and click "Add SSH key".
 ![Screenshot: Plugins](Ssh-Github.png)
4. Open your Jenkins dashboard:

   - Create a new "Freestyle project" by clicking "New Item" on the Jenkins homepage.
 ![Screenshot: Jenkins Project](Create a freestyle project.png)
5. Configure the project:

   - Add a project name and description.
   - Under the "Source Code Management" section, select "Git" and enter your GitHub repository URL.
![Screenshot: Jenkins Description](Create a freestyle project.png)
   - In the "Credentials" dropdown, click "Add" to add your private key. Paste the private key content generated earlier (beginning with `-----BEGIN OPENSSH PRIVATE KEY-----`).

   - Save your configuration.

6. Build the project:

   - Click "Build Now" on the project page.
   - Monitor the build's console output to check the location of your project on the server.

### Automating Docker Build and Run








 



