# Cavalry-action

This action uses [Cavalry](https://github.com/gblach/cavalry) tool
to build containers, run unittests in them and push the container images to the registry.

See [action.yml](action.yml)

## Usage

```yaml
steps:
- uses: actions/checkout@v3
- uses: gblach/cavalry-action@v1
  with:
    directory: directory
    engine: docker
    format: docker
```

To push images to the container registry you must be logged in to the registry before running cavalry.
The simplest way is to use [docker/login-action](https://github.com/marketplace/actions/docker-login)
before cavalry-action.

```yaml
steps:
  - uses: actions/checkout@v3
  -
    name: Login to GitHub Container Registry
    uses: docker/login-action@v1
    with:
      registry: ghcr.io
      username: ${{ github.actor }}
      password: ${{ secrets.GITHUB_TOKEN }}
  - uses: gblach/cavalry-action@v1
    with:
      directory: directory
      engine: docker
      format: docker
```

## Inputs

| Name | Default | Description |
| ---- | ------- | ----------- |
| `directory` | "." | Set working directory |
| `engine` | "docker" | Choose the engine: podman or docker |
| `format` | "oci" | Choose the image format: oci or docker |
| `flags` | "" | Add extra flags to the cavalry command line |
