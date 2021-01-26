# Task 1. Preparation
For this lab, you will need the training-data-analyst files and a Cloud Storage bucket.

Verify that the repository files are in Cloud Shell Editor
Clone the repository from the Cloud Shell command line:
```
git clone https://github.com/GoogleCloudPlatform/training-data-analyst
```
Click on refresh explorer icon. You should see the training-data-analyst directory.

Verify that you have a Cloud Storage bucket
If you don't have a bucket, you can follow these instructions to create a bucket.

In the Console, on the Navigation menu (7a91d354499ac9f1.png), click Home.
Select and copy the Project ID. For simplicity you will use the Qwiklabs Project ID, which is already globally unique, as the bucket name.
In the Console, on the Navigation menu (7a91d354499ac9f1.png), click Storage > Browser.
Click Create Bucket.
Specify the following, and leave the remaining settings as their defaults:
Property	Value (type value or select option as specified)
Name	<your unique bucket name (Project ID)>
Location type	Multi-Region
Location	<Your location>
Click Create.

Record the name of your bucket. You will need it in subsequent tasks.

In Cloud Shell enter the following to create an environment variable named "BUCKET" and verify that it exists with the echo command.
```
BUCKET="<your unique bucket name (Project ID)>"
echo $BUCKET
```
You can use $BUCKET in Cloud Shell commands. And if you need to enter the bucket name <your-bucket> in a text field in Console, you can quickly retrieve the name with echo $BUCKET.

Verify that Dataflow API is enabled for this project
Return to the browser tab for Console. In the top search bar, enter Dataflow API. This will take you to the page, Navigation menu > APIs & Services > Dashboard > Dataflow API. It will either show a status information or it will give you the option to Enable the API.

If necessary, Enable the API.

# Task 2. Open Dataflow project
The goal of this lab is to become familiar with the structure of a Dataflow project and learn how to execute a Dataflow pipeline. You will need to update some files to install Apache Beam. Apache Beam is an open source platform for executing data processing workflows.

Return to the browser tab containing Cloud Shell. In Cloud Shell navigate to the directory for this lab:
```
cd ~/training-data-analyst/courses/data_analysis/lab2/python
```
Install the necessary dependencies for Python dataflow:
```
sudo ./install_packages.sh
```
Verify that you have the right version of pip. (It should be > 8.0):

```
pip3 -V
```
If not, open a new Cloud Shell tab and it should pick up the updated version of pip.

Use refresh explorer icon in Cloud Shell editor to view the local copy of the repository.
If at any time during the DataFlow labs you are logged out of Cloud Shell due to inactivity, when you login the in-memory elements of Apache Beam will be lost. So you will need to reissue these commands before proceeding:
```
cd ~/training-data-analyst/courses/data_analysis/lab2/python
sudo ./install_packages.sh
```

# Task 3. Pipeline filtering
In the Cloud Shell code editor navigate to the directory /training-data-analyst/courses/data_analysis/lab2/python and view the file grep.py. Do not make any changes to the code.
Alternatively, you could view the file with nano. Do not make any changes to the code. If you use nano, press Ctrl + X to exit.
```
cd ~/training-data-analyst/courses/data_analysis/lab2/python
nano grep.py
```
Can you answer these questions about the file grep.py?

What files are being read?
What is the search term?
Where does the output go?
There are three transforms in the pipeline:

What does the transform do?

What does the second transform do?

Where does its input come from?

What does it do with this input?

What does it write to its output?

Where does the output go to?

What does the third transform do?

# Task 4. Execute the pipeline locally
In the Cloud Shell command line, locally execute grep.py.
```
cd ~/training-data-analyst/courses/data_analysis/lab2/python
python3 grep.py
```
Note: if you see an error that says "No handlers could be found for logger "oauth2client.contrib.multistore_file", you may ignore it. The error is simply saying that logging from the oauth2 library will go to stderr.

The output file will be output.txt. If the output is large enough, it will be sharded into separate parts with names like: output-00000-of-00001. If necessary, you can locate the correct file by examining the file's time.
```
ls -al /tmp
```
Examine the output file. Replace "-*" below with the appropriate suffix.
```
cat /tmp/output-*
```
Does the output seem logical?

# Task 5. Execute the pipeline on the cloud
Copy some Java files to the cloud.
```
gsutil cp ../javahelp/src/main/java/com/google/cloud/training/dataanalyst/javahelp/*.java gs://$BUCKET/javahelp
```
Edit the Dataflow pipeline in grepc.py. In the Cloud Shell code editor navigate to the directory /training-data-analyst/courses/data_analysis/lab2/python in and edit the file grepc.py.

Replace PROJECT and BUCKET with your Project ID and Bucket name. Here are easy ways to retrieve the values:
```
echo $DEVSHELL_PROJECT_ID
echo $BUCKET
```
Example strings before:

```
PROJECT='cloud-training-demos'
BUCKET='cloud-training-demos'
```
Example strings after edit (use your values):
```
PROJECT='qwiklabs-gcp-your-value'
BUCKET='qwiklabs-gcp-your-value'
```
Submit the Dataflow job to the cloud:
```
python3 grepc.py
```
Because this is such a small job, running on the cloud will take significantly longer than running it locally (on the order of 2-3 minutes).

Return to the browser tab for Console. On the Navigation menu , click Dataflow and click on your job to monitor progress.
Example:
img


Wait for the job status to turn to Succeeded. At this point, your Cloud Shell will display a command-line prompt.

Examine the output in the Cloud Storage bucket. By clicking Storage > Browser and click on your bucket. 

Alternatively, you could download the file in Cloud Shell and view it:
```
gsutil cp gs://$BUCKET/javahelp/output* .
cat output*
```
