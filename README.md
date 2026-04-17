postgres-rdkit
==============

This repository provides a Dockerfile for extending the official PostgreSQL debian-based Docker image, with the installation of the RDKit cartridge.

Example command to build the image (PostgreSQL 18 + RDKit 2026.03.1):

```bash
docker build -f Dockerfile \
    --build-arg postgres_image_version=18 \
    --build-arg postgres_version=18 \
    --build-arg boost_dev_version=1.88 \
    --build-arg boost_version=1.88 \
    --build-arg rdkit_git_ref=Release_2026_03_1 \
    --tag ghcr.io/dalito/postgres-rdkit:pg18-rdkit_2026_03_1 .
```

For everything related to how to run postgres, you should be able to just refer to the documentation for the [upstream image](https://hub.docker.com/_/postgres).

For everything related to how to use the RDKit cartridge, you can refer to the related [documentation](https://www.rdkit.org/docs/Cartridge.html).
