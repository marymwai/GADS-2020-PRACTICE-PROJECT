`#PRACTICE PROJECT LAB TRANSLATION 1`

`#MODULE: ESSENTIAL GOOGLE CLOUD INFRASTRUCTURE: FOUNDATION - Virtual Machines`

##### `#LAB: CREATING VIRTUAL MACHINES.`

`#Objectives: In this lab, you learn how to perform the following tasks:`

- `Create several standard VMs`
- `Create advanced VMs`

`#Task 1: Create a utility VM`

​	`#step 1:  Create VM`

​		`gcloud compute instances create utility-vm --machine-type=n1-standard-1 --image=debian-9-stretch --region=us-central1 --zone=us-central1-c --tags http`

​	`#step 2: Explore the VM details`

​		`gcloud compute instances describe` 

​	`#step 3: Explore the VM logs`

​		`gcloud logging read`

``	

`#Task 2: Create a  windows VM`

​	`#step 1: Create VM`

​		`gcloud compute instances create windows-vm     --region=europe-west2  --zone=europe-west2-a   --machine-type=n1-standard-2  --image-family=windows-server  --tags http    --boot-disk-type=ssd-persistent-disk   --boot-disk-size=100GB   --root-password=password`

​	`#step 2: Allow http & https traffic`

​		`gcloud compute firewall-rules create allow-http   --action=ALLOW  --direction=INGRESS   --rules=http:80   --target-tags=http`



`#Task 3: Create a  custom VM`

​	`#step 1: Create VM`

​		`gcloud compute instances create custom-vm   --region=us-west1  --zone=us-west1-b    --machine-type=custom   --custom-cpu=6   --custom-memory=32GB`

​	`#step 2:  SSH into the custom VM`

​		`gcloud compute ssh custom-vm`

​	`#step 3: To see info about unused and used memory and swap space on our custom VM`

​		`free`

​	`#step 4: To see details about the RAM installed on our VM`

​		`sudo dmidecode -t 17`

​	`#step 5: To verify the number of processors`

​		`nproc`

​	`#step 6: To see details about the CPUs installed on our VM`

​		`lscpu`

​	`#step 7: To exit the SSH terminal`

​		`exit`

``				