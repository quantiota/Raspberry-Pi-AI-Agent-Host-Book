# Raspberry Pi AI Agent Host


## A Simplified Overview of the AI Agent Host

 The AI Agent Host can be complex given that it involves several aspects such as AI, edge computing, Docker, and Raspberry Pi. Let me attempt to simplify it:  

The AI Agent Host is essentially a setup that allows you to run AI applications directly on a Raspberry Pi, which is a small, low-cost computer often used in various tech projects.  

The AI Agent Host functions as a "host" for an AI "agent". These applications can interact with live data, coming from either online sources (APIs) or the Raspberry Pi's own sensors, to make decisions or predictions.  

Moreover, the AI Agent Host is designed to be modular, which means you can add or remove different components depending on what your project needs. For example, if you need a specific database or visualization tool, you can add it to the setup.  

Also, you can use this setup in combination with a powerful GPU server. So, if you have tasks that are too demanding for the Raspberry Pi, you can send them to this server for processing. This is made possible with the inclusion of CodeServer and remote connection to a JupyterHub installed on the GPU server.  

Finally, the AI Agent Host uses lightweight services like QuestDB and Grafana, suitable for the Raspberry Pi's limited resources, and is optimized for DietPi, a lightweight operating system ideal for single-board computers like Raspberry Pi.  

I hope this explanation helps simplify the concept of the AI Agent Host. If you have any further questions or if something is still unclear, feel free to ask!  

### Features

The AI Agent Host, designed specifically for AI development, offers several key features making it an ideal solution for Raspberry Pi 4 with 8GB RAM, especially when running DietPi OS:

1. **Modular Environment**: The AI Agent Host is built as a module-based system, allowing different components to be added or removed based on the requirements of the project. This is perfect for the customizable nature of Raspberry Pi. Furthermore, by adding an AI Agent container, the AI Agent Host can be transformed into an AI Agent Lab, expanding its capabilities for AI development and experimentation.

2. **Live Data Interaction**: With the ability to work with live data from both APIs and Raspberry Pi's own sensors, AI Agent Host becomes a powerful tool for real-time data analysis, modeling, and decision-making.

3. **Lightweight Services**: Services like QuestDB and Grafana used in the AI Agent Host are lightweight yet robust, making them suitable for the Raspberry Pi's limited hardware resources compared to larger servers.

4. **Remote Development Capabilities**: The inclusion of Code-Server allows you to connect to a remote JupyterHub installed on a powerful GPU Server when necessary, using Raspberry Pi as the Docker host.

5. **Data Handling and Visualization**: QuestDB for efficient data handling and Grafana for intuitive data visualization are integral for any AI and machine learning projects.

6. **Optimized for DietPi**: The AI Agent Host's compatibility with DietPi, a lightweight OS optimized for single-board computers like Raspberry Pi, ensures efficient use of the Raspberry Pi's hardware resources.

7. **Community Support**: With active communities for both Raspberry Pi and AI Agent Host, you can expect robust support and resources for your AI development projects.

These features make the AI Agent Host a dynamic, effective, and efficient environment for AI development on a Raspberry Pi 4 with 8GB RAM, especially for projects involving real-time or sensor data.

### AI Agent Host Architecture Diagram

 ![AI Agent Host diagram](.images/ai-agent-host-diagram.png)
 
