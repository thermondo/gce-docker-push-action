# Google Cloud Container Registry Docker Push

Github action to push a docker image to [Google Cloud's Container Registry](https://cloud.google.com/container-registry).

## Prerequisites

Set up the following resources manually in the Cloud Console or use a tool like [Terraform](https://www.terraform.io).

* Enable Container Registry API
* Create Service Account with Role `Storage Admin` and export a new JSON key.

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
| `creds`                          | ***Required*** Service Account JSON Key (not base64 encoded)                |
| `image`                          | ***Required*** Image name                                                   |
| `registry`                       |  Registry host name (must match destination image), default: "gcr.io"       |


## Example Usage

```
uses: thermondo/gce-docker-push-action@v1
with:
  creds: ${{ secrets.GOOGLE_APPLICATION_CREDENTIALS }}
  image: gcr.io/my-project-name-123456/image-name
```
