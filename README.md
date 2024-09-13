Containers for development

These containers are primarily for my rust development


## Bootc containers

### How to build an image

Install osbuild-selinux:

```shell
sudo dnf install -y osbuild-selinux
```

Create a `./config.toml` in the bootc Containerfile's directory

```toml
[[customizations.user]]
name = "ryanbrue"
password = "password"
groups = ["wheel"]
```

Then, run bootc image builder:

```
sudo podman run \
    --rm \
    -it \
    --privileged \
    --pull=newer \
    --security-opt label=type:unconfined_t \
    -v $(pwd)/config.toml:/config.toml:ro \
    -v $(pwd)/output:/output \
    quay.io/centos-bootc/bootc-image-builder:latest \
    --type qcow2 \
    <image>
```

Types we care about: `qcow2`, `anaconda-iso`