# EC2 Instance: vijay3

## Application

[Open the application](http://100.55.8.51)

**Running:** `vijaygodson/demo-website:latest`

The application container starts automatically at first boot — allow a minute after creation before opening the link.

## For developers

This repository is your playground — changes here affect only this instance.

- `src/` — the application source. Edit it and push to `main` (via a pull request): the **Build and Deploy** workflow rebuilds the image and pushes it to **your own Docker Hub repo** — `kishorereddy91/demo-website:latest` — never to the main release repo, then restarts the container on this instance with your build.
- `Dockerfile` — how `src/` is packaged.
- `config/` — the Terraform for this instance (platform-managed). Changes here re-run the Terraform workflow.

**One-time setup for builds:** in this repo's Settings → Secrets and variables → Actions, add `DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN` for **your own** Docker Hub account. The workflow uses them to push to your repo. Your repo must be public (the Docker Hub default) so this instance can pull from it without credentials.

At creation, this instance boots on the release image you picked. The first build runs on your first push that touches `src/`; from then on, the instance serves your build.

## SSH Access

[Download the .pem key](https://s3.console.aws.amazon.com/s3/object/vijay-backstage-tfstate-v2?region=us-east-1&prefix=ec2-instances/vijay3/vijay3.pem)

Private key (stored in S3 at apply time):

[Open the .pem in the S3 console](https://s3.console.aws.amazon.com/s3/object/vijay-backstage-tfstate-v2?region=us-east-1&prefix=ec2-instances/vijay3/vijay3.pem)


Or from a terminal:

    aws s3 cp s3://vijay-backstage-tfstate-v2/ec2-instances/vijay3/vijay3.pem ./vijay3.pem
    chmod 400 vijay3.pem
    ssh -i vijay3.pem ec2-user@100.55.8.51

Generate a one-hour direct-download link:

    aws s3 presign s3://vijay-backstage-tfstate-v2/ec2-instances/vijay3/vijay3.pem --expires-in 86400
