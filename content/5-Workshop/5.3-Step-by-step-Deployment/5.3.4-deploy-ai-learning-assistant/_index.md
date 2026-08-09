---
title: "Deploy AI Learning Assistant"
date: 2026-08-07
weight: 4
chapter: false
pre: " <b> 5.3.4. </b> "
---

## Objective

Deploy the **AI Learning Assistant Platform** to an **Amazon EC2** instance using **Docker Compose**. This section includes cloning the source code from GitHub, configuring environment variables, and launching the Docker Containers required by the system.

---

## Implementation

### Clone the Project Source Code

First, clone the **AI Learning Assistant Platform** source code from the GitHub Repository to the EC2 instance.

Run the following commands:

```bash
# Clone the project from GitHub
git clone https://github.com/<YOUR_GITHUB_USER>/AI-Learning-Assistant.git

# Navigate to the project directory
cd AI-Learning-Assistant
```

After the cloning process is completed successfully, the project source code will be stored on the EC2 instance and ready for the next configuration step.

---

### Configure Environment Variables

To protect sensitive information such as API Keys and passwords, the system uses **Environment Variables** instead of storing these credentials directly in the source code.

Copy the template configuration file to a local environment file:

```bash
cp projects/app/.env.template projects/app/.env.local
```

Then, open the **.env.local** file for configuration:

```bash
nano projects/app/.env.local
```

In the **.env.local** file, configure the environment variables required by the system, such as:

- **Root Password**
- **OpenAI API Key**
- **Other required application configuration settings**

After completing the configuration, save and close the **.env.local** file.

> **Note:** Do not upload the **.env.local** file containing API Keys, passwords, or other authentication credentials to the GitHub Repository.

---

### Launch the Application Using Docker Compose

After the source code and environment variables have been configured, launch the system using Docker Compose.

Run the following command:

```bash
# Launch the AI Learning Assistant Platform
docker compose -f deploy/dev/docker-compose.yml up -d
```

The `-d` option allows Docker Compose to run the containers in **detached mode**, meaning that the containers continue running in the background after the command is completed.

After the containers have been started, check their status using:

```bash
# Check the status of the containers
docker compose -f deploy/dev/docker-compose.yml ps
```

The system containers are expected to display a status of **Up**, **Running**, or **healthy**, depending on the configuration of each container.

> **Figure 5.3.7. Status of the Docker Containers after deploying the AI Learning Assistant Platform.**

> ![Figure 5.3.7](/images/5.3.7.png)

---

### System Verification

After the Docker Containers have been successfully started, verify that the system can be accessed through a Web browser.

Access the **Elastic IP** address of the Amazon EC2 instance:

```text
http://<ELASTIC_IP>
```

For example:

```text
http://13.219.3.244:3000
```

If the **AI Learning Assistant Platform** interface is displayed correctly in the browser, the application deployment process has been completed successfully.

> **Figure 5.3.8. AI Learning Assistant Platform interface after deployment on Amazon EC2.**

> ![Figure 5.3.8](/images/5.3.8.jpg)

---

## Result

After completing this step, the **AI Learning Assistant Platform** source code has been deployed to **Amazon EC2** using **Docker Compose**.

The system components are running as Docker Containers and can be verified using the **docker compose ps** command. Users can access the platform through the **Elastic IP** address of the EC2 instance.

The system is now ready for the next step, which is to configure the **Continuous Integration & Continuous Deployment (CI/CD)** pipeline.