### Q1 - Steps to export all the logs related to firewall rules to BigQuery for further analysis

* To **_view or access_** Stackdriver logs of firewall IAM members need Project **owner**, **editor** or **viewer** or **Logs Viewer** roles assigned to them.
* Firstly to view the logs, logging must be opted while creating the firewall rules.
* To export logs we have to create one or **more** **sinks** that includes a **logs query** and an **export destination**.

**Steps** :

1. Go to **Stackdriver Logging > Exports** in the Cloud Console.
2. Select an existing Google Cloud project at the top of the page.
3. If you have not yet configured any log sinks, the message No Log sinks are configured is displayed. Then create a **sink** with and select **Sink Service** as **BigQuery** and **Sink Destination** also as **BigQuery**.
4. Steps to create a Sink : 

      * To create an export sink, click Create Export at the top of the Logs Exports page. You can also do this at the top of the Logs Viewer page.
      *  To create a sink, fill in the Edit Export panel as follows:
      	
	     1. **(filter):** Enter an advanced logs query.
      	
	     2. **Sink name:** Enter the identifier you want to assign to the sink.
      	
	     3. **Sink Service:** Select the sink service as BigQuery.
      	
	     4. **Sink Destination:** Select sink Destination as BigQuery.
      	
	     5. Click **Update Sink** to create the sink.   		 				

### Q2 - Configure Apache2 HTTP server on a GCE VM instance and setup an email alert notification which triggers when the health check of the instance fails.
* Create an instance and install apache2 on it.
* In StackDriver create a policy and name it.
* Metrics to be considered for health checks are :
	1. **CPU Utilization** 
	2. **Uptime Check**
* **Reasons** :  
	1. **CPU Utilization** : To keep a check on number of requests served.
	2. **Uptime check** : To check whether our website is being served or not.(If instance is down our website wont get served.)
* **Metric Values**  :
	1. **CPU Utilization** : Violates when Any
	compute.googleapis.com/instance/cpu/utilization stream is above a threshold of 0.000001 for greater than 1 minute.
	
	2. **Uptime check** : Violates when Any monitoring.googleapis.com/uptime_check/check_passed stream is above a threshold of 1 for greater than 1 minute.

* **Policy Screenshots** :
	1. **CPU Utilization** :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/cpu-utilization.png)
	2. **Uptime Check** :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/uptime-check.png)
* **Email Screenshots** :
	1. **CPU Utilization** :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/email_utilization.png)
	2. **Uptime Check** :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/email-uptime-check.png)
	3. **Check passed after sometime** :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/check_passed.png)

	

### Q3 - Create a Cloud Function to convert the pub/sub message to json file and store it in GCS bucket.
* Steps :
         
   1. Create a pub/sub topic to publish required messages.
   2. Create a cloud function and write the logic inside **main.py** which contains extracting message from topic, decoding it and putting it into a file test-file.json inside bucket.
   3. Publish the required message in the topic.
   4. Open your bucket and see the file with the message extracted from the topic in PUB/SUB.
   5. Write requirements (gcloud) inside **requirements.txt**.

* Screenshots :
		
	1. Pub/Sub Topic:
	 ![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/topic.png)
	
	2. Cloud Function :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/cloud-function.png)
	
	3. Logs of Cloud Function :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/logs-cf.png)
	
	4. test-file.json inside Bucket :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/file-in-bucket.png)
	5. message inside bucket :
	![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT3-CLOUDFUNCTION-STACKDRIVER/images/message-in-bucket.png)
	
* Code :
	
		import base64
		from gcloud import storage

		def hello_pubsub(event, context):
    	"""Triggered from a message on a Cloud Pub/Sub topic.
    	Args:
         event (dict): Event payload.
         context (google.cloud.functions.Context): Metadata for the
         event."""
         
    	pubsub_message = base64.b64decode(event['data']).decode('utf-8')
    	client = storage.Client()
    	bucket = client.get_bucket('rakeshreddy-bucket-1')
    	blob = bucket.blob('test-file.json')
    	blob.upload_from_string(pubsub_message)
