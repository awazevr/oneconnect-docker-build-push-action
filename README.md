# oneconnect-docker-build-push-action

This is a GitHub Action meant to be used as a composite action within an existing workflow. This action encapsulates setting up a checkout, build, test and push a docker image to an Elastic Container Register (ECR) in one step.

The action encapsulates the following other actions:

- [aws-actions/configure-aws-credentials](https://github.com/aws-actions/configure-aws-credentials)
- [aws-actions/amazon-ecr-login](https://github.com/aws-actions/amazon-ecr-login)
- [docker/metadata-action](https://github.com/docker/metadata-action)
- [docker/build-push-action](https://github.com/docker/build-push-action)

## Inputs

### `project-path`

**Required** Path of the project to publish

### `aws-region`

**Required** Aws region

### `aws-account-id`

**Required** Aws account id

### `ecr-repository`

**Required** ECR repository name

### `image-title`

**Required** Title of docker image

### `image-description`

**Required** Docker image description


## Usage
You can use this composite Action in your own workflow by adding:

```yml

  build:
    name: Build
    if: ${{ github.actor != 'dependabot[bot]' }}
    runs-on: ubuntu-latest
    permissions:
      actions: write
      checks: write
      contents: write
      deployments: write
      id-token: write
      issues: write
      discussions: write
      packages: write
      pages: write
      pull-requests: write
      repository-projects: write
      security-events: write
      statuses: write
    steps:

      - name: Build and Push Docker Image
        uses: awazevr/oneconnect-docker-build-push-action@v1.0.1
        with:
          project-path: "path of project"
          aws-region: ${{ secrets.AWS_REGION }}
          aws-account-id: ${{ secrets.AWS_ACCOUNT_ID }}
          ecr-repository: ${{ env.ECR_REPOSITORY }}
          image-title: "Title of docker image"
          image-description: "Description of docker image"

```

