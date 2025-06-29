

# Workload Automation FileProxy
## Introduction
Workload Automation is a complete, modern solution for batch and real-time workload management. It enables organizations to gain complete visibility and control over attended or unattended workloads. From a single point of control, it supports multiple platforms and provides advanced integration with enterprise applications including ERP, Business Analytics, File Transfer, Big Data, and Cloud applications.
You can use the file proxy to store and manage securely files to be transferred with the File Transfer integration available on [Automation Hub](https://www.yourautomationhub.io/). Installing the file proxy as a separate component on a workstation different from the master domain manager allows you to reduce network traffic and resource usage on the master domain manager.
Docker adoption ensures standardization of your workload scheduling environment and provides an easy method to replicate environments quickly in development, build, test, and production environments, speeding up the time it takes to get from build to production significantly. Install your environment using Docker to improve scalability, portability, and efficiency.





## Supported tags
- 10.2.4.00.20250423
- 10.2.3.00.20241122
- 10.2.2.00.20240424
- 10.2.1.00.20231201
- 10.2.0.00.20230728
- 10.1.0.05.20240712
- 10.1.0.04.20231201
- 10.1.0.03.20230511-amd64
- 10.1.0.02.20230301
- 10.1.0.00.20220304
- 9.5.0.05.20211217
 
 ## Supported platforms
 The supported operating systems are: Windows, Linux intel based 64-bit, and Linux on Z.
 



## Accessing the container images
### From the Entitled Registry
You can access the Workload Automation FileProxy container image from the Entitled Registry:
1. Access the entitled registry. Contact your HCL sales representative for the login details required to access the HCL Entitled Registry.
3.  Run the following command to login into the HCL Entitled Registry:
        
	docker login -u <your_username> -p <your_entitled_key> hclcr.io

Before you deploy HCL Workload Automation components on Linux on Z, see [Deploying Docker compose on Linux on Z](https://help.hcltechsw.com/workloadautomation/v1024/distr/src_pi/awspizLinuxDeployments.html)





## Getting Started
You can deploy the HCL Workload Automation containers using either Docker compose or Docker run. For both of these methods, ensure you download and install [Docker](https://www.docker.com).
### Getting started with Docker compose
Download and install [Docker compose](https://docs.docker.com/compose/). We recommend version 1.27 or later to take advantage of named volumes.
To start the container via Docker Compose, run the following command to clone the current repository:

	git clone https://github.com/WorkloadAutomation/hcl-workload-automation-docker-compose.git

If you do not have GitHub installed in your environment, download the ZIP file from the main page of the repository:
    Click on "Code" and select "Download ZIP"
If you want customize the installation parameters, modify the **docker-compose.yml** file.
Accept the product licenses by setting the **LICENSE** parameter to **"accept"** in the **wa.env** file located in the container package as follows: **LICENSE=accept**
In the directory where  the **docker-compose.yml** file has been located, you can start the containers by running the following command:
    docker-compose up -d wa-fileproxy
Once the command has been launched, be sure that the containers are started using the following command:
    docker ps
You can optionally check the container logs using the following command:
    docker-compose logs -f wa-fileproxy
### Getting Started with Docker run
To start the container from the command-line, launch the following command by adding the name of the image that has been loaded:
    docker run \
        -d -e SSL_PASSWORD=<your_certificate_password> \
        -e LICENSE=ACCEPT \
        -v <path_on_host_containing_certs>:/opt/wautils/certs \
        hcl-workload-automation-fileproxy:10.1.0.00.<release_date>
> **Note:** The name of the image has to be the same as the one you loaded on your local workstation when you launched the docker load command.
> **Note:** After launching the docker load command, you can see the name of the loaded image that should be defined either in the *docker run* command or in the *docker-compose.yml* file to start the container. For further information, see the Configuration Variables section.
### Installing with .PEM certificates
To use custom certificates, modify the volume `<path_on_host_containing_certs>:/opt/wautils/certs` with the path of the directory that contains your certificates at the place of `<path_on_host_containing_certs>`. In the defined folder, add the following certificates:
      - ca.crt
      - tls.key
      - tls.crt
## Configuration Variables
The following table lists the configurable variables for the Workload Automation FileProxy:
For example, specify the variable and its value as follows:
| Variable        | Description                                                                                                                                                                                                                                                                   | Mandatory   | Example     | Default   |
| --------------  | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  | ----------  | ----------- | ----------- | 
| LICENSE         | Use ACCEPT to agree to the license agreement          | yes         | accept       | notaccepted
| WA_DEBUG        | The container is executed in debug mode to keep container running in case of errors | no       | true                                          | false
| SSL_PASSWORD    | The password to access the certificates                                                                                                                                                                                                                                  | yes         | password   | |                      |
| SSL_PORT        | The port to be used for secure communication                                                                                                                                                                                                                                  | yes         | 44444     | 44444 |                      |








## Supported Docker versions
This image is officially supported on Docker version 19.xx.xx, or later.

Support for versions earlier than 19.xx.xx, is provided on a best-effort basis.

See the [Docker installation documentation](https://docs.docker.com/engine/installation/) for details on how to upgrade your Docker daemon.  


  

## Limitations
The owner of all product files is the wauser user, thus the product does not run as root, but as wauser only. Do not perform the login as root to start processes or run other commands, otherwise it might create some issues.
On amd64 and Linux on Z platforms.


## Additional Information
For additional information about how to use the HCL Workload Automation, see the [online](https://help.hcl-software.com/workloadautomation/v1024/index.html) documentation. For technical issues, search for Workload Scheduler or Workload Automation on [StackOverflow](http://stackoverflow.com/search?q=workload+scheduler).


## License
The Dockerfile and associated scripts are licensed under the [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0). HCL Workload Automation is licensed under the HCL International Program License Agreement. This license for HCL Workload Automation can be found [online](). Note that this license does not permit further distribution.
