
I took part in the Microsoft Ignite: Optimize Azure with Defender for Cloud Challenge! I decided to document what I've learned in a blog. 

## Create an azure resource group and virtual network.

- Creating a virtual network using your active Azure subscription
  
![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/4a63bfc9-9ff6-470e-aa32-579bc2e733a4)

 - Creating a new resource group - az-rg-1 and named the Virtual network - vnet-1. Region will be East-US
   
![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/0a51a2d0-cc8f-4712-a6f0-2d8b1b5446a2)

- Editing the subnet-1, leaving the default addresses and the default size for our purposes. Also making sure the Private subnet is "Enabled"

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/ac19d464-5f3c-42f8-931c-7c696754aa43)

- Review & Create stage

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/ecd5bb8b-7686-4041-81a9-40c05ca8534a)



## Create application security groups to enable you to group together servers with similar functions, such as web servers. 

- Searching for the Application Security Groups section in the search bar. Then creating a new application security group, using our previous Resource group and active subscription. We will name the Instance asg-web as this is for our web application. 

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/b1aa7f7a-9106-4cef-a4fe-ede6c7715c27)

- Creating the security group, validation passed, going on to Create.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/be2f1f4c-cd38-4899-ba6e-b48d6b56598a)



- The application security group "asg-web" has been created and we are in deployment for the second created one called "asg-mgmt"

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/da211198-327f-473a-ba74-51c0adba66fa)



- Validation passed for the second security group "asg-mgmt"

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/98f164a9-3023-42d1-b2f7-38ef94b5180f)



## Create a network security group to secure network traffic in your virtual network.

Searched for Network Security Groups in the search bar.

- Created a security group named "nsg-1". It's passed the validation stage.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/fbd7f5d2-164a-4a64-9a96-6a03db002e54)


- The deployment is complete for the security group "nsg-1"

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/d05d7f8b-ce96-4c07-b281-2517cb686586)


## Now to Associate the network security group to the subnet

Going into nsg-1 we go to the left side and click "Subnets" under "settings"

 ![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/e069f610-4e38-4093-9711-38f21e52e8a4)


Since we don't already have a subnet, we will click the "+ Associate" button to Associate a subnet.

We will use the virtual network vnet-1(az-rg-1) and name the subnet (subnet-1).

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/aa876f91-773b-4db3-a945-0b557777735e)



## Time to create security rules for the network security group with the subnet of the virtual network created earlier.

- Clicking add to create a new inbound security rule.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/93e7da5e-5c2e-4ff2-b5bb-f507fcf07894)


- We will use the "asg-web" application security group we created earlier. Leave service as custom and the default ports, making sure TCP is selected. We will name this rule "allowweball". A nice name to describe exactly what it does.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/0118855a-15ab-4128-aa77-79efa97b459b)

- In this one we will use the "asg-mgmt" application security group. We will name this one  "allowrdpall" to allow all RDP. Making sure that RDP is selected from the Service drop down and the appropriate port #3389 shows up as default. We will save this rule.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/0176b750-3cfc-4e44-87cc-fbf52ad47eee)


### Time to create a virtual machine

- Searching Virtual Machine in the search bar and selecting create a virtual machine, we come to this window.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/114ec19f-28f5-4878-9a32-8d95310b152f)


- Using our Azure subscription and az-rg-1 resource group, we will name this virtual machine vm-1. "No infrastructure redundancy required" will be selected for this. Standard security and Windows Server 2022 Datacenter: Azure Edition.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/7482055d-bb42-4fd6-ab3e-cd69bb9ac53c)


- Onto the Disks section! We will select the only free option available which is Standard_b1s - 1 vcpu. Login information was provided during the challenge to use.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/fcb2ee39-53b8-4535-ae4d-1b56087c9c75)
 

- Onto the Networking section! We will use "vnet-1" and the "subnet-1" we created earlier. We will create a new Public IP vm-1-ip and selected "None" for the NIC network security group.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/118e0f88-d7d6-4cf1-ad49-c73f46511d86)


- It's passed the validation and onto the Review + Create section, ready to be finalized with the "Create" button.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/7dad0038-e5c8-4420-9003-b5153d73c90d)


- Deployment is in progress for the vm.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/1770b49b-09bb-4724-ab4e-f5e0363219ea)


- Deployment is complete!

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/c1a3b86d-e0d5-4aa2-b3ad-098df6c074bd)


### Onto creating the second VM - vm-2

- Passed validation.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/39cc8e55-8207-4c76-bee8-aba2b18be384)


- Deployment in progress.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/3825a2ec-6c32-482d-bebf-e69405b8d0fe)


