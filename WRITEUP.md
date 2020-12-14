# Write-up Template

### Analyze, choose, and justify the appropriate resource option for deploying the app.

*For **both** a VM or App Service solution for the CMS app:*
- *Analyze costs, scalability, availability, and workflow*
- *Choose the appropriate solution (VM or App Service) for deploying the app*
- *Justify your choice*

**Virtual Machine**
- ***Cost:*** Virtual machines are slightly more expensive with the low spec option **B1ls** averaging at **$4.38** a month with pricing options.
- ***Scalability:*** Autoscaling via azure **virtual machine scale sets**. The client can scale the number of VMs in the scale set manually, or define rules to autoscale based on resource usage like CPU, memory demand, or network traffic.
- ***Availability:*** This is supported out of the box via azure **SLA for Virtual Machines**. For any Single Instance Virtual Machine using Standard HDD Managed Disks for Operating System Disks and Data Disks, they guarantee to have Virtual Machine Connectivity of at least 95%.
- ***Workflow:*** A lot of the management activities have to be performed manually by the client. The deployment is pretty straight forward as CI/CD solutions e.g. **Github Actions, Azure Devops Pipelines, Bitbucket Pipelines**. Some automation can be achieved via shell scripts but these still have to be written by the client.

**App Service**
- ***Cost:*** They can be costly as well but offer a free pricing tier for dev/test purposes i.e. the **F1** pricing tier with plenty of other non free options as well. Control over pricing that is scriptable.
- ***Scalability:*** Independently scalable tiers (cpu, memory and disk) and scale out (vm instances) are supported out of the box for app services. Clients have the option of scaling either manually via azure portal or the command line or automatically via azure's autoscaling feature.
- ***Availability:*** This is also supported out for the box via azure **SLA für App Service**. Microsoft Azure guarantee that Apps running in a customer subscription will be available 99.95% of the time. No SLA is provided for Apps under either the Free or Shared tiers.
- ***Workflow:*** Management and deployment is also straight forward as CI/CD solutions e.g. **Github Actions, Azure Devops Pipelines, etc** and a few others are supported out of the box. Merging your changes to the main branch therefore automatically triggers a CI/CD pipeline that builds and deploys your latest code to azure app service while azure app service takes care of restarting your application to pick the latest changes.

**Option Selected: App Service**
The application can be accessed via this link: [Article CMS App](https://article-cms-app.azurewebsites.net/)

**Justification:** In this case is the Azure App Service the best option, because:
- It ist not needed to think about the underlying OS or keeping it patched
- It can use Linux  or Windows if I like, and I can run PHP, Ruby, Java, .NET
- Lots of automatic benefits - backups, custom domains, ssl certs, git deploy, App Service Extensions, and on and on. Dozens of features.
- Control over pricing that is scriptable. We could write scripts to really pinch pennies by scaling your units up and down based on time of day or month.
- An "App Service Plan" on Azure can host as many Web Apps, Mobile Apps/Backends, Logic Apps and stuff in one as you like, barring perf or memory issues.

### Assess app changes that would change your decision.

*Detail how the app and any other needs would have to change for you to change your decision in the last section.*

**For projects that may require substantial modifications to the technology stack in the future, or for people worried about being locked into a single vendor, the extra work required to launch and maintain Virtual Machines might be worth it.**
