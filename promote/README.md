<!-- NOTE: This file's contents are automatically generated. Do not edit manually. -->
# Docker Promote (Action)

Promote an existing Docker image by retagging and pushing it to a specified container registry.

This action uses `crane` to retag the image and `cosign` to sign the image.

For Signing the images, this action uses [cosign](https://github.com/sigstore/cosign) using GitHub OIDC tokens for authentication. 

This action requires a GitHub token with the following permissions:
```yaml  
  permissions:
    contents: read
    id-token: write # Needed for OIDC authentication with cosign
```

## 🔧 Inputs

|           Name           |                                                     Description                                                     |Required|         Default        |
|--------------------------|---------------------------------------------------------------------------------------------------------------------|--------|------------------------|
|        `registry`        |                                       Container registry to push the image to                                       |   Yes  |           ``           |
|    `registry_username`   |                                         Username for the container registry                                         |   No   |           ``           |
|    `registry_password`   |                                         Password for the container registry                                         |   No   |           ``           |
|          `image`         |               The image to promote. This must include the registry URL. e.g. ghcr.io/owner/repo/image               |   Yes  |           ``           |
|       `source-tag`       |                          The source image tag. This tag must already exist in the registry.                         |   Yes  |           ``           |
|       `target-tag`       |                                                The target image tag.                                                |   No   |`${{ github.ref_name }}`|
|`create-major-version-tag`|Create a tag with only the major version. Should only be used if the target_tag variable is a valid semantic version.|   No   |         `false`        |

## 📤 Outputs

|  Name  |                                        Description                                       |
|--------|------------------------------------------------------------------------------------------|
| `tags` |The tags of the promoted image. This includes the registry URL and image name and the tag.|
|`digest`|                              The digest of the pushed image                              |

## 🚀 Usage

```yaml
- name: Docker Promote
  uses: eidp/actions-docker/promote@v0
  with:
    # your inputs here
```
