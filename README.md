
# HCL Workload Automation

## Introduction

Workload Automation is a complete, modern solution for batch and real-time workload management. It enables organizations to gain complete visibility and control over attended or unattended workloads. From a single point of control, it supports multiple platforms and provides advanced integration with enterprise applications including ERP, Business Analytics, File Transfer, Big Data, and Cloud applications.

Docker adoption ensures standardization of your workload scheduling environment and provides an easy method to replicate environments quickly in development, build, test, and production environments, speeding up the time it takes to get from build to production significantly. Install your environment using Docker to improve scalability, portability, and efficiency.

This readme file contains the high-level steps to deploy all of the Workload Automation product components. However, for more detailed information about configuring a specific component, see:

* [Server](readmes/readme_SERVER.md)
* [Console](readmes/readme_CONSOLE.md)
* [Dynamic Agent](readmes/readme_DYNAMIC_AGENT.md)
* [Zcentric Agent](readmes/readme_ZCENTRIC_AGENT.md)

## Accessing the container images

You can access the HCL Workload Automation container images from the Entitled Registry:

1. Contact your HCL sales representative for the login details required to access the HCL Entitled Registry.

2. Execute the following command to log in into the HCL Entitled Registry:

       docker login -u <your_username> -p <your_entitled_key> hclcr.io

The images are as follows:

* hclcr.io/wa/hcl-workload-automation-agent-dynamic:9.5.0.07.20240327
* hclcr.io/wa/hcl-workload-automation-server:9.5.0.07.20240327
* hclcr.io/wa/hcl-workload-automation-console:9.5.0.07.20240327

## Getting Started

If you want to start the containers via Docker Compose, use the following command to clone the current repository:

    git clone https://github.com/WorkloadAutomation/hcl-workload-automation-docker-compose.git

If you do not have git installed in your environment, download the ZIP file from the main page of the repository:

    Click on "Code" and select "Download ZIP"

If you want to customize the installation parameters, modify the **docker-compose.yml** file.

Accept the product licenses by setting the **LICENSE** parameter to **"accept"** in the **wa.env** file located in the container package as follows: **LICENSE=accept**

In the directory where  the **docker-compose.yml** file is located, you can start the containers by running the following command:

    docker-compose up -d

To verify that the containers are started, run the following command:

    docker ps 

You can optionally check the container logs using the following command:

    docker-compose logs -f <container_name>

Where, <container_name> represents one of the following: wa-server, wa-console or wa-agent.

### Notes

If your server component uses a timezone different from the default timezone, then to avoid problems with the FINAL job stream, you must update MAKEPLAN within the **DOCOMMAND**, specifying the **timezone** parameter and value. For example, if you are using the America/Los Angeles timezone, then it must be specified as follows:

    $JOBS

    WA_WA-SERVER_XA#MAKEPLAN
    DOCOMMAND "TODAY_DATE=`${UNISONHOME}/bin/datecalc today pic YYYYMMDD`; ${UNISONHOME}/MakePlan -to `${UNISONHOME}/bin/datecalc ${TODAY_DATE}070
    0 + 1 day + 2 hours pic MM/DD/YYYY^HHTT` timezone America/Los_Angeles"
    STREAMLOGON wauser
    DESCRIPTION "Added by composer."
    TASKTYPE OTHER
    SUCCOUTPUTCOND CONDSUCC "(RC=0) OR (RC=4)"
    RECOVERY STOP

## Supported Docker versions

This image is officially supported on Docker version 19.x or later.

Support for versions earlier than 19.x is provided on a best-effort basis.

Please see the [Docker installation documentation](https://docs.docker.com/engine/installation/) for details on how to upgrade your Docker daemon.

## Limitations

The owner of all product files is the wauser user, thus the product does not run as root, but as wauser only. Do not perform the login as root to start processes or execute other commands such as JnextPlan, otherwise it might create some issues.

Limited to amd64 and Linux on Z platforms.

## Additional Information

For additional information about using the HCL Workload Automation, see the [online](https://help.hcltechsw.com/workloadautomation/v95/distr/src_pi/awspipartdepcont.html) documentation. For technical issues, search for Workload Scheduler or Workload Automation on [StackOverflow](http://stackoverflow.com/search?q=workload+scheduler).

## License

The Dockerfile and associated scripts are licensed under the [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0). HCL Workload Automation is licensed under the HCL License Agreement. This license for HCL Workload Automation can be found [online](https://www.hcl-software.com/resources/master-agreements). Note that this license does not permit further distribution.
