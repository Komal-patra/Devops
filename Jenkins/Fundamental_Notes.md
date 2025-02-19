# Jenkins

## Overview

Jenkins is a **CI/CD tool** used for automating the build, test, and deployment process.

- **CI (Continuous Integration)**: Continuous build + continuous test
- **CD (Continuous Delivery)**: Deployment manually
- **CD (Continuous Deployment)**: Deployment automatically

### Key Features
- Free and open-source
- Platform-independent
- Built on Java 11
- Initially called **Hudson** (became paid, owned by Oracle, then made free)
- Plugin-rich ecosystem
- Default port number: **8080**

---

## Setting Up Jenkins on AWS EC2

### Security Group Settings
Ensure the following ports are allowed:
- **8080** (Jenkins)
- **80** (HTTP)

### Steps to Install Jenkins

#### Step 1: Install Git, Java 17, and Maven
```bash
yum install git java-17-amazon-corretto maven -y
```

#### Step 2: Add Jenkins Repository
```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
```

#### Step 3: Install Java 11 and Jenkins
```bash
sudo yum install java-17-amazon-corretto -y
yum install jenkins -y
```
To switch Java versions (if needed):
```bash
update-alternatives --config java
```

#### Step 4: Start and Check Jenkins Service
```bash
systemctl start jenkins.service
systemctl status jenkins.service
```

### Accessing Jenkins
- Open your browser and enter: **`http://<PUBLIC_IP>:8080`**
- If access is blocked, update the **inbound rules** for port **8080**.
- To retrieve the admin password:
```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```
- Install plugins and create a user.

---

## Jenkins Job Types
- **Freestyle project**
- **Pipeline**
- **Multi-configuration project**
- **Folder**
- **Multi-branch pipeline**
- **Organization folder**

#### Job Actions
- **Create Job**: "New Item" → Choose job type
- **Run Job**: Click "Build Now"
- **Edit Job**: "Configure"
- **Build Logs**: Located in `/var/lib/jenkins/workspace/`

#### Parameterized Builds
- Choice parameters
- String parameters
- Multi-line string parameters
- File parameters
- Boolean parameters

---

## Troubleshooting

### Changing Jenkins Port Number
```bash
vim /usr/lib/systemd/system/jenkins.service  # Edit line 67 (Environment)
systemctl daemon-reload
systemctl restart jenkins.service
```

### Enabling Auto-Restart
```bash
chkconfig jenkins on
```

### Passwordless Login
```bash
vim /var/lib/jenkins/config.xml  # Change useSecurity from true to false
systemctl restart jenkins.service
```

### Parallel Builds
- Enable **"Execute concurrent builds if necessary"**
- Modify **"Manage Jenkins" → "Nodes" → "Built-in node" → Configure → Number of executors**

### Restore Deleted Jobs
- Install the **"Job Configuration History"** plugin

---

## Jenkins Triggers (CRON Jobs)

### CRON Syntax
```
* * * * *
| | | | |
| | | | |__ Day of the week (0-7)
| | | |____ Month (1-12)
| | |______ Day of the month (1-31)
| |________ Hour (0-23)
|__________ Minute (0-59)
```

### Build Triggers
- **Scheduled Jobs**: `Build periodically` → `* * * * *`
- **Poll SCM** (checks for code changes): `Poll SCM` → `* * * * *`
- **Webhooks** (GitHub triggers builds on commits):
  - GitHub → Repository → Webhooks → Add webhook → Payload URL: `jenkinsurl/github-webhook/`
  - Jenkins → Job → "Build triggers" → "GitHub hook trigger for GITScm polling"

---

## Throttle Builds
- Restricts the number of builds per interval to prevent crashes
- Configure: **Throttle builds → Number of builds: 3 → Time period: Hours**

---

## Master-Slave Architecture

### Purpose
- Distributes builds across multiple nodes
- Reduces load on Jenkins server
- Uses **SSH** for communication

### Steps to Set Up Slave Node
1. Install Java on the slave machine:
```bash
sudo dnf install -y java-11-amazon-corretto
```
2. Configure in Jenkins:
   - "Manage Jenkins" → "Nodes & Clouds" → "New Node" → Provide name → Permanent Agent
   - Set:
     - **Number of Executors**: Defines concurrent builds
     - **Remote Root Directory**: Default `/var/lib/jenkins/workspace/`
     - **Usage**: "Only build jobs with label expression matching this node"
     - **Launch Method**: "Launch agents via SSH"
   - Provide SSH credentials using a **private key**

---

## File Transfer via Jenkins
- Install "Publish over SSH" plugin
- Add SSH server details in "Manage Jenkins → System → Publish over SSH"
- In Job configuration: Add "Send files or execute commands over SSH"

---

## Jenkins Pipelines

### Syntax
```groovy
pipeline {
    agent any
    stages {
        stage('one') {
            steps {
                sh 'touch pipeline_file'
                sh 'echo "Hello World" >> pipeline_file'
            }
        }
    }
}
```

### Example: CI/CD Pipeline
```groovy
pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/ReyazShaik/java-project-maven-new.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Artifact') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
}
```

---

## Tomcat Setup

### Steps
1. Install Java:
```bash
sudo dnf install -y java-11-amazon-corretto
```
2. Download and Extract Tomcat:
```bash
wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.35/bin/apache-tomcat-10.1.35.tar.gz
tar -zxvf apache-tomcat-10.1.35.tar.gz
```
3. Configure User Authentication:
```xml
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<user username="tomcat" password="root123456" roles="manager-gui, manager-script"/>
```
4. Start Tomcat:
```bash
cd apache-tomcat-10.1.35/bin/
sh startup.sh
```

### Jenkins-Tomcat Integration
- Install **"Deploy to container"** plugin
- Configure a Jenkins job with **WAR deployment** to Tomcat

---

## SonarQube Integration
- Used for code quality analysis

### Setup
```bash
cd /opt/
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.6.50800.zip
unzip sonarqube-8.9.6.50800.zip
amazon-linux-extras install java-openjdk11 -y
chown sonar:sonar sonarqube-8.9.6.50800 -R
chmod 777 sonarqube-8.9.6.50800 -R
su - sonar
sh /opt/sonarqube-8.9.6.50800/bin/linux/sonar.sh start
```

---
