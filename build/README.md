# Docker Build Action

You can use the Action as follows:

```yaml
name: Example building a Docker image using Kaniko 
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
    - name: Run Docker Build via Kaniko
      uses: eeveebank/github-actions-snyk/docker@master
      with:
        image: your/image-to-build
```
