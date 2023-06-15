# Google Cloud Container Registry Docker Push

Github action to push a docker image to [Google Cloud's Container Registry](https://cloud.google.com/container-registry).

Other registries are supported, if you override defaults.

## Prerequisites

Set up the following resources manually in the Cloud Console or use a tool like [Terraform](https://www.terraform.io).

* Enable Artifact Registry service and create a Docker image registry
* Create Service Account with permissions to read and write to the image registry

Before this action runs, you are responsible for building the image and tagging it with all the tags you need. Example
tags may look like:

* `gcr.io/my-project-name-123456/image-name`
* `gcr.io/my-project-name-123456/image-name:latest`
* `gcr.io/my-project-name-123456/image-name:1`
* `gcr.io/my-project-name-123456/image-name:1.0`
* `gcr.io/my-project-name-123456/image-name:1.0.1`

_All_ tags will be pushed.

## Github Action Inputs

| Variable                         | Description                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| `username`                       | Registry username. Defaults to `_json_key` if not specified                 |
| `creds`                          | ***Required*** Registry password or service account JSON key                |
| `image`                          | ***Required*** Image name                                                   |
| `registry`                       | Registry host name (must match destination image), default: `gcr.io`        |


## Example Usage

**publish to google cloud artifact registry**

```yaml
uses: thermondo/gce-docker-push-action@v1
with:
  creds: ${{ secrets.GOOGLE_APPLICATION_CREDENTIALS }}
  registry: ${{ vars.CLOUDSDK_COMPUTE_REGION }}-docker.pkg.dev
  image: ${{ vars.CLOUDSDK_COMPUTE_REGION }}-docker.pkg.dev/${{ vars.CLOUDSDK_CORE_PROJECT }}/${{ vars.CONTAINER_REPOSITORY_NAME }}/image-name
```

**publish to github container registry**

```yaml
uses: thermondo/gce-docker-push-action@v1.1
with:
  username: ${{ github.actor }}
  creds: ${{ secrets.GITHUB_TOKEN }}
  registry: ghcr.io
  image: ghcr.io/namespace/image-name
```
