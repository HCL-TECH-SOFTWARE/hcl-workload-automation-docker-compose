<!DOCTYPE html>
<!-- saved from url=(0052)file:///C:/Users/preethi.kv/Downloads/Readme.md.html -->
<html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <link rel="stylesheet" href="./Readme.md_files/style.css">
</head>

<body class="stackedit">
  <div class="stackedit__html"><h1 id="hcl-workload-automation">HCL Workload Automation</h1>
<h2 id="introduction"><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose#introduction"></a>Introduction</h2>
<p>Workload Automation is a complete, modern solution for batch and real-time workload management. It enables organizations to gain complete visibility and control over attended or unattended workloads. From a single point of control, it supports multiple platforms and provides advanced integration with enterprise applications including ERP, Business Analytics, File Transfer, Big Data, and Cloud applications.</p>
<p>Docker adoption ensures standardization of your workload scheduling environment and provides an easy method to replicate environments quickly in development, build, test, and production environments, speeding up the time it takes to get from build to production significantly. Install your environment using Docker to improve scalability, portability, and efficiency.</p>
<p>This readme file contains the high-level steps to deploy all of the Workload Automation product components. However, for more detailed information about configuring a specific component, see:</p>
<ul>
<li><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose/blob/master/readmes/readme_SERVER.md">Server</a></li>
<li><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose/blob/master/readmes/readme_CONSOLE.md">Console</a></li>
<li><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose/blob/master/readmes/readme_DYNAMIC_AGENT.md">Dynamic Agent</a></li>
<li><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose/blob/master/readmes/readme_ZCENTRIC_AGENT.md">Zcentric Agent</a></li>
<li><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose/blob/master/fileproxy/README.md">FileProxy</a></li>
</ul>
<h2 id="accessing-the-container-images"><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose#accessing-the-container-images"></a>Accessing the container images</h2>
<p>You can access the HCL Workload Automation container images from the Entitled Registry:</p>
<ol>
<li>
<p>Contact your HCL sales representative for the login details required to access the HCL Entitled Registry.</p>
</li>
<li>
<p>Execute the following command to log in into the HCL Entitled Registry:</p>
<pre><code> docker login -u &lt;your_username&gt; -p &lt;your_entitled_key&gt; hclcr.io

</code></pre>
</li>
</ol>
<p>The images are as follows:</p>
<ul>
<li><a href="http://hclcr.io/wa/hcl-workload-automation-agent-dynamic:10.1.0.03.20230511-amd64">hclcr.io/wa/hcl-workload-automation-agent-dynamic:10.1.0.03.20230511-amd64</a></li>
<li><a href="http://hclcr.io/wa/hcl-workload-automation-server:10.1.0.03.20230511-amd64">hclcr.io/wa/hcl-workload-automation-server:10.1.0.03.20230511-amd64</a></li>
<li><a href="http://hclcr.io/wa/hcl-workload-automation-console:10.1.0.03.20230511-amd64">hclcr.io/wa/hcl-workload-automation-console:10.1.0.03.20230511-amd64</a></li>
</ul>
<h2 id="other-supported-tags"><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose#other-supported-tags"></a>Other supported tags</h2>
<ul>
<li>10.1.0.03.20230511-amd64</li>
<li>10.1.0.02.20230301</li>
<li>10.1.0.01.20221130</li>
<li>10.1.0.00.20220722</li>
<li>10.1.0.00.20220512</li>
<li>10.1.0.00.20220304</li>
<li>9.5.0.06.20221216</li>
<li>9.5.0.06.20220617</li>
<li>9.5.0.05.20211217</li>
</ul>
<h2 id="getting-started"><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose#getting-started"></a>Getting Started</h2>
<p>If you want to start the containers via Docker Compose, use the following command to clone the current repository:</p>
<pre><code>git clone https://github.com/WorkloadAutomation/hcl-workload-automation-docker-compose.git

</code></pre>
<p>If you do not have git installed in your environment, download the ZIP file from the main page of the repository:</p>
<pre><code>Click on "Code" and select "Download ZIP"

