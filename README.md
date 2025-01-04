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

The `ORGANIZATION` and `ACCESS_TOKEN` (GitHub personal access token) environment variables are used for requesting a runner registration token.

Build the image and spin up the container in detached mode:

```
$ docker build --tag runner-image .

$ docker run \
  --detach \
  --env ORGANIZATION=<YOUR-GITHUB-ORGANIZATION> \
  --env ACCESS_TOKEN=<YOUR-GITHUB-ACCESS-TOKEN> \
  --name runner \
  runner-image
```
Make sure to replace `<YOUR-GITHUB-ORGANIZATION>` and `<YOUR-GITHUB-ACCESS-TOKEN>` with your organization and personal access token, respectively.

Take a quick look at the container logs:

```
$ docker logs runner -f
```

You should see something similar to:

```
--------------------------------------------------------------------------------
|        ____ _ _   _   _       _          _        _   _                      |
|       / ___(_) |_| | | |_   _| |__      / \   ___| |_(_) ___  _ __  ___      |
|      | |  _| | __| |_| | | | | '_ \    / _ \ / __| __| |/ _ \| '_ \/ __|     |
|      | |_| | | |_|  _  | |_| | |_) |  / ___ \ (__| |_| | (_) | | | \__ \     |
|       \____|_|\__|_| |_|\__,_|_.__/  /_/   \_\___|\__|_|\___/|_| |_|___/     |
|                                                                              |
|                       Self-hosted runner registration                        |
|                                                                              |
--------------------------------------------------------------------------------

# Authentication


√ Connected to GitHub

# Runner Registration

Enter the name of the runner group to add this runner to: [press Enter for Default]
Enter the name of runner: [press Enter for 332d0614b5e9]
This runner will have the following labels: 'self-hosted', 'Linux', 'X64'
Enter any additional labels (ex. label-1,label-2): [press Enter to skip]
√ Runner successfully added
√ Runner connection is good

# Runner settings

Enter name of work folder: [press Enter for _work]
√ Settings Saved.


√ Connected to GitHub

2021-10-23 22:36:01Z: Listening for Jobs
```