- Deployment complete!

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/3d5a76e9-45a5-4bc5-9363-bd6e5528ccd0)



## Associate network interfaces to an application security group

- Now we can see the VMs we've created.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/2dfcf281-61a9-48db-a5a8-05faddddf3aa)


After selecting the first VM, we will go to the "Networking" tab under the "Settings" in the left menu.

We see there's section "Application Security Groups" under the Network Interface and we will select "Configure the applications security groups" edit option. This one is for "asg-web".

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/52ccf5d4-3093-48dd-acb3-f2d4e5dd0160)

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/4d214635-a530-4ef4-88fa-90b104f74d03)

- Created one for "asg-mgmt" as well!

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/2ecbd0d8-232a-4132-afc6-dcda12bc5e76)


# Created a Log Analytics workspace for Microsoft Defender for Cloud

In the search bar, typing "Log Analytics Workspaces" will bring you to this screen.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/1625a017-41cd-4be3-8245-23990a406751)


We will create a new workspace using the resource group azure-rg-1 and naming the instance with the name provided in the challenge "azwrkspc1a".

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/a4179901-390a-42cf-b149-31ecdf705118)


- Then we will deploy it!

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/73dcf874-fc11-4940-a2a4-8215ec53ad69)


![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/40cbc8e6-772d-49ce-a6cb-cad2a6162d2b)


## Enable just-in-time access on Virtual Machines

In this section, I learned how to configure and use Microsoft Defender for Cloud's just-in-time (JIT) access to protect Azure VMs from unauthorized network access.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/fc4d2bb3-2c48-4df0-99c0-9ac2ed5ca82f)

- Vm-1 configuration window
![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/35a6411e-f3a6-4b39-bd2f-53a545e249a3)

- Selected the VM in which I need to configure
![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/60a4044a-7e42-4c23-bb5e-77b83c635123)

- Viewing the JIT acess configuration which shows the port number, IP range and the time range. 
![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/b21338d5-f454-4d55-ac4a-5f0bc0a43d86)

- Configured JIT access for vm-1
![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/f32447bb-e9b2-4562-966c-21eb4d0db154)

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/49659c79-f5a1-4c9f-b75b-513954d6307a)


## Collecting data from your workloads with the Log Analytics agent

In this section, I learned how to configure and integrate a Log Analytics agent and workspace in Defender for Cloud in order to collect data from Azure VMs, Scale Sets, IaaS containers and non-Azure machines to monitor for security vulnerabilities and threats.

- Selected the workspace to use.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/03c49308-e995-4a33-b4e9-828121463c16)


- Defender Plans section under settings.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/ef530bc6-d7b2-41cf-8ca0-dc105ccc5988)


- Settings & Monitoring

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/1f27cd53-2975-43ca-816e-8fe5a0e4a815)

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/ac470d80-8090-4ea6-8bfd-a6b052e85eca)


![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/aa843721-f4dc-4bf1-95d2-4e2041018a64)



## Configured Key Vault  firewall and virtual networks.

In this section, I learned how to use the Azure portal to configure the Azure Key Vault networking settings to work with other apps and Azure services. 

Searched for the Key Vaults and ended up here!

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/8a64dbba-a210-4280-ab75-550252d10ee2)

Created a key vault named AZAPLKeyVaultx.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/dd9a8a6b-2feb-48f0-bc58-688de21617c7)

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/33e2d7bd-245a-4c0f-91c5-6ca8f57c6bd9)


Going into the Networking section of the created Key Vault.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/2acefae4-0773-4567-acda-61b55e499dad)


## Configured Azure Key Vault Recovery management with soft delete and purge protection.

In this section, I learned how to use purge protection in order to prevent the deletion of key vaults, secrets and certificates. 

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/a828c929-e3fe-4e90-862b-e26f1eb3ed5e)

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/26f5de7f-5273-4a22-85a2-80e942e9eb5e)



## Deploy a virtual machine to test connectivity privately and securely to the SQL server across the private endpoint. 

- Created a virtual network (classic). Created a new resource group "CreateSQLEndpointTutorial" with the instance name myVNet1a.

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/896af4e0-3b5a-410c-b258-5cdafcbad2ca)

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/1ae10cad-fc6f-4f76-a5cd-c86aa3e95124)



Do to my limited subscription, I was unable to fully create it. 

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/9c44db68-a1db-446f-8a7d-f8273d3fd347)

![image](https://github.com/CertainRisk/optimize-azure-with-defender-for-cloud-challenge/assets/141761181/5ede6be8-56f8-439e-a422-4b10fa42e4e9)
