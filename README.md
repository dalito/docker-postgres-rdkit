postgres-rdkit
==============

This repository provides a Dockerfile for extending the official PostgreSQL debian-based Docker image, with the installation of the RDKit cartridge.

The `ARG` defaults in the `Dockerfile` set what is built: the PostgreSQL base, pinned by digest, and the RDKit git ref. A local build needs no build arguments:

```bash
docker build --tag postgres-rdkit .
```

## Image tags

The `image` workflow publishes to `ghcr.io/dalito/postgres-rdkit` with tags of the form `<PostgreSQL>-rdkit-<RDKit>-<revision>`, for example `18.6-rdkit-2026.09.1-1`. The revision counts rebuilds of the same PostgreSQL and RDKit pair, such as a rebuild on a patched base. Dependabot reads the whole tag as one version, so a consumer pinning a tag gets update proposals.

A published tag is never overwritten. Consumers pin a tag together with its digest.

## Updating

- Dependabot proposes updates of the PostgreSQL base digest and of the workflow actions. It does not propose PostgreSQL major versions, which need a data-directory upgrade in every consumer.
- The `rdkit-release` workflow opens an issue once a month when RDKit has a newer release than the `Dockerfile` builds. The update is a change of the `rdkit_git_ref` default.

Every pull request builds the image, runs the RDKit test suite against the cartridge, and checks that the final image loads the extension and reports the RDKit release the `Dockerfile` names.

## Releasing

After the change is merged, tag the merge commit on `main` with the image tag and push the tag:

```bash
git tag 18.6-rdkit-2026.09.1-1
git push origin 18.6-rdkit-2026.09.1-1
```

The `image` workflow builds from the tag and refuses to publish if the tag does not name the PostgreSQL release in the image and the RDKit release in the `Dockerfile`, or if the tag is already published.

## Usage

For everything related to how to run postgres, you should be able to just refer to the documentation for the [upstream image](https://hub.docker.com/_/postgres).

For everything related to how to use the RDKit cartridge, you can refer to the related [documentation](https://www.rdkit.org/docs/Cartridge.html) or [repository](https://github.com/rdkit/rdkit).
