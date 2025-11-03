<!-- NOTE: This file's contents are automatically generated. Do not edit manually. -->
# Docker Build and Push (Action)

Build and push Docker images to a container registry with multi-platform support, caching, 
and image signing using cosign.

The default versioning strategy uses semantic versioning based on Git tags, and tags images with the commit SHA on branch builds.

For Signing the images, this action uses [cosign](https://github.com/sigstore/cosign) using GitHub OIDC tokens for authentication. 

This action requires a GitHub token with the following permissions:
```yaml  
  permissions:
    contents: read
    id-token: write # Needed for OIDC authentication with cosign
```

## 🔧 Inputs

|Name                |Description                                                                                                                                                                         |Required|Default                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|--------------------------|
|`registry`          |Container registry to authenticate with                                                                                                                                             |No      |`ghcr.io`                 |
|`registry-username` |Username for the container registry                                                                                                                                                 |No      |`github`                  |
|`registry-password` |Password for the container registry                                                                                                                                                 |No      |`${{ github.token }}`     |
|`image`             |The image to build and push. This must include the registry URL. e.g. ghcr.io/owner/repo/image                                                                                      |Yes     |``                        |
|`context`           |Build context for Docker. Typically the directory containing the Dockerfile.                                                                                                        |No      |`.`                       |
|`dockerfile`        |Path to the Dockerfile                                                                                                                                                              |No      |`Dockerfile`              |
|`build_args`        |Additional build arguments for Docker                                                                                                                                               |No      |``                        |
|`platforms`         |Target platforms for the Docker image (e.g., linux/amd64,linux/arm64)                                                                                                               |No      |`linux/amd64,linux/arm64` |
|`additional_tags`   |Additional tags to apply to the image, separated by new lines. See the [docker/metadata-action](https://github.com/docker/metadata-action) documentation for supported tag formats. |No      |``                        |

## 📤 Outputs

|Name     |Description                                                                              |
|---------|-----------------------------------------------------------------------------------------|
|`tags`   |The tags of the pushed image. This includes the registry URL and image name and the tag. |
|`digest` |The digest of the pushed image                                                           |

## 🚀 Usage

```yaml
- name: Docker Build and Push
  uses: eidp/actions-docker/build-push@v0
  with:
    # your inputs here
```
