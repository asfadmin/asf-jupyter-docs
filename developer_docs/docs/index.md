# OpenSARlab

***Alaska Satellite Facility's OpenSARlab***

OpenSARlab is a deployable service that creates a scalable Kubernetes cluster in Amazon AWS, running JupyterHub. Users
have access to customizable environments running JupyterLab and authenticated accounts with persistent storage.

OpenSARlab addresses the following issues common to teaching and developing SAR data science techniques, especially in
 a collaborative setting:
 
 * Most SAR analysis algorithms require the installation of many interdependent Python science packages
 * Teaching and collaboration is often slowed or interrupted when student or collaborators work in varying
 environments with different versions of installed dependencies
* SAR data products are often quite large, which leads to slow, expensive data transfers
* SAR scientists with limited resources may lack access to the hardware required for analysis

OpenSARlab insures that groups of scientists or students have access to identical environments, containing the same
software and running on the same hardware. It runs in the cloud, which means that anyone with a moderately reliable 
internet connection can access their development environment. OpenSARlab sits alongside ASF's data archives in AWS, 
allowing for low latency transfer of large data data products.

While OpenSARlab was designed with SAR data science in mind, it is not limited to this field. Any group software 
development scenario involving large datasets stored in AWS and/or the need for complicated development environments
can benefit from working in an OpenSARlab deployment. 

## How to Access OpenSARlab

### As a Paid Service Managed by Alaska Satellite Facility Enterprise
 
Contact ASF-E to discuss options for setting up an OpenSARlab deployment to suit your needs.

### Deploy OpenSARlab to Your Own AWS Account

Take our publicly accessible codebase and create your own, self-managed deployments in Amazon AWS.

## Contact Us

Have questions, suggestions, or need advice? We would love to hear from you! [Send an email]()