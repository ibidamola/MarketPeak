# MarketPeak

# Capstone Project: E-Commerce Platform Deployment with Git, Linux, and AWS

## Table of Contents

- [E-commerce Platform Deployment with Git, Linux, and AWS](#platform deployment-with-git)
  - [Git Version Control Setup](#Git-version-control-setup)
    - [1. Implement Version Control With Git](#Implement-Version-Control-with-Git)
    - [1.1 Initialize Git Repository](#11-initialize-git-repository)
    - [1.2 Obtain and Prepare the E-Commerce Website Template](#12-obtain-and-prepare-the-e-commerce-website-template)
    - [1.3 Stage and Commit the Template to Git](#13-stage-and-commit-the-template-to-git)
    - [1.4 Push the Code to Your GitHub Repository](#14-push-the-code-to-your-github-repository)
  - [AWS Deployment](#AWS-deployment)
    - [2.1 Set Up an AWS EC2 Instance](#21-set-up-an-aws-ec2-instance)
    - [2.2 Clone the Repository on the Linux Server](#22-clone-the-repository-on-the-linux-server)
    - [2.3 Install a Web Server on EC2](#23-install-a-web-server-on-ec2)
    - [2.4 Configure httpd for Website](#24-configure-httpd-for-website)
    - [2.5 Access Website from Browser](#25-access-website-from-browser)
  - [Continuous Integration and Deplayment Workflow](#3-continuous-integration-and-deployment-workflow)
    - [1 Developing New Features and Fixes](#step-1-developing-new-features-and-fixes)
    - [2 Version Control with GitHub](#step-2-version-control-with-git)
    - [3 Pull Requests and Merging to the Main Branch](#step-3-pull-requests-and-merging-to-the-main-branch)
    - [4 Deploying Updates to the Production Server](#step-4-deploying-updates-to-the-production-server)
    - [5 Testing the New Changes](#step-5-testing-the-new-changes)
  - [Challenges and Troubleshooting](#challenges-and-troubleshooting)
  - [Conclusion](#conclusions)

## Scenario

You have been assigned to develop an e-commerce website for a new online marketplace named "MarketPeak." This platform will feature product listings, a shopping cart, and user authentication. Your objective is to utilize Git for version control, develop the platform in a Linux environment, and deploy it on an AWS EC2 instance.

## Tasks

### 1. Implement Version Control with Git

#### 1.1 Initialize Git Repository

Begin by creating a project directory named "MarketPeak_Ecommerce". Inside this directory, initialize a Git repository to manage your version control.

```bash
mkdir MarketPeak_Ecommerce
cd MarketPeak_Ecommerce
git init
```

![Git Initialization](<images/git init.png>)

#### Explanation:

I started by creating a new directory named "MarketPeak_Ecommerce" to organize all the project files. Then, I initialized a Git repository within this directory to enable version control, which helps in tracking changes and collaborating with others.

#### 1.2. Obtain and Prepare the E-Commerce Website Template

Instead of developing the website from scratch, you'll use a pre-existing e-commerce website template. This approach allows you to focus on the deployment and operational aspects, rather than on web development. The actual web development is done by web/software developers on the project.

Download a suitable e-commerce website template from Tooplate or any other free template resource. Extract the downloaded template into your project directory, MarketPeak_Ecommerce.

#### Explanation:

I downloaded a coffee shop e-commerce website template from Tooplate because it had all the features needed for the project. I then extracted the downloaded template into the "MarketPeak" directory to prepare it for customization and deployment.


#### 1.3. Stage and Commit the Template to Git

Add your website files to the Git repository. Set your Git global configuration with your username and email. Commit your changes with a clear, descriptive message.

```bash
git add .
git config --global user.name "YourUsername"
git config --global user.email "youremail@example.com"
git commit -m "Initial commit with basic e-commerce site structure"
```



#### Explanation:

I added all the website files to the Git repository using `git add .`. Then, I configured Git with my username and email to ensure proper tracking of changes. Finally, I committed the changes with a clear message to document the initial setup of the e-commerce site.

#### 1.4. Push the Code to Your GitHub Repository

Create a remote repository on GitHub named "MarketPeak_Ecommerce". Link your local repository to GitHub and push your code.

```bash
git remote add origin https://github.com/your-git-username/MarketPeak_Ecommerce.git
git push -u origin main
```

![Git Push](images/git%20remote%20add%20origin.png)

#### Explanation:

I created a remote repository on GitHub and linked it to my local repository using the `git remote add origin` command. Then, I pushed the local commits to the remote repository on GitHub using `git push -u origin main`, enabling version control and collaboration.

### 2. AWS Deployment

#### 2.1. Set Up an AWS EC2 Instance

Log in to the AWS Management Console. Launch an EC2 instance using an Amazon Linux AMI. Connect to the instance using SSH.

#### Explanation:

I logged into the AWS Management Console and launched a new EC2 instance using the Amazon Linux AMI. This instance serves as the server where the e-commerce platform will be deployed. I connected to the instance using SSH to perform further configurations.

#### 2.2. Clone the Repository on the Linux Server

Clone the GitHub repository to your AWS EC2 instance using SSH or HTTPS.

```bash
# SSH Method
git clone git@github.com:yourusername/MarketPeak_Ecommerce.git

# HTTPS Method
git clone https://github.com/yourusername/MarketPeak_Ecommerce.git
```

![ssh keygen](<images/ssh keygen.png>)

#### Explanation:

I cloned the GitHub repository to the EC2 instance using the SSH method. This step ensures that the latest version of the e-commerce platform is available on the server for deployment.

### 2.3. Install a Web Server on EC2

Install Apache web server on the EC2 instance.

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

![Install Apache](<images/install apache.png>)

#### Explanation:

I installed the Apache web server on the EC2 instance using the `yum` package manager. This involved updating the package list, installing Apache (`httpd`), starting the web server, and enabling it to start automatically on server boot.

### 2.4. Configure httpd for Website

Clear the default httpd web directory and copy MarketPeak Ecommerce website files to it.

```bash
sudo rm -rf /var/www/html/*
sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/
```

Reload the httpd service to apply the changes.

```bash
sudo systemctl reload httpd
```

![Configure httpd](<images/sudo rm-rf.png>)
![reload httpd](<images/sudo system reload.png>)

#### Explanation:

I cleared the default web directory (`/var/www/html/`) and copied the e-commerce website files to this directory. Then, I reloaded the Apache service to apply the changes, making the website accessible through the server.

### 2.5. Access Website from Browser

Open a web browser and access the public IP of your EC2 instance to view the deployed website.

#### Explanation:

I accessed the public IP address of the EC2 instance in a web browser to verify that the e-commerce platform was successfully deployed and accessible online.

![ip address website deployed](<images/ip address hosted.png>)
### 3. Continuous Integration and Deployment Workflow

#### Step 1: Developing New Features and Fixes

Create a development branch and implement changes.

```bash
git branch development
git checkout development
```

#### Explanation:

I created a new branch named "development" to isolate new features and bug fixes from the stable version of the website. This ensures that the main branch remains stable while development work is ongoing.

![branch creation](<images/git branch.png>)

#### Step 2: Version Control with Git

Stage and commit your changes.

```bash
touch info.html
git add .
git commit -m "Added new feature html page 'info' "
git push origin development
```
To edit the new file in my EC2 Intance i used:

```bash
vim info.html
```
#### Explanation:

I created a new featatre called info page,  staged the changes using `git add .` and committed them with a descriptive message. Then, I pushed the development branch to GitHub to enable collaboration and version tracking.

![Cloning Repository](<Images/Cloning Repository.png>)

#### Step 3: Pull Requests and Merging to the Main Branch

Create a pull request on GitHub to merge the development branch into the main branch. Review and merge the PR.

```bash
git checkout main
git merge development
git push origin main
```

#### Explanation:

I created a pull request on GitHub to merge the development branch into the main branch. After reviewing the changes, I merged the pull request and pushed the updated main branch to GitHub.

![pull merge main branch](<Images/pull merge.png>)

#### Step 4: Deploying Updates to the Production Server

Pull the latest changes on the server and restart the web server if necessary.

```bash
git pull origin main
sudo systemctl reload httpd
```

#### Explanation:

I pulled the latest changes from the main branch on the EC2 instance and reloaded the Apache service to apply the updates. This ensures that the production server is always running the latest version of the website.



#### Step 5: Testing the New Changes

Access the website and test the new features or fixes.

#### Explanation:

I accessed the website through the public IP address of the EC2 instance to test the new features or fixes in the live environment. This step ensures that the updates work as expected.

![Updated Website](<images/updated deployment.png>)

### 7. Capstone Submission

#### 7.1. Document Your Process

Provide a detailed README.md file documenting the steps you took to deploy the entire flow. Include any troubleshooting or challenges you faced and how you overcame them.

#### Explanation:

I documented the entire deployment process in a README.md file, including any troubleshooting steps and challenges faced. This documentation serves as a guide for others who may work on the project in the future.

### Challenges and Troubleshooting

Throughout this process, I encountered several challenges and addressed them as follows:

**Challenge**: Difficulty in configuring the Apache server.

    Solution: I researched and found that the issue was related to incorrect directory permissions. I used chmod to set the correct permissions and reloaded the Apache service.
**Challenge**: SSH connection timeouts while accessing the EC2 instance.

    Solution: I ensured that my security group settings in AWS were correctly configured to allow inbound SSH traffic.
**Challenge**: Git push to GitHub failed due to authentication issues.
git 
    Solution: I switched to using SSH instead of HTTPS for GitHub authentication, generating a new SSH key and adding it to my GitHub account.

#### Conclusions:

I shared the Git repository with the mentor by providing access to the remote repository on GitHub. This allows the mentor to review the project and provide feedback.

```

```
