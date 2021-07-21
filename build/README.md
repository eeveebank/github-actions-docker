# Snyk Docker Action

A [GitHub Action](https://github.com/features/actions) for using [Snyk](https://snyk.io) to check for
vulnerabilities in your Docker images.

_Note: The action **must** point to a tag whose manifest list only includes image layers (if only an `amd64` version
exists for example) or to a tag whose manifest list includes references to all platforms where the action is to run!_

You can use the Action as follows:

```yaml
name: Example scanning a Docker image using Snyk 
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
    - name: Run Snyk to check Docker image for vulnerabilities
      uses: eeveebank/github-actions-snyk/docker@master
      env:
        SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      with:
        image: your/image-to-test
```

The Snyk Docker Action has properties which are passed to the underlying image. These are
passed to the action using `with`.

| Property | Default        | Description                                       |
| :------- | :------------- | :------------------------------------------------ |
| args     |                | Additional arguments to pass to Snyk              |
| command  | container test | Snyk command to run; defaults to 'container test' |
| image    |                | Image to test                                     |

For example, you can choose to only report on high severity vulnerabilities and scan a `linux/arm64` image.

```yaml
name: Example workflow for Docker using Snyk 
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
    - name: Run Snyk to check Docker images for vulnerabilities
      uses: eeveebank/github-actions-snyk/docker@master
      env:
        SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      with:
        image: your/image-to-test
        args: --severity-threshold=high --platform=linux/arm64
```
