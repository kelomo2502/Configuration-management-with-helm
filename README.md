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
  /etc/apt/sources.list.d/jenkins.list > /dev/null```

    `sudo apt-get update`
    `sudo apt-get install jenkins`


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
helm is a package manager for kubernetes. It simplifies kubernetes deployment and also provides easy way for rolling back deployment incase we need to
- Include a hands-on guide for creating a simple Helm chart.
To create charts, we would need to first intall helm by running the following commands:
Note: We we are installing on an ubuntu machine but you can go to the official site to see how you can install for other OS
[Install Helm](https://helm.sh/docs/intro/install/)

```bash
   curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
   chmod 700 get_helm.sh
   ./get_helm.sh
```

After installation, we can create our helm chart by running `helm create <name of chart>` in our desired folder

### Working with Helm Charts

**Objective:** Guide students in working with Helm charts for application deployment.
Steps:

- Deploy a sample web application using the Helm chart created.
  In this example we are deploying a simple cafe web app template from tooplate.com. After downloading the sample app we we would create a folder call "Configuration management with helm"
  let's see how the folder strucuture will look like:
  Configuration-management-with-helm/
      app/
         Dockerfile
      cafe-chart/
   the app directory contains all our app and other folders and files needed to run the website while our cafe-chart contains our helm chart created from runnig `helm install cafe-chart` in the root directory of our project
- Introduce values and templates in Helm charts.
  The helm install command generate a scaffold for our helm packgaes aand files needed to use our helm chart but we would focus more on the values.yaml and deployment.yaml at this stage

  We would edit the image part of the values.yaml to use the image we would be building from our app after we specified our Dockerfile in the app directory.
  Our Dockerfile looks something like this:

```DSL
FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*

COPY . /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

  ```

we can build the docker image by running
`docker build -t docker-username/image-name:tag .`
we can push the image by running:
`docker push docker-username/image-name:tag`
Note: you need to login to your dockerhub account by runnig `docker login` The follow the prompt

- Explore upgrading and rolling back applications using Helm.
  Having created the helm chart and editing our values.yaml and deployment.yaml file to use our docker image, we can upgrade our helm deployment by running:
  `helm upgrade --install name-of release chart-directory`
  A rollback can be achieved in the similar version from the CLI by first running helm list
  
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
