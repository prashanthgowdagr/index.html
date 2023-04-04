# simple-index.html-app

The index.html contains simple plai text which will be displayed in the browser.

Docker file has dependences to run webapp using Nginx-alpine 

Jenkins file has groovy script to add in config part, 
This will pull the code from the Git in 1st stage.
In 2nd stage this will build the docker file and tag them as per build number and aso tags it latest.
Then also push to docker Hub using credentials provided in the Jenkins creds.

Before running the Docker container it will also delete the old container if any running..
