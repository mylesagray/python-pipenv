# Python sample app using pipenv package manager

A basic sample which began life as part of the [Packeto Buildpack](https://github.com/paketo-buildpacks/samples) samples. Designed to illustrate how buildpacks and supply chains work to build and deploy an application. Should work just fine with VMware Tanzu Application Platform and VMware Tanzu Application Service.

## Running Locally

`pipenv run gunicorn --bind=127.0.0.1:8000 app:app`

## Viewing

`curl http://localhost:8000`

## Running on TAP

```bash
tanzu apps workload create python-sample \
  --git-repo https://github.com/benwilcock/python-pipenv \
  --git-branch main \
  --type web \
  --label app.kubernetes.io/part-of=python-sample \
  --annotation autoscaling.knative.dev/minScale=1 \
  --namespace default \
  --tail \
  --yes 
```

## Application Endpoints

1. `/`  HTML home page (shows a single page app containing a static image and some text). Contains a link to the source code.
1. `/messages` REST [GET] (shows a single hardcoded message as part of a list of messages).
1. `/versions` Plaintext (shows the version of Gunicorn used in this app).
