[![Linting](https://github.com/janbrummer/build-rpm-action/actions/workflows/lint.yml/badge.svg)](https://github.com/janbrummer/build-rpm-action/actions/workflows/lint.yml)

# Build RPM Packages GitHub Action

This action builds RPM packages in a clean, flexible environment and is based on build-deb-action by jtdor.

It is mainly a shell wrapper around `rpmbuild`, using a configurable
Docker image to install build dependencies in and build packages. Resulting
.rpm files and other build artifacts are moved to a specified place.

> [!IMPORTANT]
> This action is intended to be used with repositories that are prepared to be packaged
> in the standard RPM way. This means repositories must provide a spec file
> that contains information and rules about the package(s) to be built.
>
> If you are looking for an action that packages an arbitrary repository, you
> might prefer looking for a different action on the
> [GitHub Marketplace](https://github.com/marketplace?type=actions).

## Usage
### Basic Example
```yaml
on: push

jobs:
  build-rpms:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: janbrummer/build-rpm-action@v1
```

### Input Parameters
All input parameters have a default value or are optional.

#### `artifacts-dir`
Directory relative to the workspace where the built packages and other
artifacts will be moved to.

Defaults to `rpm/artifacts` in the workspace.

#### `docker-image`
Name of a RPM-based Docker image to use as build container or path of a
Dockerfile in the workspace to build a temporary container from.

Defaults to `fedora:latest`.

#### `extra-build-deps`
Extra packages to be installed as “build dependencies”. *This should rarely be
used, build dependencies should be specified in the spec file

Optional and empty by default.

#### `source-dir`
Directory relative to the workspace that contains the package sources.

Defaults to the workspace.

#### `spec-file`
Location of the spec file used for building the package.

Defaults to every top level spec file.
