# OpenSARlab

***Alaska Satellite Facility's OpenSARlab***

OpenSARlab is a service providing users with persistent, customizable computing environments. It insures that groups of scientists and students have access to identical environments, containing the same software, running on the same hardware. It operates in the cloud, which means anyone with a moderately reliable internet connection can access their development environment. OpenSARlab sits alongside ASF's data archives in AWS, allowing for low latency transfer of large data products.

OpenSARlab addresses the following issues common to teaching and developing SAR data science techniques, especially in
 a collaborative setting:
 
 * Most SAR analysis algorithms require the installation of many interdependent Python science packages
 * Teaching and collaboration is often slowed or interrupted when student or collaborators work in varying
 environments with different versions of installed dependencies
* SAR data products are often quite large, which leads to slow, expensive data transfers
* SAR scientists with limited resources may lack access to the hardware required for analysis

OpenSARlab is a deployable service that creates an autoscaling Kubernetes cluster in Amazon AWS, running JupyterHub. 
Users have access to customizable environments running JupyterLab via authenticated accounts with persistent storage.

While OpenSARlab was designed with SAR data science in mind, it is not limited to this field. Any group 
development scenario involving large datasets and/or the need for complicated development environments
can benefit from working in an OpenSARlab deployment.

## How is OpenSARlab different from Binder?

- Persistent, authenticated user accounts
- User group management 
- Persistent user storage
    - Cost reducing storage management features
- Customizable server resources (pick your EC2 size)
- Deployable to other AWS accounts
- Developer defined server timeouts (not restricted to 10 minutes of inactivity)

## How to Access OpenSARlab

### As a Paid Service Managed by Alaska Satellite Facility Enterprise
 
Contact ASF-E to discuss options for setting up an OpenSARlab deployment to suit your needs.

### Deploy OpenSARlab to Your Own AWS Account

Take our publicly accessible codebase and create your own, self-managed deployments in Amazon AWS.

## Contact Us

Have questions, suggestions, or need advice? We would love to hear from you! [Send an email]() #TODO address?