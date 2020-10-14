# SnykCon 2020: Building Safer Images with Snyk Container

These are the steps for the demos used in this session. The sample app is also in this repo.

Incidentally, if you want to go deeper on the the full steps to fix app code and the container, there is a full walkthrough using this same app from [DockerCon 2020](https://github.com/jimcodified/dockercon2020).

## Setup:

Assuming you've cloned this repo to your machine, the following steps will get you prepared. 

> Note - I'm using Docker Desktop to prep but this is not required. If you prefer other container tools, like [buildah](https://buildah.io), those should work just fine as well.

```bash
cd ./alpha-blog

```


## Detecting code issues inside a container

This is shown from the Snyk UI. To see Snyk's ability to detect code inside a container you simply need to do the following:

1. Setup Snyk's integration with a compatible container registry (Docker Hub, ECR, ACR, GCR, etc)
2. Ensure you've checked "Detect application vulnerabilities" when you setup the registry integration. You can go to your "Settings --> Integrations" page to double check.
3. Add a container image that has one or more supported language frameworks in it: Python (via requirements.txt), Ruby, PHP, or Node.

## Securing the base images

### Picking a decent base image to start FROM

> Setup:

```bash
cd ./alpha-blog

```

CLI:
1. 

1. This is shown from the Snyk UI. To see this you simply need to setup Snyk integration with a compatible SCM system (GitHub, Bitbucket, GitLab, Azure repos...) and import a repo with a Dockerfile in it.