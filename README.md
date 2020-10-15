# SnykCon 2020: Building Safer Images with Snyk Container

These are the steps for the demos used in this session. The sample app is also in this repo.



---

## Setup

Assuming you've cloned this repo to your machine, the following steps will get you prepared for the demos that follow.

1. You'll need some local container tools. The steps here assume Docker but other tools should work fine.
2. You'll need Snyk, obviously. [Install instructions](https://support.snyk.io/hc/en-us/articles/360003812538-Install-the-Snyk-CLI).
3. The app in the `java-svc` folder build with `maven` - there's a readme in that directory with some details if you want to use buildpacks or jib.

---

## Blog app

The app in the `blog` directory is a Ruby app. No Ruby expertise is required to play around with it. Incidentally, if you _DO_ want to go deeper on the the full steps to fix app code in addition to container, there is a full walkthrough using this same app from [DockerCon 2020](https://github.com/jimcodified/dockercon2020).

The two shell scripts in that folder: `gooder.sh` and `badder.sh` basically just copy the original Dockerfile, Gemfile, and deployment.yaml (the _badder_ files) in to the folder (all of which exhibit many security issues!); and then copy the newer fixed files in (_gooder_ files).

You can use the Snyk CLI to test any of these things:

* Container: `snyk container test <imagename:tag> --file=Dockerfile`
  * You'll need to build the images first, of course
* Code: `snyk test --all-projects`
* Infrastructure as code: `snyk iac test deployment.yaml`

Swap the `test` subcommand with `monitor` to send the results to Snyk for updates on new vulns, etc.


## Java app

The app in the `java-svc` directory is just a simple Java starter app. The only goal there is to show building & testing containers without the need for Docker tools. There's a readme in that folder with more instructions.