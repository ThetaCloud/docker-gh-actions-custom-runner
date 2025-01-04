# docker-gh-actions-custom-runner
Repository contains code to build custom GitHub Actions Runner image

# Project overview

The  `start.sh`  script is responsible for registering the runner with the GitHub repository. It uses the  `ACCESS_TOKEN`  to authenticate with the GitHub API and get the registration token. The registration token is then used to configure the runner with the GitHub repository. 
The  `cleanup`  function is used to remove the runner from the GitHub repository when the script is interrupted. 
The  `run.sh`  script is responsible for starting the runner. 
This `Dockerfile` sets up a Docker image for a specific application. It includes the following steps:
1. Specifies the base image to use.
2. Copies the application code into the image.
3. Installs any necessary dependencies.
4. Exposes the required port.
5. Defines the command to run the application.


# Build

