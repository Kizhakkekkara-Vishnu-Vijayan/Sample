# VPROFILE Project

## Overview 

The VPROFILE project is a multi-tier web application designed to showcase the deployment and management of a cloud-based environment using various technologies. The project architecture includes a database layer using MySQL, a backend application server running on Apache Tomcat, and a frontend web server powered by NGINX. Additionally, it utilizes services like RabbitMQ for message queuing and Memcached for caching, ensuring a scalable and efficient system.

## Description 

The VPROFILE project demonstrates how to set up and configure a robust infrastructure for a web application using a combination of open-source technologies. It covers the entire process from setting up virtual machines (VMs) to configuring each service, ensuring that all components work together seamlessly. The project is an excellent opportunity to practice deploying and managing a cloud-based environment, which is critical for any DevOps or cloud engineering role.

## Getting Started 

To get started with the VPROFILE project, you will need to prepare your environment with the necessary tools and dependencies. Once your environment is ready, follow the setup instructions to configure the VMs and deploy the application.

### Prerequisites 
Ensure that you have the following installed on your machine:

* Oracle VM VirtualBox
* Vagrant
* Vagrant plugins (e.g., hostmanager)
* A suitable code editor (e.g., Git Bash)

### Setup Overview

1. Clone the Repository: Start by cloning the project repository to your local machine.
2. VM Setup: Use Vagrant to bring up the required virtual machines, each handling a specific role such as database management, application serving, and web serving.
3. Service Configuration: Configure each service (MySQL, Memcached, RabbitMQ, Tomcat, NGINX) on its respective VM.
4. Deploy the Application: Once the environment is set up, deploy the web application and ensure all services are running correctly.

### Further Steps 

After setting up the project, you can explore various aspects such as load balancing with NGINX, database caching with Memcached, and message queuing with RabbitMQ. The application should be accessible either directly via the backend server (Tomcat) or through the frontend web server (NGINX).

## Project flow diagram

![3-tier Architecture diagram](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/flow_diagram.png)
