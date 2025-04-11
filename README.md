# Configuration-management-with-helm

Project design and implement a simplified CI/CD pipeline using Jenkins, with a primary focus on Helm charts. The objective is to automate the deployment of a basic web application, promoting understanding and hands-on experience for those new to the field.

## Pre-requisite

- Basic knowledge of Jenkins essentials
- Enthusiasm and completion of the Introduction to Helm Charts and Working with Helm Charts mini projects

## Project Deliverables

- Documentation for each Helm chart component setup.</li>
- Explanation of simplified security measures implemented at each step.
- Step-by-step demonstration of the  CI/CD pipeline with Helm integration.

## Project Components

- Configure Jenkins server for a CI/CD pipeline automation.
Steps:
Install Jenkins on a dedicated server (with detailed explanations).
Set up necessary plugins (Git, Helm, etc.) with simple configurations.
Configure Jenkins with basic security measures suitable for beginners.

**Instructions for Jenkins:**

- Provide step-by-step documentation for Jenkins installation.
  Detail installation guide for jenkins can be found at
  [Jenkins installation](https://www.jenkins.io/doc/book/installing/docker/). However we would be installing Jenkins on ubuntu for this project.
  Before installing Jenkins we need to make make sure our system has Java JDK 17 or higher installed.

  Run `java --version` or install by running:

  ```bash
  sudo apt update
  sudo apt install fontconfig openjdk-17-jre

  ```

  The proceed to installing Jenkins LTS version by running:

  ```bash
  sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

  echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  <https://pkg.jenkins.io/debian-stable> binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

    sudo apt-get update
    sudo apt-get install jenkins

```

- Simplify the plugin installation and configuration steps.
After installation, you can access Jenkins via its default port: 8080 on your local machine by visiting [](http://localhost:8080)
- Outline basic security measures applied to the Jenkins server.
1. Create an admin user with a strong password to prevent unauthorised users and finish setup
2. Enable global secuirity and set authentication
   Under Jenkins security realm, choose Jenkin's own user database. Hence ensure allow user to signup is unchecked unless there is a need for it.
3. Ensure Jenkins is run behind a reverse-proxy like nginx or apache and configure HTTPs with TLS certificates
4. Alternatively, configure Jenkins to run directly on HTTPS by editing the jenkins.xml or startup command.
5. Install security related plugins
   - Role based authorization starategy
   - matrix authorization strategy
   - OWASP depency check
   - Audit Trail

### Helm Chart Basics

**Objective:** Introduce the fundamental concepts of Helm charts.
Steps:

- Explain what Helm charts are and their purpose.
- Walkthrough of creating a basic Helm chart for a web application.
- Cover Helm chart templating basics.

**Instructions:**

- Provide beginner-friendly explanations of Helm chart concepts.
- Include a hands-on guide for creating a simple Helm chart.

### Working with Helm Charts

**Objective:** Guide students in working with Helm charts for application deployment.
Steps:

- Deploy a sample web application using the Helm chart created.
- Introduce values and templates in Helm charts.
- Explore upgrading and rolling back applications using Helm.

- Instructions:
- Include simple examples and explanations for deploying applications with Helm.

- Provide a guide for Helm chart customization.

### Integrating Helm with Jenkins

**Objective:** Integrate Helm with Jenkins for automated deployments.
Steps:

- Integrate Jenkins with Helm for deployment automation.
- Configure Jenkins to use Helm charts in the CI/CD pipeline.
**Instructions:**
- Provide step-by-step instructions for integrating Helm with Jenkins.
- Simplify Jenkins configurations for Helm chart deployments.

### Integrating Helm With Jenkins

- Difference Between Helm and Kustomize
