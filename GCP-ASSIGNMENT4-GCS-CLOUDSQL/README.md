### Q1 - Host a static website using GCS bucket.

Steps : 

* Create a GCS bucket with desired storage configurations.
* Include all the files related to static website inside bucket.
* Make the files of your static bucket public by clicking on 3 dots and allowing it to all users.
* Access your bucket files by clicking on the index.html file and file URL.
* Your website is now accessible through the URL to the internet.

Screenshots : 

* Bucket :
 
![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT4-GCS-CLOUDSQL/images/bucket-details.png)

* Static Website :

![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT4-GCS-CLOUDSQL/images/static-website.png) 

### Q2 - Create a folder structure in the bucket as follows (manually) : 
 	-folder1
		- file1.txt
		-folder2
			-file2.txt
### Download the entire folder (folder1) on the local (cloud shell or vm) using python3 with standard library.

Screenshots : 

* Before Downloading : 

![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT4-GCS-CLOUDSQL/images/before-downloading.png)

* Bucket Details :

![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT4-GCS-CLOUDSQL/images/bucket-details-2.png)

* Cloud shell message :

![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT4-GCS-CLOUDSQL/images/cloud-shell-message.png)

* After Downloading :

![](https://raw.githubusercontent.com/hackerbat/GCP-ASSESSMENT/master/GCP-ASSIGNMENT4-GCS-CLOUDSQL/images/after-downloading-1.png)

Code :
		
	from google.cloud import storage
	import os

	BUCKET_NAME = 'rakesh-bucket-1'
	DOWNLOAD_FOLDER = 'folder1'
	DESTINATION_FOLDER = 'Downloads/'

	make destination folder in local machine
	try:
    	os.mkdir(DESTINATION_FOLDER)
	except Exception as e:
    	print('Destination folder already exists.')

	def main():
    	client = storage.Client()

    	bucket = client.get_bucket(BUCKET_NAME)

    	blobs = bucket.list_blobs()
    		
    	for b in blobs:
        
        	fold = DESTINATION_FOLDER + ''
        
        	if b.name.startswith(DOWNLOAD_FOLDER) and b.name[-1] != '/':
            
          	folder_struct = b.name.split('/')
            
            	for folder in folder_struct[:-1]:
                	fold += folder + '/'
                	try:
                    	os.mkdir(fold)
                	except Exception as e:
                    	pass
            
      		b.download_to_filename(fold + folder_struct[-1])

    print('Bucket "folder1" has been Downloaded to local !')

	if __name__ == '__main__':
    main()

		


