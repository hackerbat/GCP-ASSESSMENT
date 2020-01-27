### Q1 - Steps to export all the logs related to firewall rules to BigQuery for further analysis

### Q2 - Configure Apache2 HTTP server on a GCE VM instance and setup an email alert notification which triggers when the health check of the instance fails.
* Create an instance and install apache2 on it.
* In StackDriver create a policy and name it.
* Metrics to be considered for health checks are :
	1. CPU Utilization 
	2. Uptime Check
* **Reasons** :  
	1. **CPU Utilization** : To keep a check on number of requests served.
	2. **Uptime check** : To check whether our website is being served or not.(If instance is down our website wont get served.)
* **Metric Values**  :
	1. CPU Utilization : Violates when Any
	compute.googleapis.com/instance/cpu/utilization stream is above a threshold of 0.000001 for greater than 1 minute.
	
	2. Uptime check : Violates when Any monitoring.googleapis.com/uptime_check/check_passed stream is above a threshold of 1 for greater than 1 minute.

* **Policy Screenshots** :
	1. **CPU Utilization** :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/cpu-utilization.png)
	2. **Uptime Check** :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/uptime-check.png)
* **Email Screenshots** :
	1. CPU Utilization :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/email_utilization.png)
	2. Uptime Check :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/email-uptime-check.png)

### Q3 - Create a Cloud Function to convert the pub/sub message to json file and store it in GCS bucket.

		 
