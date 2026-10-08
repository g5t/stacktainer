# stacktainer 
ECDC stack + McCode-Plumber apptainer images

# Images
Images are defined and built in their associated repositories

| image | repository |
|-------|------------|
| ECDC binaries | [stacktainer-ecdc](https://github.com/g5t/stacktainer-ecdc) |
| ECDC binaries + McCode-Plumber | [stacktainer-splitrun](https://github.com/g5t/stacktainer-splitrun) |
| temporary Kafka server | [stacktainer-kafka](https://github.com/g5t/stacktainer-kafka) |

Built images are hosted by Github, and can be retrieved via, e.g.,

```cmd
apptainer pull oras://ghcr.io/g5t/stacktainer/splitrun:9.7
apptainer pull oras://ghcr.io/g5t/stacktainer/kafka:3.1
```

# Use
The modulefile defined in this repository is intended to be the gateway to _using_ the full stack `splitrun`.

```cmd
module load stacktainer/1.2
```

The `kafka` module file provides two commands (under `sh`-like shells only, at the moment) to `start-kafka` and `stop-kafka`.
The `splitrun` module file provides aliases to the useful binaries and programs in the image

## Off VISA
The modulefiles look for `{name}_{version}.sif` in `/apps/containers/bin/stacktainer` unless
`STACKTAINER_IMAGES` names another directory. The directory holding *this repository* must
be on `MODULEPATH`, since the modules are named `stacktainer/...`:

```cmd
module use /path/to/parent/of/stacktainer
export STACKTAINER_IMAGES=/path/to/images
module load stacktainer/1.2
```

A SIF is mounted through FUSE, which some hosts -- containers, mostly -- do not provide. If
`{name}_{version}/` exists beside the SIF it is used instead, and needs no FUSE. Make one by
extracting the image's filesystem partition:

```cmd
apptainer sif dump 4 splitrun_9.7.sif > splitrun_9.7.squashfs
unsquashfs -no-xattrs -d splitrun_9.7 splitrun_9.7.squashfs
```

`BIND` defaults to VISA's filesystems; entries that do not exist on the host are dropped
rather than stopping the container from starting.
