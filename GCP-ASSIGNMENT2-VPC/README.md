### Q1 - Create an instance A in default VPC
1. Go to compute Engine --> VM instances --> Create.
![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT2-VPC/images/1.png)

2. Name the instance accordingly and configure it with desired configuration. 
![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT2-VPC/images/2.png)
3. Inside Networking interface, Select Default network. 
![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT2-VPC/images/3.png)
4. Click Create. A GCP instance in Default VPC will be created.

### Q2 - Launch instance B with only private ip in default VPC in different zone
1. Go to Compute Engine --> VM instances -->Create Instance
2. Name the instance with desired name and configure it in different region compared to previous instance.
3. In **Networking Interface** select **Default** Network.
4. Choose **External Ip** as **none**.
![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT2-VPC/images/4.png)

### Q3 - Configure NAT so that instance B can access internet.
Use the gcloud CLI in cloud shell for creating NAT in CLOUD NAT.

* Creating a CLOUD router for NAT
		
		gcloud compute routers create (cloud router name)
		\ --network (network name)
		\ --region us-central1
		
*  Creating a NAT for our private subnet in the given region  

		gcloud compute routers nats (nat config name)
		\--router-region us-central1 
		\--router (cloud router name) 
		\--nat-all-subnet-ip-ranges 
		\--auto-allocate-nat-external-ips
		
### Q4 - SSH into private instance using public instance		
1. SSH into public instance.
2.In terminal of public instance type - ssh (private instance name) (This will take us to the terminal of private instance)
3.In private instance's terminal type - sudo apt-get install nginx

