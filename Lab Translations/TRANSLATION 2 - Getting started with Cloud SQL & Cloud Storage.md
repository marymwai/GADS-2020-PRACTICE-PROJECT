#### `#PRACTICE PROJECT LAB TRANSLATION 2`

##### `#MODULE:  Google Cloud Platform Fundamentals - Core Infrastructure`

##### 	`#LAB - Google Cloud Fundamentals: Getting Started with  Cloud SQL`

##### 	`#Objectives:`

`In this lab, you learn how to perform the following tasks:`
`-Create a Cloud Storage bucket and place an image into it.`
`-Create a Cloud SQL instance and configure it.`
`-Connect to the Cloud SQL instance from a web server.`
`-Use the image in the Cloud Storage bucket on a web page.`

###### `#Task 1: Launch Cloud SDK`

###### `#Task 2: Deploy a web server VM instance`

​	`#step 1: Create VM Instance:` 
​		`gcloud compute instances create bloghost --machine-type=n1-standard-1 --image=debian-9-stretch --zone=us-central1-a --tags http`

​		`gcloud compute firewall-rules create allow-http --action=ALLOW --direction=INGRESS --rules=http:80 --target-tags-http`

​	`#step 2: Enter the following script as the value for Startup script:`
​		`apt-get update`
​		`apt-get install apache2 php php-mysql -y`
​		`service apache2 restart`

###### `#Task 3: Create a Cloud Storage bucket using the gsutil command line`

​	`#step 1: Enter your chosen location into an environment variable called LOCATION:`
​		`export LOCATION=US`

​	`#step 2: Cloud Shell, the DEVSHELL_PROJECT_ID environment variable contains your project ID. Enter this command to make a bucket named after your project ID:`
​		`gsutil mb -l $LOCATION gs://$DEVSHELL_PROJECT_ID`

​	`#step 3: Retrieve a banner image from a publicly accessible Cloud Storage location & Copy the banner image to your newly created  Cloud Storage bucket:`
​		`gsutil cp gs://cloud-training/gcpfci/my-excellent-blog.png my-excellent-blog.png /`
​		`gsutil cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png`

​	`#step 4: Modify the Access Control List of the object you just created so that it is readable by everyone:`
​		`gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png`

###### `#Task 4: Create the Cloud SQL instance`

​	`#step 1: Create Cloud SQL Instance`
​		`gcloud sql instances create blog-db --database-version=MYSQL_5_7 /`
​		`--tier=db-n1-standard-1 --region=us-central1 --zone=us-central1-a /`
​		`--root-password=password123`

​	`#step 2: Add User Account`
​		`gcloud sql users create blogdbuser --pasword=PASSWORD`

​	`#step 3: Add Network`

****

###### `#Task 5: Configure an application in a Compute Engine instance to use Cloud SQL`

`	 #step 1: SSH into bloghost instance`

​		 `gcloud compute ssh bloghost` 

`	       #step 2: change working directory to document root of web server`

`		cd /var/www/html`

`#step 3: use nano editor to edit a file, index.php and add content to it`

`						sudo nano index.php`

`	<html> <head><title>Welcome to my excellent blog</title></head> <body> <h1>Welcome to my 			excellent blog</h1> <?php $dbserver = "CLOUDSQLIP"; $dbuser = "blogdbuser"; $dbpassword = "DBPASSWORD"; // In a production blog, we would not store the MySQL // password in the document root. Instead, we would store it in a // configuration file elsewhere on the web server VM instance. $conn = new mysqli($dbserver, $dbuser, $dbpassword); if (mysqli_connect_error()) {        echo ("Database connection failed: " . mysqli_connect_error()); } else {        echo ("Database connection succeeded."); } ?> </body></html>  ....press ctrl+X to exit nano.`

`#step 4: Restart web server`

`	sudo service apache2 restart`

`#step 5:  open new browser tab and paste the bloghost VM instance' external IP followed by /inde.php`

`	loading the page should give an error beginning with-Database connection failed: ...`

`#step 6: Edit index.php again`

`	sudo nano index.php`

`	nano text editor, replace CLOUDSQLIP with the Cloud SQL instance Public IP address that you noted above. Leave the quotation marks around the value in place.`

`In the **nano** text editor, replace DBPASSWORD with the Cloud SQL database password that you defined above. Leave the quotation marks around the value in place.`

`press Ctrl+O then Enter to save the edits`

`press Ctrl+X to exit nano`

`#step 7: Restart web server`

`sudo service apache2 restart`

`Return to the web browser tab in which you opened your **bloghost** VM instance's external IP address. Reloading the page should give a successful connection`

