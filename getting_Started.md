# Prerequisites for Workshop

## Windows
For BPM Enterprise, you need to use docker-compose. To run docker-compose on a windows machine, you need a docker desktop. For this reason, a windows server does not work as the Docker desktop does not run on a Windows server yet. When this becomes available, you should be able to do all of this on a Windows server. If you want to do this in the cloud, you will need to use Azure as AWS does not offer Windows 10. We have Azure images to share if you are interested.

## Linux
For Linux, All you need is to install docker-compos. Docker-compose on Linux is generally not a problem. I found that CentOS performs better when using a cloud AWS instance. The GUI on CentOS is more responsive than RedHat or other Linux instances. 


## Docker
To run the BPM Runtime Developer Server, you will need Docker-Compose installed on your environment. When we created this workshop, Docker Desktop did not run on windows 2016 or 2019 servers.
Make sure docker is installed and running before you start the BPME Server Run-time setup. You can download the BPM Enterprise binaries from the following location. https://docs.docker.com/docker-for-windows/install/

## BPM Enterprise
Instructions to Download the software or spin up an AMI
All software is available from the TIBCO edeliver website at
https://edelivery.tibco.com/storefront/eval/tibco-bpm-enterprise-formerly-tibco-activematrix-bpm-/prod10346.html

Select your operating system, accept the license agreement, and then individual file download.

You will need to download the TIBCO BPM Enterprise Software (v 5.0.0) server as well as the TIBCO Business Studio - BPM Edition Software (v 5.0.0) design-time components.

For the workshop, it may be easier to use the same machine for the server and the design-time components. We have created an Azure Windows 10 environment configured for the workshop with all required software.  Please reach out too, Mike Myburgh (mmyburgh@tibco.com) or Jagesh Tamboli (jtamboli@tibco.com) for details on this setup. We are working on getting this environment on Azure Marketplace.

### Server Installation
When installing the server, select to install the developer environment. This setup installs everything you will need for this workshop. The BPM Developer server installs the BPM Core Runtime and the Docker images required to run the server. As a recommendation, create a Tibco folder (c:\tibco) on windows or just \tibco in your Linux home folder.

The server install consists of 2 components. One is the binaries and, the other is the configuration for the BPM node. The binaries should normally put in c:\tibco\bpome50 and the configuration in c:\tibco\bpme50\config.

#### Starting and stopping the server components
The BPM Enterprise Development environment can be started and stopped with a docker-compose command. Docker-compose should be executed, from the following folder,
C:\tibco\bpme\bpm\5.0\samples\bpm-compose. The docker-compose.yml file manages the environment setup for you.

Microsoft Visual Studio Code is a great editor for creating all sorts of coding artifacts. What is nice about VS Code is that it allows you to install multiple different types of plugins for editing code, managing Docker containers, etc.

**Note: when doing a docker-compose down, it will delete all the deployed artifacts from your BPM Enterprise node. To preserve the project artifacts, do a docker-compose stop command to stop your node and a docker-compose start to bring the node up again.**

### Design-time installation
The design-time component consists of an Eclipse install with all the required functionality for designing BPM Enterprise components. You should always install the BPM Enterprise server and Design-time in separate folders. We recommended installing the design-time in c:\tibco\studio-50. 

Complete the setup and move to the next section.

# Understanding Case Management Methodology
The Next Step is to understand the implementation of the Case Management Methodology in the TIBCO BPM solution.
### Next Step : [Understanding Case Management Methodology](case_Management.md)

# Understanding the used case

Case Management use case - Disputes processing example.

### Build a Disputes Management Workflow

Let's begin by understanding the components of a project
### Next step: [Building Components of a Project](build_Project.md)