</code></pre>
<p>If you want to customize the installation parameters, modify the  <strong>docker-compose.yml</strong>  file.</p>
<p>Accept the product licenses by setting the  <strong>LICENSE</strong>  parameter to  <strong>“accept”</strong>  in the  <strong>wa.env</strong>  file located in the container package as follows:  <strong>LICENSE=accept</strong></p>
<p>In the directory where the  <strong>docker-compose.yml</strong>  file is located, you can start the containers by running the following command:</p>
<pre><code>docker-compose up -d

</code></pre>
<p>To verify that the containers are started, run the following command:</p>
<pre><code>docker ps 

</code></pre>
<p>You can optionally check the container logs using the following command:</p>
<pre><code>docker-compose logs -f &lt;container_name&gt;

</code></pre>
<p>Where, &lt;container_name&gt; represents one of the following: wa-server, wa-console or wa-agent.</p>
<h3 id="notes"><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose#notes"></a>Notes</h3>
<p>If your server component uses a timezone different from the default timezone, then to avoid problems with the FINAL job stream, you must update MAKEPLAN within the  <strong>DOCOMMAND</strong>, specifying the  <strong>timezone</strong>  parameter and value. For example, if you are using the America/Los Angeles timezone, then it must be specified as follows:</p>
<pre><code>$JOBS

