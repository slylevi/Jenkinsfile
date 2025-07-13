# Jenkinsfile
# Splunk Logging Lab + CI/CD Automation with Jenkins & Ansible

This project simulates a real-world logging and monitoring system using **Splunk**, while showcasing a complete **CI/CD pipeline** powered by **Jenkins**, **GitHub**, and **Ansible**. It’s built on macOS with automation, monitoring, and system configuration in mind — a hands-on replica of what’s used in production TechOps and DevOps environments.

---

## 📦 Technologies Used

- **Jenkins** – CI/CD automation server
- **Ansible** – Configuration management
- **GitHub** – Source control
- **Python** – Log simulation
- **macOS** – Host system
- **VirtualBox + Ubuntu (optional)** – For Linux-based testing
- **Splunk Enterprise (Trial)** – Local logging and monitoring

---

## 📁 Project Structure

splunk-logging-lab/
├── Jenkinsfile # Jenkins pipeline (pulls repo, runs Ansible)
├── deploy.yml # Ansible playbook to simulate deployment
├── log_generator.py # Python script to simulate log activity
├── error_storm.py # Simulated incident: ERROR log flood
└── README.md # Project documentation


---

## 🚀 What This Project Does

### 🔹 Simulates a Logging Pipeline
- Uses Python to generate live application logs
- Ingests logs into Splunk via monitored log files
- Builds a dashboard and alert system inside Splunk

### 🔹 Automates CI/CD Workflow
- Jenkins pulls code from GitHub
- Runs `ansible-playbook` to simulate a deployment
- Writes `index.html` or other artifacts to simulate a "release"

---

## 🛠️ Jenkins Pipeline (Jenkinsfile)

```groovy
pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'git@github.com:slylevi/splunk-logging-lab.git'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh 'ansible-playbook ./deploy.yml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}
