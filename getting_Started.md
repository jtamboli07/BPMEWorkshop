# Prerequisites for Workshop

## Docker
To run the BPM Runtime Developer Server you will need Docker-Compose installed on your environment. This means you will need Docker Desktop on Windows 10 or Docker Compose on a linux environment. At the time we created this workshop, Docker Desktop did not work on windows 2016 or 2019 servers.
Make sure docker is installed and running before you start the BPME Server Run-time setup. The software can be found here https://docs.docker.com/docker-for-windows/install/

## BPM Enterprise
Instructions to Download the software or spin up an AMI
All software are available from TIBCO edeliver website at
https://edelivery.tibco.com/storefront/eval/tibco-bpm-enterprise-formerly-tibco-activematrix-bpm-/prod10346.html

Select your operating system, accept the license agreement and then individual file download.

You will need to download the TIBCO BPM Enterprise Software (v 5.0.0) server as well as the TIBCO Business Studio - BPM Edition Software (v 5.0.0) design-time components.

For the workshop it may be easier to use the same machine for the server as well as design-time components. We have created a Azure Windows 10 environment that has already been configured for the workshop with all required components. Please reach out to Mike Myburgh (mmyburgh@tibco.com) or Jagesh Tamboli (jtamboli@tibco.com) for details on this setup. We are working on getting this environment on Azure Marketplace.

### Server Installation
When installing the server, select to install the developer environment. This setup install everything you will need for this workshop. The BPM Developer server installs the BPM Core Runtime as well as the Built Docker images required to run the server. As a best practice it is recommended to create a tibco folder (c:\tibco) on windows or just tibco in your linux home folder.

The server install consists of 2 components. One is the binaries and the other the configuration for the BPM node. The binaries should normally put in c:\tibco\bpome50 and the configuration in c:\tibco\bpme50\config.

#### Starting and stopping the the server components
The BPM Enterprise Development environment can be started and stopped with a docker-compose command. The command should be executed from the following folder
C:\tibco\bpme\bpm\5.0\samples\bpm-compose. The docker-compose.yml file manages the environment setup for you.

Microsoft Visual Studio code  is a great editor for creating all sorts of coding artifacts. What is nice about VS Code is that it allows you to install multiple different types of plugins for editing code, managing docker containers etc.

**Note: when doing a docker-compose down, all the deployed artifacts will be deleted from your BPM Enterprise node. In order to preserve the project artifacts, do a docker-compose stop command to stop your node and a docker compose start to bring the node up again.**

### Design-time installation
The design-time component consists of a Eclipse install with all the required functionality for designing BPM Enterprise components. You should always install the BPM Enterprise server and Design-time in separate folders. Ii is normally good to install the design-time in c:\tibco\studio-50. 

Complete the setup and move to the next section.

# Understanding the use Case

Case Management use case Disputes processing example.

### Build a Disputes Management Workflow

Let's begin by understanding the components of a project
### Next step: [Building Components of a Project](build_Project.md)
