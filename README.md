# dsa-confluence

This repo houses the Docker Build image for DSA Confluence. Any changes made to the Dockerfile are automatically pushed to ECR via a Drone pipeline.
The current version of Confluence is 7.13.8.
In order to upgrade to a new version of Confluence, update the drone.yml file as shown below
```yaml
steps:  
- name: push_to_ecr
  image: plugins/ecr
  pull: always
  settings:
    access_key:
      from_secret: AWS_ACCESS_KEY_ID
    secret_key:
      from_secret: AWS_SECRET_ACCESS_KEY
    repo: dsa/confluence
    registry: 340268328991.dkr.ecr.eu-west-2.amazonaws.com
    region: eu-west-2
    create_repository: false
    build_args:
    - APP_BUILD=${DRONE_COMMIT_SHA}
    - DOCKER_HOST=tcp://172.17.0.1:2375
    - CONFLUENCE_VERSION=7.13.8 #New version here 
    tags:
    - 7.13.8 #New version here 
    - ${DRONE_COMMIT_SHA}

```

