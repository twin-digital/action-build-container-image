# Build Container Image

Builds a container image with a sensible set of tags and labels. The image is made available via the local docker socket, and uploaded as a build artifact for further verification. The companion action, [Load Container Image](https://github.com/twin-digital/action-load-container-image), can be used to load this artifact into a downstream job.

## Usage

```yaml
- uses: @twin-digital/build-container-image@v1
  with:
    # Name of the artficat to upload the image to.
    # Default: image
    artifact: ''

    # Path to the image build context.
    # Default: .
    context: ''

    # Password for image registry authentication.
    password: ''

    # Container image registry.
    # Default: ghcr.io
    registry: ''

    # Name of the image repository.
    repository: ''

    # Username for image registry authentication.
    username: ''
```

## Metadata

This action creates images with a pre-determined set of metadata values, as described below.

### Tags

The following labels are assigned:

* Static label: `edge`
* The name of the branch
* The git SHA for the current commit

### Labels

The following Open Container annotations will be added:

* `org.opencontainers.image.title`: The repository name
* `org.opencontainers.image.description`: The repository description
* `org.opencontainers.image.description`: HTML view URL for the repository
* `org.opencontainers.image.source`: HTML view URL for the repository
* `org.opencontainers.image.created`: Build timestamp
* `org.opencontainers.image.revision`: Git commit sha
* `org.opencontainers.image.licenses`: License from the repository

## Artifact

This action uploads the image and its metadata to the named artifact. The artifact will containe two files:

* `image.tar`: The tarball containing the image layers.
* `metadata.json`: A JSON file containing the image metadata.

The JSON file contains the following top-level properties:

* `tags`: Array of all tags assigned to the image.
* `labels`: Dictionary containing key/value pairs for all labels.

## License

The contents of this repository are released under the [MIT License](LICENSE).
