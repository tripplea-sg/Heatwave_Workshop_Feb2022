# Connect to MySQL DB System
When working in the cloud, there are often times when your servers and services are not exposed to the public internet. 
The Oracle Cloud Infrastructure (OCI) MySQL cloud service is an example of a service that is only accessible through private networks. 
Since the service is fully managed, we keep it siloed away from the internet to help protect your data from potential attacks and vulnerabilities. 
It’s a good practice to limit resource exposure as much as possible, but at some point, you’ll likely want to connect to those resources. 
That’s where Compute Instance, also known as a Bastion host, enters the picture. 
This Compute Instance Bastion Host is a resource that sits between the private resource and the endpoint which requires access to the private network 
and can act as a “jump box” to allow you to log in to the private resource through protocols like SSH. This bastion host requires a Virtual Cloud Network a
nd Compute Instance to connect with the MySQL DB Systems.
Today, you will use the Compute Instance to connect from the browser to a MDS DB System

## Task 1: Create SSH Key on OCI Cloud Shell
The Cloud Shell machine is a small virtual machine running a Bash shell which you access through the Oracle Cloud Console (Homepage). You will start the Cloud Shell and generate a SSH Key to use for the Bastion session.
### 1. To start the Oracle Cloud shell, go to your Cloud console and click the cloud shell icon at the top right of the page. This will open the Cloud Shell in the browser, the first time it takes some time to generate it.
![Image of picture1](https://github.com/tripplea-sg/Heatwave_Workshop_Feb2022/blob/main/Images/03vcn01.png)