WA_WA-SERVER_XA#MAKEPLAN
DOCOMMAND "TODAY_DATE=`${UNISONHOME}/bin/datecalc today pic YYYYMMDD`; ${UNISONHOME}/MakePlan -to `${UNISONHOME}/bin/datecalc ${TODAY_DATE}070
0 + 1 day + 2 hours pic MM/DD/YYYY^HHTT` timezone America/Los_Angeles"
STREAMLOGON wauser
DESCRIPTION "Added by composer."
TASKTYPE OTHER
SUCCOUTPUTCOND CONDSUCC "(RC=0) OR (RC=4)"
RECOVERY STOP

</code></pre>
<h2 id="docker-custom-certificates-enhancements">Docker custom certificates enhancements</h2>
<p><strong>Starting</strong> <strong>from</strong> IBM Workload Scheduler version 10.1 Fix Pack 3, the default SSL certificates have been removed from the containers of the Server, Console, and Agent components. For them to reach one another and perform the handshake, you have two different options while performing a <strong>FRESH</strong> installation:<br>
SCENARIO 1: Install in each container its own custom certificates, which must be generated by the user (recommended approach).<br>
SCENARIO 2: Do not install custom certificates, and use the custom certificate generated by each component during installation.</p>
<p>SCENARIO 1<br>
Generating your own Custom Certificates<br>
To generate the custom certificates on a Windows or UNIX machine run the following commands:</p>
<pre><code>openssl genrsa -out ./ca.key 40xx96
openssl req -x5x09 -new -nodes -key ./ca.key -subj "/CN=WA_ROOT_CA" -days 3650 -out ./ca.crt -config &lt;openssl_dir&gt;/openssl.cnf
openssl genrsa -des3 -passout pass:&lt;SSL_PASSWORD&gt; -out ./tls.key 40xx96
openssl req -new -key ./tls.key -passin pass:&lt;SSL_PASSWORD&gt; -out ./tls.csr -config &lt;openssl_dir&gt;/openssl.cnf -subj "/C=&lt;C&gt;/ST=&lt;ST&gt;/L=&lt;L&gt;/O=Global Security/OU=&lt;OU&gt; Department/CN=&lt;COMMON_NAME&gt;"
openssl x509 -req -in ./tls.csr -days 3650 -CA ./ca.crt -CAkey ./ca.key -CAcreateserial -out ./tls.crt
</code></pre>
<p>When you execute the above commands, you will receive six newly generated files, as provided in the screenshot below:</p>
<p>Store these files into the folder &lt;certificates_folder&gt; which will be later mounted as a volume of your containers.</p>
<p>SCENARIO 2</p>
<p>Only the &lt;SSL_PASSWORD&gt; variable is required to be set in this scenario, in each component in your docker-file.yaml.<br>
SSL_PASSWORD=&lt;YOUR_SSL_PASSWORD&gt; has to be set under the environment section<br>
During installation, each component will then generate its own custom certificate. Run the following commands in the Server and Console containers for them to communicate with each other:<br>
SERVER</p>
<pre><code>${WA_DIR}/TWS/JavaExt/jre/jre/bin/keytool -importcert -keystore
${WA_DIR}/usr/servers/engineServer/resources/security/TWSServerTrustFile.jks -storepass &lt;SSL_PASSWORD&gt; -storetype jks -file &lt;ca_console_file&gt; -alias wa_ca_console -noprompt
</code></pre>
<p>Console</p>
<pre><code>${WA_DIR}/TWS/JavaExt/jre/jre/bin/keytool -importcert -keystore ${WAUI_DIR}/java/jre/bin/keytool -importcert -keystore ${WAUI_DIR}/usr/servers/dwcServer/resources/security/TWSServerTrustFile.jks -storepass &lt;SSL_PASSWORD&gt; -storetype jks -file &lt;ca_server_file&gt; -alias wa_ca_server -noprompt
</code></pre>
<p>These commands will import the custom certificates of the components into the corresponding Trust Stores. In this way you can manually recover the generated certificates (&lt;ca_server_file &gt; or &lt;ca_console_file&gt;), and pass them from one component to another, and then execute the above commands.<br>
For example, if you need to import the &lt;ca_console_file&gt; generated in the Console container into the Server Trust Store, then:</p>
<ol>
<li>Retrieve &lt;ca_console_file&gt; from the container</li>
<li>Put the &lt;ca_console_file&gt; into the Server container, either through a shared volume or through docker cp command</li>
<li>Execute the SERVER command listed above</li>
</ol>
<p>Upgrade Scenario<br>
When performing an Upgrade, the above steps documented on both the scenarios are still needed, along with it, it is also required to set the SSL_KEY_FOLDER variable under the environment section of all the components. The value of such variable is the path to the already-existing folder into each component containing the default certificates coming from the previous release:<br>
SSL_KEY_FOLDER=&lt;path_to_the_folder_containing_all_your_default_certificates&gt;</p>
<p>Hybrid Scenario<br>
Let us understand hybrid scenario with an example and this is applicable starting from version 10.1 Fix Pack 3.<br>
For example, if you deploy the Server component on Container, and the Console component on-premise, this kind of hybrid deployment still needs you to perform some actions in order to import the custom certificates that are placed into the Container component into the component that is deployed on-premise.<br>
In the example above (Console on-premise, Server Container), the Console does not recognize the custom certificate &lt;ca_server_file&gt; of the Server, so you need to import that certificate into the Console’s Trust Store by executing the following command:</p>
<pre><code>${WAUI_DIR}/java/jre/bin/keytool -importcert -keystore ${WAUI_DIR}/usr/servers/dwcServer/resources/security/TWSServerTrustFile.jks -storepass &lt;SSL_PASSWORD&gt; -storetype jks -file &lt;ca_server_file&gt; -alias wa_ca_server -noprompt
</code></pre>
<h2 id="supported-docker-versions"><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose#supported-docker-versions"></a>Supported Docker versions</h2>
<p>This image is officially supported on Docker version 19.x or later.</p>
<p>Support for versions earlier than 19.x is provided on a best-effort basis.</p>
<p>Please see the  <a href="https://docs.docker.com/engine/installation/">Docker installation documentation</a>  for details on how to upgrade your Docker daemon.</p>
<h2 id="limitations"><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose#limitations"></a>Limitations</h2>
<p>The owner of all product files is the wauser user, thus the product does not run as root, but as wauser only. Don not perform the login as root to start processes or execute other commands such as Jnextplan, otherwise it might create some issues.</p>
<p>Limited to amd64 and Linux on Z platforms.</p>
<h2 id="additional-information"><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose#additional-information"></a>Additional Information</h2>
<p>For additional information on about the HCL Workload Automation, see the  <a href="https://help.hcltechsw.com/workloadautomation/v95/index.html">online</a>  documentation. For technical issues, search for Workload Scheduler or Workload Automation on  <a href="http://stackoverflow.com/search?q=workload+scheduler">StackOverflow</a>.</p>
<h2 id="license"><a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose#license"></a>License</h2>
<p>The Dockerfile and associated scripts are licensed under the  <a href="http://www.apache.org/licenses/LICENSE-2.0">Apache License 2.0</a>. HCL Workload Automation is licensed under the HCL License Agreement. This license for HCL Workload Automation can be found  <a href="https://github.com/HCL-TECH-SOFTWARE/hcl-workload-automation-docker-compose/blob/master">online</a>. Note that this license does not permit further distribution.</p>
</div>



</body></html>
