* BOSH - Creates VMs on top of physical computing infrastructure and deploys CF on top of this cloud
* CF Cloud Controller - runs apps and others processes on cloud VMs. manages app lifecycle, load etc.
* Router - Routes traffic to the VMs through a customer provided load balancer.
* CF has 2 types of VMs 
    * Component VMs that constitute platform infrastructure.
    * Host VMs for hosting apps
* Diego system - load balancing, spanning new instances, failover, etc. It uses auction algorithm.
* CF distributes app source code to the VMs with everything VMs need to compile and run the app locally. It includes "OS Stack", Buildpacks, libraries and services the app uses.
* CF Cloud Controller stages it for delivery by combining stack, buildpack, sourcecode into a "droplet" that VM can unpack, compile and run.
* How CF Organizes Users and Workspaces?
    * CF manages user accounts through 2 UAA servers, which support access control as OAuth2 internally or can connect to external stores through SAML or LDAP. One for BOSH and other one for CFCC
* Loggregator aggregates component metrics and app logs into a structured form, the "Firehose", these can be directed to specific uses such as monitoring or analyze app usage by applying "nozzles".





