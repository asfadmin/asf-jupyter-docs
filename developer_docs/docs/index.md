# OpenSARlab

***Alaska Satellite Facility's OpenSARlab***

OpenSARlab is a service providing users with persistent, customizable computing environments. It insures that groups of scientists and students have access to identical environments, containing the same software, running on the same hardware. It operates in the cloud, which means anyone with a moderately reliable internet connection can access their development environment. OpenSARlab sits alongside ASF's data archives in AWS, allowing for low latency transfer of large data products.

OpenSARlab is a deployable service that creates an autoscaling Kubernetes cluster in Amazon AWS, running JupyterHub. Users have access to customizable environments running JupyterLab via authenticated accounts with persistent storage.

While OpenSARlab was designed with SAR data science in mind, it is not limited to this field. Any group 
development scenario involving large datasets and/or the need for complicated development environments
can benefit from working in an OpenSARlab deployment.

## How will OpenSARlab benefit my work as a SAR scientist?
OpenSARlab addresses the following issues that often arise when developing SAR data science techniques, especially in
 a collaborative setting:
 
 * Most SAR analysis algorithms require the installation of many interdependent Python science packages
 * Collaboration is often slowed or interrupted when contributors work in varying
 environments with different versions of installed dependencies
* SAR data products are often quite large, which leads to slow, expensive data transfers
* SAR scientists with limited resources may lack access to the hardware required for analysis

## How will OpenSARlab benefit the class or training I am teaching?
OpenSARlab alleviates some of the pitfalls commonly encountered when teaching software development and data science in any field:

 * Teaching is often interrupted when students work in varying environments, requiring valuable instructor time to help set up their systems so they may complete their assignments.
 * Students may lack the hardware needed to run the software required for assignments.
 * Students may lack the bandwidth needed to download large data products to their local computers.
 

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

### Deploy OpenSARlab to Your Own AWS Account _(Coming Soon)_

Take our publicly accessible codebase and create your own, self-managed deployments in Amazon AWS.

## Contact Us

Have questions, suggestions, or need advice? We would love to hear from you! [Send an email](
uaf-jupyterhub-asf@alaska.edu)