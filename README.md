# SnykCon 2020: Building Safer Images with Snyk Container

These are the steps for the demos used in this session. The sample app is also in this repo.

Incidentally, if you want to go deeper on the the full steps to fix app code and the container, there is a full walkthrough using this same app from [DockerCon 2020](https://github.com/jimcodified/dockercon2020).

---

## Setup:

Assuming you've cloned this repo to your machine, the following steps will get you prepared for the demos that follow.

> Note - I'm using Docker Desktop to prep but this is not required. If you prefer other container tools, like [buildah](https://buildah.io), those should work just fine as well.

```bash
cd ./alpha-blog
docker build -t snykcon-blog:v0 .

# once the above build starts it's OK to run this build concurrently
docker build -t snykcon-blog:vFix . -f Dockerfile.rubyfixes

# after builds have finished:
snyk container monitor snykcon-blog:v0 --file=Dockerfile

# java cnb
cd ../java-svc
# brew install maven - if you haven't already
mvn spring-boot:build-image
```

---

## Detecting code issues inside a container

This is shown from the Snyk UI. To see Snyk's ability to detect code inside a container you simply need to do the following:

1. Setup Snyk's integration with a compatible container registry (Docker Hub, ECR, ACR, GCR, etc)
2. Ensure you've checked "Detect application vulnerabilities" when you setup the registry integration. You can go to your "Settings --> Integrations" page to double check.
3. Add a container image that has one or more supported language frameworks in it: Python (via requirements.txt), Ruby, PHP, or Node.

## Securing the base images

### Picking a decent base image to start FROM

CLI - 2 windows
1. `cd alpha-blog`
2. `snyk container test snykcon-blog:v0 --file=Dockerfile`
3. When scanning is complete you should get a very long list of vulns and see the bsase image recommendations. At the time of of this writing, one of the recommndations is to switch to `ruby:2.5-slim` which is what we did when we build the `snykcon-blog:vFix` image.
4. Switch to Snyk UI and show same results in the Snyk console
5. `snyk container test snykcon-blog:vFix --file=Dockerfile.rubyfixes`

### Shifting even further left - Dockerfile scanning
1. Show integration with Github: `purpledobie/blog` (already imported)
2. In UI - show `purpledobie/blog` GH project --> `alpha-blog/Dockerfile`
3. `snyk container test purpledobie/java-svc:cnb`

