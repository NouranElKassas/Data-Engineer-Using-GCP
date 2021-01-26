#Task 1: Confirm that needed APIs are enabled
1. Make a note of the name of your Google Cloud project. This value is shown in the top bar of the Google Cloud Console. It will be of the form qwiklabs-gcp- followed by hexadecimal numbers.
2. In the Google Cloud Console, on the Navigation menu(Navigation menu), click Marketplace.
3. Click Enable APIs and Services.
4. In the Search for APIs & Services box, enter Cloud Build.
5. In the resulting card for the Cloud Build API, if you do not see a message confirming that the Cloud Build API is enabled, click the ENABLE button.
6. Use the Back button to return to the previous screen with a search box. In the search box, enter Container Registry or ou will find it as a feature.
7. In the resulting card for the Container Registry API, if you do not see a message confirming that the Container Registry API is enabled, click the ENABLE button.

#Task 2. Building Containers with DockerFile and Cloud Build
1. On the Google Cloud Console title bar, click Activate Cloud Shell. When prompted, click Continue. Cloud Shell opens at the bottom of the Google Cloud Console window. Create an empty quickstart.sh file using the nano text editor.

'''
nano quickstart.sh'''
Add the following lines in to the quickstart.sh file:
'''
#!/bin/sh
echo "Hello, world! The time is $(date)."
'''
Save the file and close nano by pressing the CTRL+X key, then press Y and Enter.

Create an empty Dockerfile file using the nano text editor.

'''nano Dockerfile'''
Add the following Dockerfile command:
'''
FROM alpine'''
This instructs the build to use the Alpine Linux base image.

Add the following Dockerfile command to the end of the Dockerfile:
'''
COPY quickstart.sh /'''
This adds the quickstart.sh script to the / directory in the image.

Add the following Dockerfile command to the end of the Dockerfile:
'''
CMD ["/quickstart.sh"]'''
This configures the image to execute the /quickstart.sh script when the associated container is created and run.

The Dockerfile should now look like:
'''
FROM alpine
COPY quickstart.sh /
CMD ["/quickstart.sh"]'''
Save the file and close nano by pressing the CTRL+X key, then press Y and Enter.

In Cloud Shell, run the following command to make the quickstart.sh script executable.
'''
chmod +x quickstart.sh'''
In Cloud Shell, run the following command to build the Docker container image in Cloud Build.
'''
gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/quickstart-image .'''
'''
Important:
Don't miss the dot (".") at the end of the command. The dot specifies that the source code is in the current working directory at build time.'''

When the build completes, your Docker image is built and pushed to Container Registry.

In the Google Cloud Console, on the Navigation menu (Navigation menu), click Container Registry > Images.

The quickstart-image Docker image appears in the list
