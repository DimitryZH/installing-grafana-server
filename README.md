

# Installing Grafana Server on Linux Ubuntu 22.04

## Overview
This project automates the installation and configuration of Grafana Server on a Linux Ubuntu 22.04 system. This script streamlines the setup process for system administrators and DevOps engineers by automating the installation of Grafana, adding Prometheus as a data source, and ensuring that the Grafana server is correctly configured to start on system boot.

## Features
- Automated Installation: Installs Grafana and its dependencies with a single command.
- Version Specification: Easily change the Grafana version by modifying a single variable.
- Prometheus Integration: Automatically configures Prometheus as a data source for Grafana.
- Systemd Integration: Ensures Grafana starts on system boot and provides commands to check its status.

## Usage:
**Clone the repository**:

   ```bash
   git clone https://github.com/DimitryZH/installing-grafana-server.git
   cd Grafana-Install-Script
   ```
**Make the script executable**:

   ```bash
   chmod +x install_grafana.sh
   ```
**Run the script**:

   ```bash
   sudo ./install_grafana.sh
   ```

## Configuration
- Grafana Version: Modify the GRAFANA_VERSION variable in the script to install a different version of Grafana.
- Prometheus URL: Change the PROMETHEUS_URL variable to point to your Prometheus server's URL.
## Results
Upon executing the script, the following steps and their outputs were observed:

**Navigating to the Grafana Directory**:

 ```bash
ubuntu@ip-172-31-30-156:/usr/share/grafana$ cd /usr/share/grafana
ubuntu@ip-172-31-30-156:/usr/share/grafana$ ll
total 96
drwxr-xr-x  10 root root  4096 May 24 15:00 ./
drwxr-xr-x 126 root root  4096 May 24 15:00 ../
-rw-r--r--   1 root root  5529 Apr 10 15:23 Dockerfile
-rw-r--r--   1 root root 34523 Apr 10 15:23 LICENSE
-rw-r--r--   1 root root   105 Apr 10 15:23 NOTICE.md
-rw-r--r--   1 root root  3261 Apr 10 15:23 README.md
-rw-r--r--   1 root root     8 Apr 10 15:23 VERSION
drwxr-xr-x   2 root root  4096 May 24 15:00 bin/
drwxr-xr-x   3 root root  4096 May 24 15:00 conf/
drwxr-xr-x   3 root root  4096 May 24 15:00 docs/
drwxr-xr-x   2 root root  4096 May 24 15:00 npm-artifacts/
drwxr-xr-x   6 root root  4096 May 24 15:00 packaging/
drwxr-xr-x   3 root root  4096 May 24 15:00 plugins-bundled/
drwxr-xr-x  16 root root  4096 May 24 15:00 public/
drwxr-xr-x   2 root root  4096 May 24 15:00 tools/
```
This output shows the various files and directories present in the Grafana installation directory, including configuration files, documentation, and executable binaries.

**Navigating to the bin Directory**:

 ```bash
ubuntu@ip-172-31-30-156:/usr/share/grafana$ cd bin
ubuntu@ip-172-31-30-156:/usr/share/grafana/bin$ ll
total 196568
drwxr-xr-x  2 root root      4096 May 24 15:00 ./
drwxr-xr-x 10 root root      4096 May 24 15:00 ../
-rwxr-xr-x  1 root root 197566416 Apr 10 15:23 grafana*
-rwxr-xr-x  1 root root   1852200 Apr 10 15:23 grafana-cli*
-rwxr-xr-x  1 root root   1852200 Apr 10 15:23 grafana-server*
```
Bin directory contains the executable binaries for Grafana, Grafana CLI, and Grafana Server. Listing the contents confirms these executables are in place and ready to be used.

**Navigating to and Inspecting the Datasources Configuration Directory**:

 ```bash
ubuntu@ip-172-31-30-156:/usr/share/grafana/bin$ cd /etc/grafana/provisioning/datasources
ubuntu@ip-172-31-30-156:/etc/grafana/provisioning/datasources$ ls -la
total 16
drwxr-xr-x 2 root grafana 4096 May 24 15:00 .
drwxr-xr-x 8 root grafana 4096 May 24 15:00 ..
-rw-r--r-- 1 root root     105 May 24 15:00 prometheus.yaml
-rw-r----- 1 root grafana 2648 May 24 15:00 sample.yaml
```
Here is  Grafana datasources provisioning directory and its contents. Confirm that the prometheus.yaml file has been created, which contains the configuration for adding Prometheus as a data source in Grafana.

**Displaying the Contents of prometheus.yaml**:

 ```bash
ubuntu@ip-172-31-30-156:/etc/grafana/provisioning/datasources$ cat prometheus.yaml 
apiVersion: 1

datasources:
  - name: Prometheus
    type: prometheus
    url: http://172.31.30.156:9090
```
The prometheus.yaml file has been correctly configured to use the specified Prometheus server URL.

These steps verify that Grafana has been installed, its binaries are present and executable, and Prometheus has been correctly configured as a data source.
Next navigate to Grafana UI.

**Screenshot of Grafana UI on Port 3000**:

After starting Grafana, access it via a web browser at ```http://your-server-ip:3000```. The following screenshot shows the Grafana UI with the Prometheus data source automatically connected:

![grafana-ui-data-sources](https://github.com/DimitryZH/installing-grafana-server/assets/146372946/9140293f-128e-43b4-844f-53d0f7ff32c3)


**Screenshot of Dashboard 1860 (Node Exporter Full)**:

Once Prometheus is connected, import and configure dashboard 1860 (Node Exporter Full) to visualize system metrics. The following screenshot shows this dashboard:

![grafana-dashbord-ID1860-Node-Exporter-Full](https://github.com/DimitryZH/installing-grafana-server/assets/146372946/1d94a93a-df01-4b7b-9c33-dd94ec16d463)

## Conclusion

This project demonstrates the  installation and configuration of Grafana on an Ubuntu 22.04 system using a custom Bash script. The script automates the process of setting up Grafana, including downloading and installing necessary packages, configuring Grafana to start as a service, and integrating Prometheus as a data source.
