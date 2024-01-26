
This is a simple Python email validation application. The app provides system information and a realtime monitoring screen with dials showing CPU, memory, IO and process information.

The app has been designed with cloud native demos & containers in mind, in order to provide a real working application for deployment, something more than "hello-world" but with the minimum of pre-reqs. It is not intended as a complete example of a fully functioning architecture or complex software design.

Typical uses would be deployment to Kubernetes, demos of Docker, CI/CD (build pipelines are provided), deployment to cloud (Azure) monitoring, auto-scaling

Method 1: Check for a valid email address using regular expression
This method either returns None (if the pattern doesn’t match) or re.MatchObject contains information about the matching part of the string. This method stops after the first match, so this is best suited for testing a regular expression more than extracting data. 


import re
 
# Make a regular expression
# for validating an Email
regex = r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,7}\b'
 
# Define a function for
# for validating an Email
def check(email):
 
    # pass the regular expression
    # and the string into the fullmatch() method
    if(re.fullmatch(regex, email)):
        print("Valid Email")
 
    else:
        print("Invalid Email")
 
# Driver Code
if __name__ == '__main__':
 
    # Enter the email
    email = "ankitrai326@gmail.com"
 
    # calling run function
    check(email)
 
    email = "my.ownsite@our-earth.org"
    check(email)
 
    email = "ankitrai326.com"
    check(email)
    
Output:

Valid Email
Valid Email
Invalid Email


Makefile
A standard GNU Make file is provided to help with running and building locally.

help                 💬 This help message
lint                 🔎 Lint & format, will not fix but sets exit code on error
lint-fix             📜 Lint & format, will try to fix errors and modify code
image                🔨 Build container image from Dockerfile
push                 📤 Push container image to registry
run                  🏃 Run the server locally using Python & Flask
deploy               🚀 Deploy to Azure Web App
undeploy             💀 Remove from Azure
test                 🎯 Unit tests for Flask app
test-report          🎯 Unit tests for Flask app (with report output)
test-api             🚦 Run integration API tests, server must be running
clean                🧹 Clean up project
Make file variables and default values, pass these in when calling make, e.g. make image IMAGE_REPO=blah/foo

Makefile Variable	Default
IMAGE_REG	ghcr.io
IMAGE_REPO	benc-uk/python-demoapp
IMAGE_TAG	latest
AZURE_RES_GROUP	temp-demoapps
AZURE_REGION	uksouth
AZURE_SITE_NAME	pythonapp-{git-sha}
The app runs under Flask and listens on port 5000 by default, this can be changed with the PORT environmental variable.

Containers
Public container image is available on GitHub Container Registry

Run in a container with:

docker run --rm -it -p 5000:5000 ghcr.io/benc-uk/python-demoapp:latest
Should you want to build your own container, use make image and the above variables to customise the name & tag.

Kubernetes
The app can easily be deployed to Kubernetes using Helm, see deploy/kubernetes/readme.md for details

GitHub Actions CI/CD
A working set of CI and CD release GitHub Actions workflows are provided .github/workflows/, automated builds are run in GitHub hosted runners