:pencil: High resolution diagram [Application architecture diagram](https://raw.githubusercontent.com/quantiota/Raspberry-Pi-AI-Agent-Host-Boook/images/ai-agent-host-diagram.png)




### AI Agent Host: A Novel Approach to Edge Computing

The AI Agent Host offers an innovative setup, connecting edge devices like the Raspberry Pi to a JupyterHub on a remote GPU server. This unique configuration, part of a broader trend known as edge computing, enables real-time data analysis and decision-making on the edge while offloading computationally intensive tasks to a GPU server in the cloud.

While this specific setup is not commonly seen or standardized, it adds significant value to fields that require real-time data analysis and decision-making capabilities at the edge. Potential applications include autonomous vehicles, Internet of Things (IoT), robotics, and more.

One of the primary challenges in edge computing is developing an infrastructure that allows for seamless communication and integration between edge devices and cloud servers. The AI Agent Host provides a powerful solution to this challenge, offering a framework that could potentially standardize these interactions.

As the AI industry continues to evolve rapidly, this innovative approach may become more commonplace. The AI Agent Host is at the forefront of this technological development, paving the way for new use cases and implementations.

Please note that while we strive to keep this document up-to-date, the field of AI is continuously evolving. For the latest information and developments, we recommend staying active in relevant online communities and keeping up with the latest research.

## How to set up the AI Agent Host on Raspberry Pi

The AI Agent Host was tested on DietPi installed on a Raspberry Pi 4 8GB. No other Linux distributions have been tested, but the instructions should be reasonably straightforward to adapt.

When testing the AI Agent Host, you can expect several types of test results depending on the specific aspects you are testing. Here are some common types of test results you might encounter:

1. **Successful deployment**: This result indicates that your Docker Compose configuration successfully deploys and starts all the services defined in your configuration file. It means that the containers are running, and the services are accessible as expected.

2. **Connectivity tests**: These tests verify whether the services within your Docker Compose setup can communicate with each other. They ensure that the networking between the containers is properly configured, and the services can interact as intended.

3. **Functional tests**: These tests assess the functionality of the services running within the Docker Compose setup. For example, if you have a web application container, you might test whether it responds correctly to HTTP requests, processes user input, and produces the expected output. Additionally, you can add the possibility to run notebooks as part of your functional tests. For instance, if your Docker Compose setup includes a Jupyter Notebook, you can design tests that execute specific notebook cells or workflows and verify the expected results. This allows you to validate the functionality of your notebooks and ensure that they produce the desired outcomes when running within the Docker Compose environment. Running notebooks as functional tests can help you ensure the correctness and reliability of your data processing, analysis, or machine learning workflows encapsulated in the notebooks within the Docker Compose environment.

4. **Integration tests**: These tests evaluate how well the different services integrated within your Docker Compose configuration work together. They validate whether the services can cooperate and exchange information or perform complex tasks as expected.

5. **Performance tests**: These tests focus on assessing the performance characteristics of your Docker Compose setup. They might involve measuring response times, throughput, resource utilization, or scalability under different workloads or stress conditions.

6. **Error handling tests**: These tests check how your Docker Compose configuration handles various error scenarios. For example, you might deliberately simulate a service failure and observe if the system gracefully recovers or if error conditions are properly handled.

7. **Security tests**: These tests assess the security posture of your Docker Compose setup. They might involve vulnerability scanning, penetration testing, or checking for misconfigurations that could expose your services to potential threats.

The specific test results you will obtain depend on the test cases you execute and the quality of your Docker Compose configuration. It's important to design and execute a comprehensive set of tests to ensure the reliability, performance, and security of your Dockerized application.

## Getting Started

To install the AI Agent Host, follow these steps:

1. Set up DietPi Operating System on the Raspberry Pi

The installation of DietPi consists of few steps:

- Provide the SD card installation media
- Get the DietPi image and put it on the installation media
- Boot up the DietPi device and go through one time installation steps
  
Following these steps you will be able to initially setup DietPi and install additional software packages you would like to use, using dietpi-software.

With root:dietpi login credentials:

Run dietpi-software from the command line.

```
dietpi-software
```

Choose Browse Software and select I2C, Prometheus Node Exporter, Docker Compose, Docker and Git. Finally select Install.
DietPi will do all the necessary steps to install and start these software items.


```
             |  [*] 72  I2C: enables support for I2C based hardware

             |  [*] 99   Prometheus Node Exporter: Prometheus exporter for hardware and OS metrics

             │  [*] 134  Docker Compose: Manage multi-container Docker applications                 
                 
             │  [*] 162  Docker: Build, ship, and run distributed applications    

             |  [*] 17   Git: Clone and manage Git repositories locally                                  

```

2. Reboot

```
sudo shutdown -r now
```

3. Clone the AI Agent Host repository and navigate to the docker directory.

with dietpi:dietpi login credentials:

```
umask 0002
git clone https://github.com/quantiota/Raspberry-Pi-AI-Agent-Host.git
umask 0022
cd Raspberry-Pi-AI-Agent-Host/docker

```
## Prerequisites

**Note**: A **fully qualified domain name**  (FQDN) is mandatory for running any notebooks from VSCode over **HTTPS**.


### 1 Generate Certificates with Certbot

We will use the Certbot Docker image to generate certificates. This service will bind on ports 80 and 443, which are the standard HTTP and HTTPS ports, respectively. It will also bind mount some directories for persistent storage of certificates and challenge responses. 

If you want to obtain separate certificates for each subdomain, you will need to run the **certbot certonly** command for each one. You can specify the subdomain for which you want to obtain a certificate with the -d option, like this:

```
sudo docker compose -f init.yaml run certbot certonly -d vscode.yourdomain.tld
```


```
sudo docker compose -f init.yaml run certbot certonly -d questdb.yourdomain.tld
```


```
sudo docker compose -f init.yaml run certbot certonly -d grafana.yourdomain.tld
```

**Important:** Replace **'yourdomain.tld'** with your actual domain in the commands above.

Please note that the **certonly** command will obtain the certificate but not install it. You will have to configure your Nginx service to use the certificate. Additionally, make sure that your domain points to the server on which you're running this setup, as Let's Encrypt validates domain ownership by making an HTTP request.

Also, remember to periodically renew your certificates, as Let's Encrypt's certificates expire every 90 days. You can automate this task by setting up a cron job or using a similar task scheduling service.


```
# /etc/cron.d/certbot: crontab entries for the certbot package (5 am, every monday)
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

 0 5 * * 1 sudo docker compose run certbot renew

```

### 2 Setup Environment Variables

Firstly, you will want to create an '**.env**' file in the docker folder with the following variables:

```
# sudo nano .env

# VSCode
PASSWORD=yourpassword

# Grafana
GRAFANA_QUESTDB_PASSWORD=quest

# QuestDB
QDB_PG_USER=admin
QDB_PG_PASSWORD=quest

```
and to define your domain name in the '**nginx.env**' file:

```
    # sudo nano nginx/nginx.env

    DOMAIN=yourdomain
```

Remember to replace the placeholders with your actual domain, passwords, and usernames. 

The environment variables will be replaced directly within the Nginx configuration file when the Docker services are started.


### 3 Generate dhparam.pem file

The **dhparam.pem** file is used for Diffie-Hellman key exchange, which is part of establishing a secure TLS connection. You can generate it with OpenSSL. Here's how to generate a 2048-bit key:

```
sudo openssl dhparam -out ./nginx/certs/dhparam.pem 2048
```

Generating a dhparam file can take a long time. For a more secure (but slower) 4096-bit key, simply replace 2048 with 4096 in the above command.

### 4 Generate .htpasswd file for QuestDB 

The user/password are the default one: admin:admin

The **.htpasswd** file is used for basic HTTP authentication. You can change it using the **htpasswd** utility, which is part of the Apache HTTP Server package. Here's how to create an **.htpasswd** file with a user named **yourusername**:
```
sudo htpasswd -c ./nginx/.htpasswd yourusername
```
This command will prompt you for the password for **yourusername**. The **-c** flag tells **htpasswd** to create a new file. **Caution**: Using the **-c** flag will overwrite any existing **.htpasswd** file. 

If **htpasswd** is not installed on your system, you can install it with **apt** on Ubuntu:

```
sudo apt-get install apache2-utils
```

### 5 Configure the Dockerfile for your specific needs.

When working with Docker, the Dockerfile acts as a blueprint for building containerized applications. While it's possible to utilize a standard or generic Dockerfile, it's often essential to tailor it to your project's unique demands. This is especially true when working with Python applications and their dependencies, or when there's a need to grant specific permissions like access to the [I2C bus](https://github.com/quantiota/Raspberry-Pi-AI-Agent-Host/tree/main/docs/weather-station).

Customizing your Dockerfile allows you to:

- **Manage Dependencies**: Through the use of a [**requirements.txt**](https://github.com/quantiota/Raspberry-Pi-AI-Agent-Host/blob/main/docker/vscode/requirements.txt) file, you can streamline and track the exact package versions your project requires.

- **Grant Specific Hardware Permissions**: If your application interacts with hardware interfaces such as I2C, it's necessary to grant the container the right permissions to access and communicate with these devices. In the Dockerfile, you can set up [user groups and permissions](https://github.com/quantiota/Raspberry-Pi-AI-Agent-Host/blob/main/docker/vscode/README.md) to ensure that your containerized application can successfully access and utilize the I2C bus or other necessary hardware interfaces.

By taking the time to customize your Dockerfile, you ensure that your application runs reliably and consistently in any environment.




### 6 Set up device mappings

Before initiating your services with Docker Compose, it's crucial to set up device mappings  ([I2C](https://github.com/quantiota/Raspberry-Pi-AI-Agent-Host/tree/main/docs/weather-station), [UART](https://github.com/quantiota/Raspberry-Pi-AI-Agent-Host/tree/main/docs/vehicle-tracking)) especially if any of your services require direct access to hardware devices on the host machine.

In our docker compose configuration
```
services:
  vscode:
    devices:
      - "/dev/i2c-1:/dev/i2c-1"

```
We've explicitly mapped the **/dev/i2c-1** device from the host to **/dev/i2c-1** inside the container. By doing so, when the service **vscode** is launched, it will have the necessary permissions to directly interface with the I2C device as if the service were running directly on the host.

Failing to set up this mapping before running **docker compose up** might lead to issues, as the service won't be able to access or communicate with the desired device, potentially causing errors or incomplete functionality.

It's essential to map these devices in the Docker Compose configuration **before** launching the service to ensure that the required hardware interactions function seamlessly within the containerized environment.


### 7 Launch the AI Agent Host using the provided docker-compose configuration.
After completing these steps, you can bring up the Docker stack using the following command:

```
sudo docker compose up --build -d
```
This will start all services as defined in your **docker-compose.yaml** file.


## Usage

### 1 Once the services are up and running, you can access the AI Agent Host interfaces:

- QuestDB: Visit https://questdb.domain.tld in your web browser.
- Grafana: Visit https://grafana.domain.tld in your web browser.
- Code-Server: Visit https://vscode.domain.tld in your web browser.

### 2 To connect the AI Agent Host to a remote JupyterHub environment from Code-Server:

1. Set up or use an existing remote JupyterHub that includes the necessary dependencies for working with your notebooks and data.

2. Connect to the remote JupyterHub environment from within the Code-Server interface provided by the AI Agent Host

### 3 Start working with your notebooks and data, using the pre-installed tools and libraries included in your remote environment.

You can also run the existing notebooks in the project folder within VSCode. 

[Weather Station](https://github.com/quantiota/Raspberry-Pi-AI-Agent-Host/tree/main/notebooks/weather-station) 

[GPS Tracker](https://github.com/quantiota/Raspberry-Pi-AI-Agent-Host/tree/main/notebooks/vehicle-tracking) 


## Frequently Asked Questions

1. **What is the AI Agent Host?**
   The AI Agent Host is a Dockerized environment designed for AI development. It's built on a modular system that allows different components to be added or removed based on the requirements of the project.

2. **Why use the AI Agent Host on a Raspberry Pi 4 8GB?**
   The AI Agent Host is lightweight yet powerful, making it suitable for the Raspberry Pi's limited hardware resources. It's designed to work with live data from both APIs and Raspberry Pi's own sensors, making it a powerful tool for real-time data analysis, modeling, and decision-making.

3. **Which services does the AI Agent Host include?**
   The AI Agent Host includes services such as Code-Server (a code editor), Grafana (a visualization tool), and QuestDB (a database). Additional services can be added or removed as needed.

4. **What do I need to connect to the Code-Server from a browser with HTTPS?**
   A fully qualified domain name (FQDN) is necessary to connect to the Code-Server from a browser using HTTPS. The FQDN ensures that the secure connection is correctly established.

5. **Can the AI Agent Host on a Raspberry Pi be used in combination with a remote JupyterHub installed on a GPU server?**

   Yes, this is one of the unique and powerful features of the AI Agent Host setup. You can use the AI Agent Host installed on a Raspberry Pi for real-time data analysis and decision making at the edge, while also connecting remotely to a JupyterHub installed on a GPU server for handling computationally intensive tasks. This innovative setup opens up new possibilities for AI development, especially in fields like IoT and edge computing.

6. **Can I use the AI Agent Host with other versions of the Raspberry Pi?**
   While the AI Agent Host has been tested and works well on the Raspberry Pi 4 8GB model, it should theoretically work on other models with sufficient hardware capabilities. However, performance may vary.

7. **Which operating systems are compatible with the AI Agent Host?**
   The AI Agent Host has been tested and found to be compatible with DietPi installed on a Raspberry Pi 4 8GB. Compatibility with other Linux distributions hasn't been extensively tested.

8. **Can I add my own services to the AI Agent Host?**
   Absolutely! The AI Agent Host is designed to be modular, allowing you to add or remove Docker containers as needed. This means you can customize the environment to include the exact tools and services that best suit your specific project's needs.

9. **What if I need help or support with the AI Agent Host?**
   There are active communities for both Raspberry Pi and AI Agent Host where you can expect robust support and resources for your AI development projects.



   ## References


1. Connect to a JupyterHub from Visual Studio Code. [Visual Studio Code](https://code.visualstudio.com/docs/datascience/jupyter-notebooks#_connect-to-a-remote-jupyter-server)

2. Create an API Token. [JupyterHub](https://jupyterhub.readthedocs.io/en/stable/howto/rest.html#create-an-api-token)

3. [Visual Studio Code](https://code.visualstudio.com/)

4. [QuestDB - The Fastest Open Source Time Series Database](https://questdb.io/)

5. [Grafana - The open observability platform](https://grafana.com/)

6. [Langchain](https://python.langchain.com)








