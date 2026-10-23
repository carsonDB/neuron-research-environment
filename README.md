# Dependency-only environment

This environment contains Python, CUDA PyTorch, image/data libraries and test
tools. It contains no research source, datasets, checkpoints or credentials.

The build context is restricted by `.dockerignore`. GPU access is unnecessary
for building. Publish the image to GHCR, record the immutable `@sha256:...` image
reference in `profile.json`, then run the CLI acceptance command before enabling
experiments in the local dashboard. A CPU import test does not prove GPU readiness.

`build-ghcr.yml` is a manual GitHub Actions workflow template for the separate
public `carsonDB/neuron-research-environment` repository. Only this README,
Dockerfile/profile, the two dependency files and `.dockerignore` are published.
No repository checkout from the research project is uploaded.

Keep images referenced by experiment records, the current stable digest and one
rollback digest. Delete unused versions manually after checking those references.
Do not apply automatic expiry to an image required for reproduction.
